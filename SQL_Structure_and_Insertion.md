```markdown
# Table Structures and Data Insertion for Healthcare Appointment Management System (HAMS)
```
## 1. Patients Table

### Structure
```sql
CREATE TABLE Patients (
    PatientID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DateOfBirth DATE,
    Email VARCHAR(100),
    IsActive BIT
);
```

### Sample Data Insertion
```sql
INSERT INTO Patients (PatientID, FirstName, LastName, DateOfBirth, Email, IsActive) VALUES
(1, 'John', 'Doe', '1985-05-15', 'ram.krishna@example.com', 1),
(2, 'Jane', 'Smith', '1990-03-25', 'jhon.snow@example.com', 1);
```

## 2. Doctors Table

### Structure
```sql
CREATE TABLE Doctors (
    DoctorID INT PRIMARY KEY,
    DoctorName VARCHAR(100),
    DepartmentID INT,
    Availability VARCHAR(100)
);
```

### Sample Data Insertion
```sql
INSERT INTO Doctors (DoctorID, DoctorName, DepartmentID, Availability) VALUES
(1, 'Dr. Robert White', 1, 'Mon-Fri 9 AM - 5 PM'),
(2, 'Dr. Mukesh Brown', 2, 'Mon-Fri 10 AM - 6 PM');
```

## 3. Departments Table

### Structure
```sql
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
```

### Sample Data Insertion
```sql
INSERT INTO Departments (DepartmentID, DepartmentName) VALUES
(1, 'Cardiology'),
(2, 'Neurology');
```

## 4. Appointments Table

### Structure
```sql
CREATE TABLE Appointments (
    AppointmentID INT PRIMARY KEY,
    PatientID INT,
    DoctorID INT,
    AppointmentDate DATETIME,
    Status VARCHAR(50)
);
```

### Sample Data Insertion
```sql
INSERT INTO Appointments (AppointmentID, PatientID, DoctorID, AppointmentDate, Status) VALUES
(1, 1, 1, '2024-09-20 10:00:00', 'Scheduled'),
(2, 2, 2, '2024-09-21 11:30:00', 'Scheduled');
```

## 5. Feedback Table

### Structure
```sql
CREATE TABLE Feedback (
    FeedbackID INT PRIMARY KEY,
    PatientID INT,
    DoctorID INT,
    FeedbackRating INT,
    Comments TEXT
);
```

### Sample Data Insertion
```sql
INSERT INTO Feedback (FeedbackID, PatientID, DoctorID, FeedbackRating, Comments) VALUES
(1, 1, 1, 5, 'Excellent service!'),
(2, 2, 2, 4, 'Very knowledgeable doctor.');
```

## Data Generation
We can use data generation tools like:
- **[Mockaroo](https://www.mockaroo.com/)**: Create custom datasets with various data types.
- **[GenerateData](https://generatedata.com/)**: Generate random data for testing.
- Also will update the kaggle data link soon.
