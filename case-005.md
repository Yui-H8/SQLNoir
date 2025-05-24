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
<details open><summary> crime </summary>

  
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

</details>


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

* Access on the day of the incident
```sql
SELECT *
FROM computer_access_logs
WHERE server_location LIKE '%Helsinki%'
AND access_date = 19890421
ORDER BY access_time
;
```
|id|employee_id|server_location|access_date|access_time|
|:----|:----|:----|:----|:----|
|91|99|Helsinki|19890421|09:00|
|31|112|Helsinki|19890421|09:20|
|10|112|Helsinki|19890421|15:20|
|127|33|Helsinki|19890421|16:30|
---
👾 Who are these 3 employees?
<details open><summary> 3 employees </summary>


  
* keycard_access_logs
```sql
SELECT *
FROM employee_records e LEFT JOIN keycard_access_logs k
ON e.id = k.employee_id
WHERE e.id IN ('99','112','33')
;
```
|id|employee_name|department|occupation|home_address|id|employee_id|keycard_code|access_date|access_time|
|:----|:----|:----|:----|:----|:----|:----|:----|:----|:----|
|33|Frank Parker|Engineering|Quality Engineer|147 Willow Ave, North Miami Beach, FL|NULL|NULL|NULL|NULL|NULL|
|99|Elizabeth Gordon|Engineering|Solutions Architect|147 Coastal Pine Rd, Doral, FL|89|99|QX-035|19890421|08:30|
|112|Ruth Henderson|Administration|Technical Documentation Specialist|543 Helium Road, Pinecrest, FL|NULL|NULL|NULL|NULL|NULL|

* 📧 email_log -> null

* 🗄 facility_access_log
```sql
SELECT e.id, employee_name, occupation, f.*
FROM employee_records e LEFT JOIN facility_access_logs f
ON e.id = f.employee_id
WHERE e.id IN ('99','112','33')
AND access_date = 19890421
ORDER BY e.id, f.access_time
;
```
|id|employee_name|occupation|id|employee_id|facility_name|access_date|access_time|
|:----|:----|:----|:----|:----|:----|:----|:----|
|99|Elizabeth Gordon|Solutions Architect|74|99|Facility 18|19890421|08:55|
|99|Elizabeth Gordon|Solutions Architect|37|99|Facility 22|19890421|10:42|
|99|Elizabeth Gordon|Solutions Architect|23|99|Facility 11|19890421|11:56|
|99|Elizabeth Gordon|Solutions Architect|66|99|Facility 27|19890421|13:58|
|99|Elizabeth Gordon|Solutions Architect|55|99|Facility 42|19890421|16:33|
|99|Elizabeth Gordon|Solutions Architect|40|99|Facility 95|19890421|17:03|
|112|Ruth Henderson|Technical Documentation Specialist|57|112|Facility 24|19890421|10:17|
|112|Ruth Henderson|Technical Documentation Specialist|97|112|Facility 21|19890421|10:22|
|112|Ruth Henderson|Technical Documentation Specialist|77|112|Facility 23|19890421|10:47|
|112|Ruth Henderson|Technical Documentation Specialist|12|112|Facility 96|19890421|15:13|
---
☠ suspicious


</details>



☹ But... these three were not the culprits (I submitted).
---
🫥 A server in Helsinki / A keycard marked QX- succeeded by a two-digit odd number.

```sql
SELECT DISTINCT  ABS(CAST(SUBSTR(keycard_code, -3) AS INTEGER)) AS abs_last_three_digits, 
e.id
FROM employee_records e JOIN keycard_access_logs k 
ON e.id = k.employee_id
JOIN computer_access_logs c
ON e.id = c.employee_id
WHERE abs_last_three_digits % 2 = 1
AND keycard_code LIKE '%QX%'
AND c.server_location LIKE '%Helsinki%'
;
```
|abs_last_three_digits|id|
|:----|:----|
|219|23|
|35|99|
|241|56|


👾 Who are these 3 employees?

```sql
SELECT e.id, e.employee_name, keycard_code, k.access_date, k.access_time, server_location	
FROM employee_records e JOIN keycard_access_logs k 
ON e.id = k.employee_id
JOIN computer_access_logs c
ON e.id = c.employee_id
WHERE e.id IN ('23','99','56')
AND server_location = 'Helsinki'
GROUP BY e.id, keycard_code, k.access_date, k.access_time, server_location
;
```

