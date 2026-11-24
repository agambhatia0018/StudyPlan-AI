# Technical Report: AI-Powered Timetable and Study Plan Generator

**Course:** SCSE4041 – Prompt Engineering  
**Milestone:** Milestone 2  
**Team ID:** PE-B65-56  
**Batch:** B65-80  
**Team Name:** PromptPioneers  
**Team Leader:** Saksham Kumar (S24CSEU2007)  
**Team Members:**  
- S24CSEU2007 – Saksham Kumar
- S24CSEU2030 – Team Member 2
- S24CSEU2003 – Team Member 3
- S24CSEU2002 – Team Member 4
- S24CSEU2005 – Team Member 5
- S24CSEU0764 – Team Member 6

---

## 1. Executive Summary & Problem Statement

College students frequently struggle with managing multiple subjects, varying exam schedules, differing topic difficulties, personal commitments, and realistic daily cognitive limits. Traditional timetable generators often rely on static schedules or naive generative AI prompts that produce unvalidated, conflicting, or hallucinated timetables (such as scheduling sessions during class commitments, exceeding study-hour limits, or neglecting subjects with imminent exams).

**StudyPlan AI** addresses this challenge by combining a rigorous **three-stage prompt engineering architecture** with **deterministic Python validation** and heuristic scheduling algorithms. Generative AI outputs are never assumed to be valid without programmatic verification.

---

## 2. System Architecture

StudyPlan AI is structured as a modular Python application with a Streamlit interface:

```text
StudyPlan-AI/
├── app.py                      # Multi-page dashboard entry point
├── config.py                   # Central configurations & constants
├── modules/
│   ├── ai_service.py           # OpenAI API client & tolerant timetable parser
│   ├── prompt_engine.py        # Versioned prompt builder (V1, V2, V3) & diff engine
│   ├── constraint_validator.py # Deterministic timetable & profile validation engine
│   ├── timetable_generator.py  # Heuristic rule-based local planner
│   ├── priority_analyzer.py    # Exam urgency, difficulty & priority scoring
│   ├── revision_planner.py     # Spaced revision & mock-test allocation
│   ├── evaluation.py           # Automated test harness for 12 scenarios
│   ├── export_manager.py       # PDF, CSV, and JSON data exporters
│   └── ui.py                   # Streamlit UI styling and component helpers
├── pages/                      # 8 Dedicated multi-page feature views
├── prompts/                    # Externalized prompt templates (prompt_v1, v2, v3)
├── results/                    # Prompt iteration logs & documentation
└── tests/                      # Automated unit test suite & scenario test cases
```

### Key Architectural Components:
1. **Student Profile & Input Management:** Captures subjects, exam dates, difficulty ratings, priorities, completed topics, weekly available days, study windows, session/break durations, and fixed commitments.
2. **Deterministic Priority Scoring:** Uses a mathematical formula rather than model speculation:
   $$\text{Score} = 0.45 \times \text{Exam Urgency} + 0.30 \times \text{Subject Difficulty} + 0.25 \times \text{Personal Priority}$$
3. **Prompt Engine & Tolerant Parser:** Compiles structured JSON student profiles into versioned prompt templates and parses markdown/JSON responses into clean Pandas DataFrames.
4. **Constraint Validation Engine:** Independent Python validation pipeline verifying zero overlapping sessions, commitment compliance, preferred study windows, session duration integrity, and near-exam coverage warnings.
5. **Local Fallback Planner:** Rule-based scheduling heuristic enabling full application usage without an API key.

---

## 3. Tools and Models Used

- **Primary AI Model:** OpenAI GPT-4o-mini (temperature: 0.2 for deterministic adherence to constraints and JSON formatting).
- **Execution Environments:**
  - *API Mode:* Direct programmatic invocation via the official OpenAI Python SDK.
  - *Prompt Mode:* Interactive copy/paste pipeline compatible with ChatGPT, Gemini 2.5 Flash in Google AI Studio, or Claude.
- **Frontend & UI:** Streamlit with Plotly visualizations for study allocation and workload distribution.
- **Data & Processing Libraries:** Pandas, Python standard `datetime`, `difflib`, `json`.
- **Export Engine:** ReportLab for dynamic PDF timetable generation.
- **Testing Harness:** Python `unittest` framework and a custom deterministic scenario evaluation runner.

---

## 4. Prompt Engineering & Iterative Design

The project employs an iterative prompt engineering progression across three distinct versions:

### V1 – Baseline Prompt (`prompts/prompt_v1.txt`)
- **Structure:** Zero-shot directive instructing the model to act as a study-planning assistant and generate a day-wise timetable.
- **Changes / Features:** Basic timetable request covering subjects and dates.
- **Reason:** Establish a minimal baseline to evaluate raw model scheduling logic.
- **Limitations Identified:** Unstructured outputs, hallucinated session times, overlapping sessions, lack of consideration for daily study limits or existing recurring commitments.

