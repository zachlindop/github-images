# Doctor Workload Analysis

## Project Overview
This analysis summarizes doctor appointments and unique patients in the hospital. 
It helps identify which doctors are busiest and highlights opportunities to balance workload.

## SQL Query
```sql
WITH appointment_summary AS (
    SELECT 
        d.id AS doctor_id,
        d.first_name || ' ' || d.last_name AS doctor_name,
        a.id AS appointment_id,
        p.id AS patient_id
    FROM doctors d
    LEFT JOIN appointments a 
        ON d.id = a.doctor_id
    LEFT JOIN patients p
        ON a.patient_id = p.id
)
SELECT 
    doctor_id,
    doctor_name,
    COUNT(appointment_id) AS total_appointments,
    COUNT(DISTINCT patient_id) AS unique_patients
FROM appointment_summary
GROUP BY 
    doctor_id,
    doctor_name
ORDER BY 
    total_appointments DESC;