# Academic Module Sample Data

Use `thisapp.Seed_Academic_Sample_Data()` after the app is uploaded to create a large demo dataset. The seed is guarded by academic year `2025-2026`; if that year already exists, it returns without adding duplicates.

## Insert Order
1. Academic_Years
2. Subjects
3. Staff
4. Classes
5. Class_Subjects
6. Students
7. Exams
8. Lesson_Plans
9. Attendance
10. Marks

## Dataset Summary
| Form | Sample Count | Notes |
|---|---:|---|
| Academic_Years | 1 | Active year 2025-2026 |
| Subjects | 6 | Math, English, Science, History, Computer Science, Art |
| Staff | 6 | Teaching, academic admin, and office sample users |
| Classes | 5 | Grades 6A, 6B, 7A, 8A, 9A |
| Class_Subjects | 6 | Active subject-teacher mappings |
| Students | 25 | Demo students distributed across all classes |
| Exams | 4 | Completed and scheduled assessments |
| Lesson_Plans | 4 | Completed, in-progress, and planned lessons |
| Attendance | 15 | Present/Absent/Late/Excused examples |
| Marks | 15 | Pass/fail distribution for dashboard testing |

## Import-Ready Reference Values

### Academic Years
| Academic_Year_Name | Start_Date | End_Date | Status |
|---|---|---|---|
| 2025-2026 | 01-Apr-2025 | 31-Mar-2026 | Active |

### Subjects
| Subject_Code | Subject_Name | Subject_Type | Status |
|---|---|---|---|
| MATH | Mathematics | Core | Active |
| ENG | English | Language | Active |
| SCI | Science | Core | Active |
| HIST | History | Core | Active |
| COMP | Computer Science | Practical | Active |
| ART | Art | Co-curricular | Active |

### Staff
| Staff_Code | Name | Email | Role | Status |
|---|---|---|---|---|
| STF001 | Anita Rao | anita.rao@example.edu | Teaching Staff | Active |
| STF002 | Rohit Menon | rohit.menon@example.edu | Teaching Staff | Active |
| STF003 | Meera Kapoor | meera.kapoor@example.edu | Teaching Staff | Active |
| STF004 | Sanjay Iyer | sanjay.iyer@example.edu | Academic Admin | Active |
| STF005 | Farah Khan | farah.khan@example.edu | Office Staff | Active |
| STF006 | Vikram Shah | vikram.shah@example.edu | Teaching Staff | Active |

### Classes
| Class_Code | Class_Name | Section | Academic_Year | Class_Teacher | Capacity | Status |
|---|---|---|---|---|---:|---|
| G6-A | Grade 6 | A | 2025-2026 | STF001 | 35 | Active |
| G6-B | Grade 6 | B | 2025-2026 | STF002 | 35 | Active |
| G7-A | Grade 7 | A | 2025-2026 | STF003 | 35 | Active |
| G8-A | Grade 8 | A | 2025-2026 | STF006 | 35 | Active |
| G9-A | Grade 9 | A | 2025-2026 | STF004 | 40 | Active |

### Students
25 demo students are created with admission numbers `ADM2025001` through `ADM2025025`, across classes G6-A, G6-B, G7-A, G8-A, and G9-A. Parent contact fields use example.com addresses and demo phone numbers.

### Exams and Marks
The seed includes three completed exams with marks and one scheduled practical exam. Failed marks are intentionally included so `Failed_Students` and the dashboard show useful data.

## Notes
- Seeded lookup relationships use inserted record IDs, so the function is safer than manual import for linked records.
- The seed intentionally includes a few absences, late attendance records, and failed marks for dashboard validation.
- If you need CSV files instead of this reference, ask me to generate per-form CSV files.