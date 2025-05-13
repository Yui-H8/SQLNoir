### Case #003: The Miami Marina Murder
A body was found floating near the docks of Coral Bay Marina in the early hours of August 14, 1986.  
Your job detective is to find the murderer and bring them to justice.   
This case might require the use of JOINs, wildcard searches, and logical deduction. Get to work, detective.  

#### Objectives
1. Find the murderer. ( Start by finding the crime scene and go from there )
---
#### Precheck
* Find the murder
```sql
SELECT *
FROM crime_scene
WHERE  date = '19860814'
AND location = 'Coral Bay Marina'
;
```

<details open><summary> Murder </summary>

  
<table>
  <caption> Murder Detail </caption>
  <thead>
    <tr>
      <th>id</th> <th>43</th>
    </tr>
  </thead>
  <tr>
    <td> location </td> <td>Coral Bay Marina</td>
  </tr>
  <tr>
    <td> description </td> <td>The body of an unidentified man was found near the docks. </td>
  </tr>
    <tr>
    <td> suspection </td> <td>Two people were seen nearby: one who lives on 300ish "Ocean Drive" </br> and another whose first name ends with "ul" and his last name ends with "ez".</td>
  </tr>
</table>
</details>

---
* Persin who lives "Ocean Drive"
```sql
SELECT *
FROM person p JOIN confessions c
ON p.id = c.person_id
JOIN interviews i ON p.id = i.person_id
JOIN surveillance_records s ON p.id = s.person_id
JOIN hotel_checkins h ON p.id = h.person_id
WHERE p.address LIKE '%Ocean Drive%'
;
```

<details open><summary>  one who lives on 300ish "Ocean Drive"   </summary>
    
| info | - | - |
|:-----------:|:------------|:------------|
| id       | 101        | -         |
| name    | Carlos Mendez      | Fisherman       |
| alias      | Los Ojos       | -         |
| address         | 369 Ocean Drive          | -           |
| confession       | This is just a misunderstanding.       | -       |
| transcript    | I saw someone check into a hotel on August 13.     | -      |
| hotel_checkin | Coral View Resort | 19860812 |
| suspicious_activity | Asked for room service menu | - |
</details>

---
* Another whose first name ends with "ul" and his last name ends with "ez"
```sql
SELECT *
FROM person p JOIN confessions c
ON p.id = c.person_id
JOIN interviews i ON p.id = i.person_id
JOIN surveillance_records s ON p.id = s.person_id
JOIN hotel_checkins h ON p.id = h.person_id
WHERE p.name LIKE ('%ul_%')
AND p.name LIKE ('%ez')
;
```
<details open><summary>  first name ends with "ul" and his last name ends with "ez"   </summary>
    
| info | - | - |
|:-----------:|:------------|:------------|
| id       | 102        | -         |
| name    | Raul Gutierrez      | 	Nightclub Owner     |
| alias      | The Cobra       | -         |
| address         | 45 Sunset Ave          | -           |
| confession       | Alright! I've been running a blackmail operation.       | -       |
| transcript    | 	I heard someone checked into a hotel with "Sunset" in the name.     | -      |
| hotel_checkin | Marina Paradise Inn | 19860815 |
| suspicious_activity | NULL | - |
</details>

---
* How many people meet the requirements
1. checked into a hotel with "Sunset" in the name
2. Hotel check-in date is '19860813'
```sql
SELECT COUNT(DISTINCT p.id)
FROM person p JOIN confessions c
ON p.id = c.person_id
JOIN interviews i ON p.id = i.person_id
JOIN surveillance_records s ON p.id = s.person_id
JOIN hotel_checkins h ON p.id = h.person_id
WHERE h.hotel_name LIKE ('%Sunset%')
AND check_in_date = '19860813'
;
```
##### 49 person
#####  (DISTINCT : no duplicate)
---
* use confessions
```sql
SELECT p.id, name, alias, occupation, address, confession, suspicious_activity, hotel_name
FROM person p JOIN confessions c
ON p.id = c.person_id
JOIN interviews i ON p.id = i.person_id
JOIN surveillance_records s ON p.id = s.person_id
JOIN hotel_checkins h ON p.id = h.person_id
WHERE h.hotel_name LIKE ('%Sunset%')
AND check_in_date = '19860813'
AND confession LIKE ('%I did it.%')
;
```
<details open><summary>  suspicious character   </summary>
    
| info | - | - |
|:-----------:|:------------|:------------|
| id       | 8        | -         |
| name    | Thomas Brown      | Dock Worker       |
| alias      | The Fox       | -         |
| address         | 234 Port Street          | -           |
| confession       | Alright! I did it. I was paid to make sure he never left the marina alive.       | -       |
| hotel_checkin | Sunset Palm Resort | 19860813 |
| suspicious_activity | Left suddenly at 3 AM | - |
</details>

---
Answer : 	Thomas Brown


Once I narrowed it down to 49 people I looked over all the information. In advance I could have granted more conditions.
