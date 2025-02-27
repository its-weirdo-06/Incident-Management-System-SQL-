# Incident-Management-System-SQL-
Develop a comprehensive Incident Management System to track, manage, and resolve incidents. The system will include functionalities for logging incidents, assigning them to support engineers, tracking their status, and generating reports.
### **Key Features:**

- Incident logging and tracking
- Assignment of incidents to support engineers
- Status updates and resolution tracking
- Reporting and analytics on incident trends

### **Key Tables:**

- `incidents`
- `support_engineers`
- `incident_status`
- `incident_logs`

### Script :

-- Create table for support engineers

CREATE TABLE support_engineers (
engineer_id INT IDENTITY(1,1) PRIMARY KEY,
engineer_name VARCHAR(50) NOT NULL,
email VARCHAR(50) NOT NULL
);

-- Create table for incident status

CREATE TABLE incident_status (
status_id INT IDENTITY(1,1) PRIMARY KEY,
status_name VARCHAR(20) NOT NULL
);

-- Create table for incidents

CREATE TABLE incidents (
incident_id INT IDENTITY(1,1) PRIMARY KEY,
incident_description TEXT NOT NULL,
severity_level VARCHAR(10) NOT NULL,
status VARCHAR(20) NOT NULL,
reported_by VARCHAR(50) NOT NULL,
reported_at DATETIME DEFAULT CURRENT_TIMESTAMP,
assigned_to INT,
resolution_time INT, -- Resolution time in minutes or seconds (depending on your requirement)
FOREIGN KEY (assigned_to) REFERENCES support_engineers(engineer_id)
);

-- Create table for incident logs

CREATE TABLE incident_logs (
log_id INT IDENTITY(1,1) PRIMARY KEY,
incident_id INT NOT NULL,
log_description TEXT NOT NULL,
created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
FOREIGN KEY (incident_id) REFERENCES incidents(incident_id)
);

-- Sample query to generate a report of incidents by severity level

SELECT severity_level, COUNT(*) AS incident_count
FROM incidents
GROUP BY severity_level;