### V2 – Constraint-Aware Prompt (`prompts/prompt_v2.txt`)
- **Structure:** Role prompting combined with explicit constraint enumeration.
- **Changes / Features:** Added exam proximity weighting, difficulty, student priority, weekly available days, preferred time windows, break insertions, and strict non-overlap constraints.
- **Reason:** Eliminate common scheduling collisions and direct model attention to urgent/difficult subjects.
- **Limitations Identified:** Outputs varied between Markdown tables and free text, making automated parsing unreliable; no standardized error/conflict reporting mechanism.

### V3 – Optimized Structured-Output Prompt (`prompts/prompt_v3.txt`)
- **Structure:** Few-shot guided system prompt with strict output schema contract (JSON Schema), input validation instructions, and edge-case conflict protocols.
- **Changes / Features:** 
  - Strict JSON-only response contract with exact keys (`assumptions`, `conflicts`, `warnings`, `timetable`).
  - Mandatory 24-hour time formatting (`HH:MM`) and explicit duration consistency checks.
  - Inclusion of distinct session types (`Learning`, `Practice`, `Revision`, `Mock Test`, `Break`).
  - Instructions to flag insufficient preparation time and schedule shortfalls explicitly rather than producing impossible plans.
- **Reason:** Achieve 100% deterministic parseability and robust handling of conflicting commitments and incomplete student inputs.

---

## 5. Test Results and Evaluation Matrix

The application includes an automated test harness (`modules/evaluation.py`) executing 12 deterministic test scenarios covering normal, edge, and invalid inputs:

| Test ID | Test Scenario / Input Description | Expected Output | Actual Output | Status |
| :--- | :--- | :--- | :--- | :---: |
| **TC-01** | Normal profile with two dated subjects (Algorithms, Databases) | Non-empty timetable passing Python constraint validator | 196 sessions; validator valid=True | **PASS** |
| **TC-02** | Three difficult, high-priority subjects (AI, Networks, Security) | Local plan covers all three hard subjects proportionally | 60 study sessions; all three hard subjects represented | **PASS** |
| **TC-03** | One hard subject with an exam tomorrow | At least one session scheduled today before the exam | 7 session/break rows dated today | **PASS** |
| **TC-04** | One available study hour per day constraint | No scheduled day exceeds one hour of study time | max planned study/day=1h; daily-limit issue=False | **PASS** |
| **TC-05** | Twelve subjects with staggered examination dates | All 12 input subjects mapped to scheduled sessions | 12 input subjects; 12 scheduled subjects | **PASS** |
| **TC-06** | Daily recurring class commitment (09:00 - 11:00) | Zero overlap between study sessions and commitments | commitment conflicts detected=0 | **PASS** |
| **TC-07** | Subject provided without an exam date | Validation engine flags missing mandatory exam date | missing exam date detected=True | **PASS** |
| **TC-08** | Zero available daily study hours specified | Profile validation rejects non-positive daily study hours | zero available hours detected=True | **PASS** |
| **TC-09** | Invalid calendar exam date (e.g., 2026-02-30) | Profile validation detects and reports invalid calendar date | invalid calendar date detected=True | **PASS** |
| **TC-10** | Two timetable sessions overlapping by 30 minutes | Timetable validator flags collision in overlap check | overlap detected=True | **PASS** |
| **TC-11** | Extremely high request of 16 study hours per day | System raises cognitive workload warning | 16-hour request warning detected=True | **PASS** |
| **TC-12** | Exam tomorrow with zero sessions scheduled for it | Validator warns about unaddressed imminent examination | little/no preparation warning detected=True | **PASS** |

**Summary:** 12/12 Automated Test Scenarios Passed (100% Pass Rate).

---

## 6. Limitations and Future Scope

1. **State Persistence:** Currently utilizes Streamlit session state for data privacy without a database backend. Long-term progress tracking across semesters requires persistent cloud storage (e.g., PostgreSQL or Supabase).
2. **Syllabus Granularity:** Priority heuristics calculate urgency and difficulty but cannot evaluate internal syllabus module volume without direct syllabus ingestion (e.g., PDF textbook/syllabus parsing via multimodal RAG).
3. **Dynamic Schedule Adaptation:** Future iterations could incorporate real-time calendar syncing (Google Calendar / Outlook API) to automatically reschedule missed sessions when unplanned student commitments arise.

---

## 7. Conclusion

StudyPlan AI demonstrates how combining disciplined prompt engineering (progressing from baseline to schema-constrained prompts) with deterministic programmatic verification creates a reliable, collision-free, and pedagogically sound academic planning tool.
