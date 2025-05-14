# Clinic Booking System Schema

## Overview
The Clinic Booking System is designed to manage the scheduling of appointments, patient records, doctor information, and services offered in a healthcare setting. This schema provides a structured way to store and retrieve data related to departments, doctors, patients, appointments, services, medications, and prescriptions.

## Database Tables

### 1. Departments
Stores information about the various departments within the clinic.

```sql
CREATE TABLE departments (
    department_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
department_id: Unique identifier for each department (Primary Key).
name: Name of the department (Unique).
2. Doctors
Stores information about the doctors working in the clinic.

sql
Run
Copy code
CREATE TABLE doctors (
    doctor_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(20) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
doctor_id: Unique identifier for each doctor (Primary Key).
name: Name of the doctor.
email: Email address of the doctor (Unique).
phone: Contact number of the doctor.
department_id: Foreign key referencing the department the doctor belongs to.
3. Patients
Stores information about the patients visiting the clinic.

sql
Run
Copy code
CREATE TABLE patients (
    patient_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    date_of_birth DATE NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(20) NOT NULL
);
patient_id: Unique identifier for each patient (Primary Key).
name: Name of the patient.
date_of_birth: Date of birth of the patient.
email: Email address of the patient (Unique).
phone: Contact number of the patient.
4. Appointments
Stores information about the appointments scheduled by patients with doctors.

sql
Run
Copy code
CREATE TABLE appointments (
    appointment_id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_date DATETIME NOT NULL,
    reason TEXT,
    status ENUM('Scheduled', 'Completed', 'Cancelled') DEFAULT 'Scheduled',
    FOREIGN KEY (patient_id) REFERENCES patients(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES doctors(doctor_id)
);
appointment_id: Unique identifier for each appointment (Primary Key).
patient_id: Foreign key referencing the patient who booked the appointment.
doctor_id: Foreign key referencing the doctor assigned to the appointment.
appointment_date: Date and time of the appointment.
reason: Reason for the appointment.
status: Current status of the appointment (Scheduled, Completed, Cancelled).
5. Services
Stores information about the various services offered by the clinic.

sql
Run
Copy code
CREATE TABLE services (
    service_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    cost DECIMAL(10,2) NOT NULL
);
service_id: Unique identifier for each service (Primary Key).
name: Name of the service (Unique).
cost: Cost of the service.
6. Doctor-Services
Manages the many-to-many relationship between doctors and services.

sql
Run
Copy code
CREATE TABLE doctor_services (
    doctor_id INT NOT NULL,
    service_id INT NOT NULL,
    PRIMARY KEY (doctor_id, service_id),
    FOREIGN KEY (doctor_id) REFERENCES doctors(doctor_id),
    FOREIGN KEY (service_id) REFERENCES services(service_id)
);
doctor_id: Foreign key referencing the doctor providing the service.
service_id: Foreign key referencing the service offered.
7. Medications
Stores information about medications available in the clinic.

sql
Run
Copy code
CREATE TABLE medications (
    medication_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    dosage VARCHAR(50) NOT NULL
);
medication_id: Unique identifier for each medication (Primary Key).
name: Name of the medication.
dosage: Dosage information for the medication.
8. Prescriptions
Stores information about prescriptions given to patients during appointments.

sql
Run
Copy code
CREATE TABLE prescriptions (
    prescription_id INT AUTO_INCREMENT PRIMARY KEY,
    appointment_id INT NOT NULL UNIQUE,
    medication_id INT NOT NULL,
    instructions TEXT,
    FOREIGN KEY (appointment_id) REFERENCES appointments(appointment_id),
    FOREIGN KEY (medication_id) REFERENCES medications(medication_id)
);
prescription_id: Unique identifier for each prescription (Primary Key).
appointment_id: Foreign key referencing the appointment (unique one-to-one).
medication_id: Foreign key referencing the medication prescribed.
instructions: Directions for taking the medication.
