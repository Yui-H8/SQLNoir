### Case #005: The Silicon Sabotage
QuantumTech, Miami’s leading technology corporation, was about to unveil its groundbreaking microprocessor called “QuantaX.”   
Just hours before the reveal, the prototype was destroyed, and all research data was erased. Detectives suspect corporate espionage.

#### Objectives
1. Find who sabotaged the microprocessor.
---
#### Table
* incident_reports
* witness_statements
* keycard_access_logs
* computer_access_logs
* email_logs
* facility_access_logs
* employee_records
---
* Precheck
```sql
SELECT *
FROM incident_reports
WHERE location LIKE '%QuantumTech%'
;
```
|id|date|location|description|
|:----|:----|:----|:----|
|74|19890421|QuantumTech HQ|Prototype destroyed; data erased from servers.|
---
* Witness information
```sql
SELECT *
FROM witness_statements
WHERE incident_id = 74
;
```
|id|incident_id|employee_id|statement|
|:----|:----|:----|:----|
|40|74|145|I heard someone mention a server in Helsinki.|
|59|74|134|I saw someone holding a keycard marked QX- succeeded by a two-digit odd number.|
---
👥 Who are these 2 person who have employee number 145 & 134 ?
```SQL
SELECT *
FROM employee_records
WHERE id IN ( 145, 134 )
```
|id|employee_name|department|occupation|home_address|
|:----|:----|:----|:----|:----|
|134|Tina Ruiz|Human Resources|Training Coordinator|864 Isotope Isle, North Miami Beach, FL|
|145|Carl Jenkins|Hardware|Electronics Engineer|159 Qubit Quarter, Miami Shores, FL|
---
🖥 Access log to the server in Helsinki
```sql
SELECT *
FROM computer_access_logs
WHERE server_location LIKE '%Helsinki%'
;
```
|id|employee_id|server_location|access_date|access_time|
|:----|:----|:----|:----|:----|
|10|112|Helsinki|19890421|15:20|
|12|23|Helsinki|19890419|16:45|
|14|56|Helsinki|19890420|15:30|
|20|92|Helsinki|19890420|16:30|
|31|112|Helsinki|19890421|09:20|
|51|1|Helsinki|19890419|08:45|
|62|92|Helsinki|19890420|15:30|
|80|142|Helsinki|19890420|16:30|
|91|99|Helsinki|19890421|09:00|
|108|56|Helsinki|19890419|09:15|
|111|111|Helsinki|19890419|16:15|
|127|33|Helsinki|19890421|16:30|
|129|178|Helsinki|19890419|15:15|
|144|56|Helsinki|19890419|08:15|
