# Clinic Booking System Schema

## Overview
This repository contains the database schema for a Clinic Booking System. The schema is designed to manage departments, doctors, patients, appointments, services, medications, and prescriptions in a healthcare environment.

## Tables and Relationships

### Departments
- Stores clinic departments.
- `department_id`: Primary key.
- `name`: Unique department name.

### Doctors
- Stores information about doctors.
- `doctor_id`: Primary key.
- `name`, `email` (unique), `phone`.
- Foreign key: `department_id` references `departments`.

### Patients
- Stores patient records.
- `patient_id`: Primary key.
- `name`, `date_of_birth`, `email` (unique), `phone`.

### Appointments
- Tracks patient appointments with doctors.
- `appointment_id`: Primary key.
- Foreign keys: `patient_id` references `patients`, `doctor_id` references `doctors`.
- Includes `appointment_date`, `reason`, and `status` (Scheduled, Completed, Cancelled).

### Services
- Lists services offered by the clinic.
- `service_id`: Primary key.
- `name` (unique), `cost`.

### Doctor-Services
- Many-to-many relation between doctors and services.
- Composite primary key: (`doctor_id`, `service_id`).
- Foreign keys to `doctors` and `services`.

### Medications
- Stores medication details.
- `medication_id`: Primary key.
- `name`, `dosage`.

### Prescriptions
- Links medications with appointments.
- `prescription_id`: Primary key.
- Foreign keys: `appointment_id` (unique), `medication_id`.
- Includes `instructions`.

## Usage
Use the SQL `CREATE TABLE` statements in this repository to set up the database schema needed for the Clinic Booking System.

## License
This project is open source and free to use.
