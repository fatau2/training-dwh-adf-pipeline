# training-dwh-adf-pipeline

Data and Query Tasks
1. Create Table
  a. Employee Table
    CREATE TABLE Employee (
      Id INT IDENTITY(1,1),
      EmployeeId VARCHAR(10) UNIQUE NOT NULL,
      FullName VARCHAR(100) NOT NULL,
      BirthDate DATE NOT NULL,
      Address VARCHAR(500),
      CONSTRAINT PK_Employee
          PRIMARY KEY CLUSTERED (Id)
  );

  b. PositionHistory Table
    CREATE TABLE PositionHistory (
      Id INT IDENTITY(1,1),
      PosId VARCHAR(10) NOT NULL,
      PosTitle VARCHAR(100) NOT NULL,
      EmployeeId VARCHAR(10) NOT NULL,
      StartDate DATE NOT NULL,
      EndDate DATE NOT NULL,
      CONSTRAINT PK_PositionHistory
          PRIMARY KEY CLUSTERED (Id),
      CONSTRAINT FK_PositionHistory_Employee FOREIGN KEY (EmployeeId)
          REFERENCES Employee(EmployeeId)
      ON DELETE CASCADE
      ON UPDATE CASCADE
  );

2. Insert
  a. Employee Data
    INSERT INTO akasiadb.dbo.Employee (EmployeeId, FullName, BirthDate, Address) VALUES 
    ('10105001', 'Ali Anton', '1982-08-19', 'Jakarta Utara'),
    ('10105002', 'Rara Siva', '1982-01-01', 'Mandalika'),
    ('10105003', 'Rini Aini', '1982-02-20', 'Sumbawa Besar'),
    ('10105004', 'Budi', '1982-02-22', 'Mataram Kota')

  b. EmployeeHistory Data
    INSERT INTO akasiadb.dbo.PositionHistory (PosId, PosTitle, EmployeeId, StartDate, EndDate) VALUES 
    ('50000', 'IT Manager', '10105001', '2022-01-01', '2022-02-28'),
    ('50001', 'IT Sr. Manager', '10105001', '2022-03-01', '2022-12-31'),
    ('50002', 'Programmer Analyst', '10105002', '2022-01-01', '2022-02-28'),
    ('50003', 'Sr. Programmer Analyst', '10105002', '2022-03-01', '2022-12-31'),
    ('50004', 'IT Admin', '10105003', '2022-01-01', '2022-02-28'),
    ('50005', 'IT Secretary', '10105003', '2022-03-01', '2022-12-31');

ETL, Data Warehouse, and Analytics Tasks
1. Employee Data in Azure SQL Server
  a. Location: dataset/employee.json
3. Training History Data in Worksheet
  a. Location: dataset/training_history.json

5. ETL Flow compiling Employee Data and Training History Data in a Data Warehouse
  a. Employee Pipeline: pipeline/DimEmployeePipeline.json
  b. Training History Pipeline: pipeline/FactTrainingPipeline.json

7. Historical Training Data Report
   https://lookerstudio.google.com/reporting/ed5dd37e-7f1f-463f-be70-d306de1c557b/page/ZZBaE
   
9. Dashboard displaying:
   a. Total employee completed training each month: https://lookerstudio.google.com/reporting/ed5dd37e-7f1f-463f-be70-d306de1c557b/page/p_ip4wtsb3nd
   b. Total training each month: https://lookerstudio.google.com/reporting/ed5dd37e-7f1f-463f-be70-d306de1c557b/page/p_ip4wtsb3nd
