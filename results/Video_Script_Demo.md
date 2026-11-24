# StudyPlan AI – Video Demo / Reel Script (90–150 Seconds)

**Course:** SCSE4041 – Prompt Engineering  
**Project Title:** AI-Powered Timetable and Study Plan Generator  
**Team Name:** PromptPioneers  
**Team ID:** PE-B65-56  
**Target Duration:** ~120 seconds (Allowed: 90 to 150 seconds)

---

## 🎬 Quick Instructions Before Recording:
1. Open Streamlit app in your browser: `streamlit run app.py`
2. Keep your screen recording tool ready (OBS Studio, Windows Game Bar `Win + G`, or Loom).
3. Keep screen resolution clear (1080p full screen).
4. One person speaks, or team members split sections.

---

## ⏱️ Video Breakdown & Script (Hinglish & English)

### 0:00 – 0:20 (Intro & Problem Statement)
- **Screen Action:** Home / Dashboard page open karein, title aur team name dikhayein.
- **Kya Bolna Hai (Hinglish):**
  > "Hello everyone! Hum hain Team PromptPioneers (Team ID: PE-B65-56), and our project is **AI-Powered Timetable and Study Plan Generator** for SCSE4041 Prompt Engineering.  
  > College students ke paas multiple subjects, varying exam dates, aur tight schedules hote hain. Lekin normal AI prompts aksar unrealistic timetable generate karte hain jisme timings overlap hoti hain aur fixed commitments ignore ho jaati hain. Is problem ko solve karne ke liye humne banaya hai **StudyPlan AI**."
- **English Option:**
  > "Hello everyone! We are Team PromptPioneers (Team ID: PE-B65-56), presenting our project **AI-Powered Timetable and Study Plan Generator**. Students often struggle to balance multiple exams and daily commitments, and generic LLMs frequently hallucinate conflicting schedules. StudyPlan AI bridges this gap with rigorous prompt engineering and deterministic Python validation."

---

### 0:20 – 0:45 (Student Profile & Transparent Priority Scoring)
- **Screen Action:** Navigate to **Student Information** page -> dikhayein subjects add kiye hue hain, exam dates, daily hours, aur class commitment (e.g., 09:00 - 11:00). Then click on **Exam & Subject Analysis**.
- **Kya Bolna Hai (Hinglish):**
  > "Sabse pehle **Student Information** page par student apne subjects, exam dates, difficulty, daily available hours aur recurring commitments add karta hai.  
  > Next, **Exam & Subject Analysis** page par hamara deterministic formula exam urgency (45%), difficulty (30%), aur personal priority (25%) calculate karke transparent priority score deta hai—ye purely mathematical calculation hai, koi AI guesswork nahi."
- **English Option:**
  > "On the **Student Information** page, students input their subjects, exam dates, difficulty levels, daily hours, and daily commitments. On the **Exam Analysis** page, our deterministic formula calculates a transparent priority score based on 45% exam proximity, 30% difficulty, and 25% personal priority."

---

### 0:45 – 1:15 (Prompt Engineering Lab – Core Milestone 2 Focus)
- **Screen Action:** Navigate to **Prompt Engineering Lab** page. Toggle between **V1 – Baseline**, **V2 – Constraint-aware**, and **V3 – Optimized**, aur side-by-side diff dikhayein.
- **Kya Bolna Hai (Hinglish):**
  > "Ab aate hain project ke core part par—**Prompt Engineering Lab**. Humne 3 iterations develop kiye hain:  
  > - **V1 Baseline:** Simple zero-shot prompt tha, jisme timetable unstructured aur overlapping tha.  
  > - **V2 Constraint-aware:** Isme humne study windows, breaks, aur commitment restrictions add kiye.  
  > - **V3 Optimized:** Ye hamara final JSON-contract prompt hai, jisme strict output schema, 24-hour time constraints, revision/mock planning, aur conflict-handling protocols enforce kiye gaye hain. Diff viewer me aap clearly prompt improvements dekh sakte hain."
- **English Option:**
  > "In the **Prompt Engineering Lab**, we engineered three prompt iterations: V1 Baseline was a naive request that caused overlaps; V2 Constraint-Aware added study windows, breaks, and commitments; and V3 Optimized enforced a strict JSON schema contract, 24-hour time validation, and conflict protocols. The live diff viewer highlights our iterative refinements."

---

### 1:15 – 1:40 (Timetable Generation & Python Constraint Validator)
- **Screen Action:** Navigate to **Generate Study Plan** -> click **Generate Local Plan** (or show Prompt Mode) -> Table populate hote hi **Timetable Validator** tab/page par click karein. Green checks dikhayein.
- **Kya Bolna Hai (Hinglish):**
  > "Yahan **Generate Study Plan** me hum API Mode ya zero-cost Prompt Mode se timetable generate kar sakte hain.  
  > Aur sabse crucial feature: hum AI output ko blind trust nahi karte! Hamara **Timetable Validator** Python me run hota hai aur check karta hai:  
  > - Koi time overlap toh nahi hai?  
  > - Class commitments ke dauran study schedule toh nahi hui?  
  > - Aur daily limit exceed toh nahi hui?  
  > Sabhi checks pass hone ke baad hi plan student ke liye validate hota hai."
- **English Option:**
  > "Under **Generate Study Plan**, timetables are generated via API Mode or Prompt Mode. Crucially, we never trust AI outputs blindly. Our deterministic **Timetable Validator** programmatically checks for session overlaps, commitment collisions, and daily study hour violations before confirming the plan."

---

### 1:40 – 2:00 (Testing & Evaluation Page & Conclusion)
- **Screen Action:** Navigate to **Testing & Evaluation** page. Click **Run All Scenarios** -> 12/12 PASS status aur CSV download button dikhayein. Then switch to **Export** to show PDF download.
- **Kya Bolna Hai (Hinglish):**
  > "Final verification ke liye, **Testing & Evaluation** page par humne 12 automated test cases banaye hain—normal, edge, aur invalid cases jaise invalid dates aur overlapping slots. All 12 scenarios are passing with 100% success rate!  
  > Final timetable ko student PDF, CSV, ya JSON me export kar sakta hai.  
  > Thank you! Team PromptPioneers signing off."
- **English Option:**
  > "Finally, our **Testing & Evaluation** page independently runs 12 automated test scenarios covering edge cases like zero hours, invalid calendar dates, and session collisions—achieving a 100% pass rate. Students can export their verified plan to PDF, CSV, or JSON. Thank you!"

---

## 💡 Quick Tips for High Marks:
- Keep the video between **100 and 125 seconds** (so it is safely inside the 90–150s limit).
- Make sure cursor movements are smooth and text is readable.
- If recording in Hinglish, speak confidently and use formal technical terms (e.g., *deterministic validation, prompt iterations, constraint-aware, JSON schema contract*).
