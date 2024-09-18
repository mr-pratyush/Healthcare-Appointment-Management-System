
# SQL Solutions for Healthcare Appointment Management System (HAMS)


### 1. Find All Active Patients
**Purpose**: To manage patient records and facilitate communication.  
```sql
SELECT PatientID, FirstName, LastName, DateOfBirth, Email 
FROM Patients
WHERE IsActive = 1;
```

### 2. Today's Appointments
**Purpose**: To enhance daily operations by showing today's appointments.  
```sql
SELECT p.FirstName, p.LastName, a.AppointmentTime, d.DoctorName 
FROM Appointments a
JOIN Patients p ON a.PatientID = p.PatientID
JOIN Doctors d ON a.DoctorID = d.DoctorID
WHERE CAST(a.AppointmentDate AS DATE) = CAST(GETDATE() AS DATE);
```

### 3. Count of Patients by Department
**Purpose**: To analyze how many patients visit each department.  
```sql
SELECT d.DepartmentName, COUNT(p.PatientID) AS PatientCount 
FROM Departments d
LEFT JOIN Patients p ON d.DepartmentID = p.DepartmentID
GROUP BY d.DepartmentName
ORDER BY PatientCount DESC;
```

### 4. Monthly Appointment Trends
**Purpose**: To identify trends in appointments over the months.  
```sql
SELECT YEAR(AppointmentDate) AS Year, MONTH(AppointmentDate) AS Month, COUNT(*) AS AppointmentCount 
FROM Appointments 
GROUP BY YEAR(AppointmentDate), MONTH(AppointmentDate)
ORDER BY Year, Month;
```

### 5. Average Feedback Rating by Doctor
**Purpose**: To analyze feedback ratings for doctors.  
```sql
SELECT DoctorID, AVG(FeedbackRating) AS AverageRating 
FROM Feedback 
GROUP BY DoctorID 
ORDER BY AverageRating DESC;
```

### 6. Top 5 Doctors by Appointment Count
**Purpose**: To find doctors with the highest number of appointments.  
```sql
SELECT d.DoctorID, d.DoctorName, COUNT(a.AppointmentID) AS AppointmentCount 
FROM Appointments a
JOIN Doctors d ON a.DoctorID = d.DoctorID
GROUP BY d.DoctorID, d.DoctorName 
ORDER BY AppointmentCount DESC 
OFFSET 0 ROWS FETCH NEXT 5 ROWS ONLY;
```

### 7. Cumulative Appointment Count by Day
**Purpose**: To show a running total of appointments over time.  
```sql
SELECT AppointmentDate, 
       COUNT(*) AS DailyCount,
       SUM(COUNT(*)) OVER (ORDER BY AppointmentDate) AS CumulativeCount 
FROM Appointments
GROUP BY AppointmentDate
ORDER BY AppointmentDate;
```

### 8. Patients with Most Appointments
**Purpose**: To identify patients with the highest number of appointments.  
```sql
SELECT p.PatientID, p.FirstName, p.LastName, COUNT(a.AppointmentID) AS AppointmentCount 
FROM Patients p
JOIN Appointments a ON p.PatientID = a.PatientID
GROUP BY p.PatientID, p.FirstName, p.LastName 
HAVING COUNT(a.AppointmentID) > 5
ORDER BY AppointmentCount DESC;
```

### 9. Average Appointment Duration by Doctor
**Purpose**: To calculate the average duration of appointments by doctor.  
```sql
SELECT d.DoctorID, d.DoctorName, 
       AVG(DATEDIFF(MINUTE, a.StartTime, a.EndTime)) AS AverageDuration 
FROM Appointments a
JOIN Doctors d ON a.DoctorID = d.DoctorID
GROUP BY d.DoctorID, d.DoctorName;
```

### 10. No-Show Rates by Patient
**Purpose**: To analyze which patients frequently miss appointments.  
```sql
WITH NoShowCounts AS (
    SELECT PatientID, COUNT(*) AS NoShowCount 
    FROM Appointments 
    WHERE Status = 'No Show' 
    GROUP BY PatientID
)
SELECT p.PatientID, 
       p.FirstName, 
       p.LastName, 
       n.NoShowCount
FROM Patients p
JOIN NoShowCounts n ON p.PatientID = n.PatientID
ORDER BY n.NoShowCount DESC;
```
## Conclusion
<div style="color: blue;"> <p>  This query helps us easily identify all active patients in the system. By focusing only on those currently receiving care, healthcare providers can ensure effective management of patient communications and records, ultimately enhancing patient care.</p> </div> 
