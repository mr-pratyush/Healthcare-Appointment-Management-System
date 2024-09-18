# Database Schema for Healthcare Appointment Management System (HAMS)

## Overview
This document outlines the structure of the database used in the Healthcare Appointment Management System, including tables, their columns, and relationships.

## Tables

### 1. Patients
- **PatientID** (INT, Primary Key): Unique identifier for each patient.
- **FirstName** (VARCHAR): Patient's first name.
- **LastName** (VARCHAR): Patient's last name.
- **DateOfBirth** (DATE): Patient's date of birth.
- **Email** (VARCHAR): Patient's email address.
- **IsActive** (BIT): Status indicating if the patient is currently active.

### 2. Doctors
- **DoctorID** (INT, Primary Key): Unique identifier for each doctor.
- **DoctorName** (VARCHAR): Name of the doctor.
- **DepartmentID** (INT, Foreign Key): Identifier for the department the doctor belongs to.
- **Availability** (VARCHAR): Doctor’s availability schedule.

### 3. Departments
- **DepartmentID** (INT, Primary Key): Unique identifier for each department.
- **DepartmentName** (VARCHAR): Name of the department.

### 4. Appointments
- **AppointmentID** (INT, Primary Key): Unique identifier for each appointment.
- **PatientID** (INT, Foreign Key): Identifier for the patient.
- **DoctorID** (INT, Foreign Key): Identifier for the doctor.
- **AppointmentDate** (DATETIME): Date and time of the appointment.
- **Status** (VARCHAR): Current status of the appointment (e.g., Scheduled, Completed, No Show).

### 5. Feedback
- **FeedbackID** (INT, Primary Key): Unique identifier for each feedback entry.
- **PatientID** (INT, Foreign Key): Identifier for the patient giving feedback.
- **DoctorID** (INT, Foreign Key): Identifier for the doctor being reviewed.
- **FeedbackRating** (INT): Rating given by the patient (e.g., 1-5).
- **Comments** (TEXT): Additional comments from the patient.

## Relationships
- **Patients** can have multiple **Appointments** (one-to-many relationship).
- **Doctors** can have multiple **Appointments** (one-to-many relationship).
- **Departments** can have multiple **Doctors** (one-to-many relationship).
- **Patients** can provide multiple **Feedback** entries, each linked to a specific **Doctor** (one-to-many relationship).

## Database Schema Diagram
You can view the database schema diagram using the following link:
[HAMS Schema Diagram](https://drawsql.app/teams/tcs-37/diagrams/hams)
