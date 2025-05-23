# Medical Laboratory System Database

## Overview

This project implements a relational database for managing operations in a medical laboratory. It keeps track of patients, laboratorians, medical tests, test components, and results.

---
 ├─ [DB.docx](https://github.com/user-attachments/files/20414105/DB.docx)
/report.docx        ← Your written report

├─[Medical Laboratory Database System.pptx](https://github.com/user-attachments/files/20414314/Medical.Laboratory.Database.System.pptx)
 /presentation.pptx  ← Your slides

├─https://youtu.be/Ev2BAWvf89g /video_link.txt     ← Public YouTube/MS Stream URL

├─ /sql/
     
CREATE DATABASE IF NOT EXISTS Laboratorian_db; 
USE Laboratorian_db; 

 

-- Drop tables if they exist to reset data 

DROP TABLE IF EXISTS TestResult, TestComponent, MedicalTest, Component, Patient, Laboratorian; 

 

-- Tables 

CREATE TABLE Laboratorian ( 

  LaboratorianID INT PRIMARY KEY, 

  Name VARCHAR(100), 

  PhoneNumber VARCHAR(20), 

  Address VARCHAR(200) 

); 

 

CREATE TABLE Patient ( 

  PatientID INT PRIMARY KEY, 

  Name VARCHAR(100), 

  PhoneNumber VARCHAR(20), 

  Address VARCHAR(200), 

  BirthDate DATE, 

  Job VARCHAR(100) 

); 

 

CREATE TABLE Component ( 

  ComponentID INT PRIMARY KEY, 

  Name VARCHAR(100), 

  AvailableQuantity INT, 

  MinimumQuantity INT 

); 

 

CREATE TABLE MedicalTest ( 

  TestID INT PRIMARY KEY, 

  Name VARCHAR(100), 

  Price DECIMAL(10,2) 

); 

 

CREATE TABLE TestComponent ( 

  TestID INT, 

  ComponentID INT, 

  PRIMARY KEY (TestID, ComponentID), 

  FOREIGN KEY (TestID) REFERENCES MedicalTest(TestID), 

  FOREIGN KEY (ComponentID) REFERENCES Component(ComponentID) 

); 

 

CREATE TABLE TestResult ( 

  ResultID INT PRIMARY KEY, 

  TestID INT, 

  TestDate DATE, 

  PatientID INT, 

  LaboratorianID INT, 

  Result TEXT, 

  FOREIGN KEY (TestID) REFERENCES MedicalTest(TestID), 

  FOREIGN KEY (PatientID) REFERENCES Patient(PatientID), 

  FOREIGN KEY (LaboratorianID) REFERENCES Laboratorian(LaboratorianID) 

); 

 

-- Laboratorians 

INSERT INTO Laboratorian VALUES 

(1, 'Ahmed Ali', '01011111111', 'Cairo'), 

(2, 'Sara Mohamed', '01022222222', 'Giza'), 

(3, 'Omar Hassan', '01033333333', 'Alexandria'), 

(4, 'Nour El-Sayed', '01044444444', 'Aswan'), 

(5, 'Laila Said', '01055555555', 'Cairo'), 

(6, 'Yousef Hany', '01066666666', 'Giza'), 

(7, 'Hassan Tarek', '01077777777', 'Alexandria'), 

(8, 'Rana Fathy', '01088888888', 'Aswan'), 

(9, 'Maged Sobhy', '01099999999', 'Cairo'), 

(10, 'Nadine Helmy', '01000000000', 'Giza'); 

 

-- Patients 

INSERT INTO Patient VALUES 

(12527, 'Mohamed Salah', '01155555555', 'Cairo', '1990-05-15', 'Engineer'), 

(12528, 'Fatma Ali', '01166666666', 'Giza', '1985-11-20', 'Teacher'), 

(12529, 'Ahmed Nasser', '01177777777', 'Alexandria', '1995-02-10', 'Doctor'), 

(12530, 'Mona Hassan', '01188888888', 'Aswan', '2000-07-25', 'Student'), 

(12531, 'Youssef Ahmed', '01199999999', 'Cairo', '1988-12-12', 'Lawyer'), 

(12532, 'Layla Mostafa', '01200000000', 'Giza', '1992-09-09', 'Pharmacist'), 

(12533, 'Khaled Ibrahim', '01211111111', 'Alexandria', '1983-06-18', 'Nurse'), 

(12534, 'Dina Samir', '01222222222', 'Aswan', '1991-03-05', 'Engineer'), 

(12535, 'Sami Fouad', '01233333333', 'Cairo', '1987-08-28', 'Teacher'), 

(12536, 'Sara Adel', '01244444444', 'Giza', '1993-04-15', 'Doctor'); 

 

-- Components 

INSERT INTO Component VALUES 

(1, 'Glucose', 50, 30), 

(2, 'Hemoglobin', 20, 25), 

(3, 'Sodium', 60, 50), 

(4, 'Potassium', 10, 15), 

(5, 'Calcium', 35, 20), 

(6, 'Cholesterol', 40, 30), 

(7, 'Albumin', 25, 20), 

(8, 'Creatinine', 15, 10), 

(9, 'Urea', 30, 25), 

(10, 'Bilirubin', 18, 15); 

 

-- Medical Tests 

INSERT INTO MedicalTest VALUES 

(101, 'CBC', 150.00), 

(102, 'Blood Sugar', 100.00), 

(103, 'Lipid Profile', 200.00), 

(104, 'Liver Function', 180.00), 

(105, 'Kidney Function', 170.00), 

(106, 'Thyroid Panel', 160.00), 

(107, 'Vitamin D', 140.00), 

(108, 'Iron Test', 110.00), 

(109, 'CRP Test', 130.00), 

(110, 'Electrolyte Panel', 190.00); 

 

-- Test Components 

INSERT INTO TestComponent VALUES 

(101, 2), (101, 3), (101, 4), 

(102, 1), 

(103, 6), 

(104, 10), (104, 7), 

(105, 8), (105, 9), 

(106, 5), (106, 3), 

(107, 5), 

(108, 2), 

(109, 6), 

(110, 3), (110, 4); 

 

-- Test Results 

INSERT INTO TestResult VALUES 

(1, 101, '2024-05-10', 12527, 1, 'Normal'), 

(2, 102, '2024-06-15', 12528, 2, 'High'), 

(3, 103, '2023-11-20', 12529, 3, 'Borderline'), 

(4, 104, '2024-01-05', 12530, 4, 'Normal'), 

(5, 105, '2023-12-12', 12531, 5, 'High'), 

(6, 106, '2024-02-14', 12532, 6, 'Low'), 

(7, 107, '2023-08-18', 12533, 7, 'Deficient'), 

(8, 108, '2022-07-25', 12534, 8, 'Normal'), 

(9, 109, '2024-03-03', 12535, 9, 'Elevated'), 

(10, 110, '2023-04-22', 12536, 10, 'Normal'); 

 

-- Trigger to check component stock 

DELIMITER // 

 

CREATE TRIGGER CheckComponentStock 

AFTER INSERT ON TestComponent 

FOR EACH ROW 

BEGIN 

  UPDATE Component 

  SET AvailableQuantity = AvailableQuantity - 1 

  WHERE ComponentID = NEW.ComponentID; 

 

  IF (SELECT AvailableQuantity FROM Component WHERE ComponentID = NEW.ComponentID) < 

     (SELECT MinimumQuantity FROM Component WHERE ComponentID = NEW.ComponentID) THEN 

    SIGNAL SQLSTATE '45000' 

    SET MESSAGE_TEXT = 'Warning: Component stock below minimum!'; 

  END IF; 

END; 

// 

 

DELIMITER ; 

 

-- Example to trigger stock warning 

-- INSERT INTO TestComponent (TestID, ComponentID) VALUES (101, 4); 

 
## Schema Description

### Tables

- **Laboratorian**: Information about the laboratory staff.
- **Patient**: Contains personal and contact details of patients.
- **Component**: Materials used for medical tests.
- **MedicalTest**: Details of the various tests.
- **TestComponent**: Junction table linking tests to required components.
- **TestResult**: Records results for tests conducted on patients.

---

## Example Use Cases

- Track all patients who underwent a particular test.
- Monitor inventory for low-stock test components.
- Calculate the amount a specific patient has paid for tests over a time period.

---

## Sample Queries

1. Patients who did a CBC test last year
2. Components below minimum stock
3. Total money paid by a patient over the past 3 years

---

## Installation

1. Import the schema into MySQL.
2. Insert data as needed.
3. Use SQL client  for querying.

---

## Author

Developed by: [Marwa Ahmed,Sama Ossama,Haya mohammed & sama islam]

