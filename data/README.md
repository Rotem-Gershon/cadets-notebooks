# CADets Course Dataset: Internal-Medicine Admissions (synthetic)

A fully synthetic dataset of **2,000 adult admissions to internal-medicine wards** in three hospitals, January 2023 to December 2024. One row is one admission. No real patient is represented. The same dataset is used in every notebook of the course.

During this period an **AI deterioration model** was rolled out, hospital by hospital. When a patient's model score was high, an **alert** fired to the ward team, which could lead to an **early consult** (a senior or rapid-response consult within 6 hours of admission).

## Files and release schedule

| File | Released | Contents |
|---|---|---|
| `cadets_admissions_release1_core.csv` | Day 1 | Patient characteristics, background disease, admission vitals and labs, outcomes (29 columns) |
| `cadets_admissions_release2_intervention.csv` | Day 4 | Release 1 + `alert_fired`, `early_consult` (31 columns) |
| `cadets_admissions_release3_full.csv` | Day 6 | Release 2 + `hospital`, `admission_date` (33 columns) |
| Clinical notes (free text, same patients) | Day 6 | To be produced later |

`patient_id` is the same across all releases, so files can be joined.

## Data dictionary

| Column | Type | Values / units | Notes |
|---|---|---|---|
| `patient_id` | ID | P00001–P02000 | One admission per patient |
| `hospital` | categorical | A, B, C | Release 3 |
| `admission_date` | date | 2023-01-01 to 2024-12-31 | Release 3 |
| `age` | integer | years, 18–100 | |
| `sex` | categorical | F, M | |
| `bmi` | continuous | kg/m² | Has missing values |
| `smoking_status` | categorical | never, former, current | Has missing values |
| `ses_level` | ordinal | low, medium, high | Socioeconomic level |
| `population_sector` | categorical | group_1, group_2, group_3 | Neutral labels for population groups; used in fairness lessons |
| `diabetes` | binary | 0/1 | Background disease |
| `hypertension` | binary | 0/1 | Background disease |
| `heart_failure` | binary | 0/1 | Background disease |
| `ckd` | binary | 0/1 | Chronic kidney disease |
| `copd` | binary | 0/1 | Background disease |
| `active_cancer` | binary | 0/1 | Background disease |
| `admit_diagnosis_group` | categorical | infection, cardiac, respiratory, gi, other | Main reason for admission |
| `heart_rate` | integer | beats/min | First value on admission |
| `systolic_bp` | integer | mmHg | First value on admission |
| `resp_rate` | integer | breaths/min | First value on admission |
| `spo2` | integer | % | First value on admission |
| `creatinine` | continuous | mg/dL | First value on admission |
| `hemoglobin` | continuous | g/dL | First value on admission |
| `wbc` | continuous | ×10³/µL | First value on admission |
| `sodium` | integer | mmol/L | First value on admission |
| `albumin` | continuous | g/dL | Has missing values (not always ordered) |
| `crp` | continuous | mg/L | Has missing values (not always ordered) |
| `alert_fired` | binary | 0/1 | AI deterioration alert fired during the first hours. Always 0 before the model went live in that hospital. Release 2 |
| `early_consult` | binary | 0/1 | Senior / rapid-response consult within 6 h of admission. Release 2 |
| `los_days` | continuous | days | **Outcome (continuous):** length of stay |
| `icu_transfer` | binary | 0/1 | **Outcome (binary):** transfer to ICU during the admission |
| `in_hospital_death` | binary | 0/1 | **Outcome (binary):** death during the admission |
| `readmit_30d` | binary | 0/1, empty if died | **Outcome (binary):** readmission within 30 days of discharge. Empty for patients who died in hospital (not at risk) |
| `discharge_destination` | categorical | home, rehab, long_term_care, died | **Outcome (categorical)** |

## Things to know

- All values are within plausible clinical ranges; there are no invalid entries.
- Missing values are realistic: about 11% for `bmi`, 10% for `smoking_status`, 29% for `albumin`, 12% for `crp`. Why they are missing is part of the lessons.
- `readmit_30d` is empty by design for patients who died: they could not be readmitted.
- Outcome rates: in-hospital death ~9%, ICU transfer ~10%, 30-day readmission ~18% (of survivors), median LOS ~5 days.

The generator, the true effects and an answer key are kept by the course staff and are not part of the participant materials.
