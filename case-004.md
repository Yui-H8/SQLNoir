### Case #004: The Midnight Masquerade Murder
On October 31, 1987, at a Coconut Grove mansion masked ball, Leonard Pierce was found dead in the garden. Can you piece together all the clues to expose the true murderer?

#### Objectives
1. Reveal the true murderer of this complex case.
---
#### Table
* crime_scene
* person
* witness_statements
* hotel_checkins
* surveillance_records
* phone_records
* final_interviews
* vehicle_registry
* catering_orders
---
Precheck
```sql
SELECT *
FROM crime_scene
WHERE date = '19871031'
AND location LIKE '%Coconut Grove%'
;
```

<details open><summary> crime </summary>

  
<table>
  <caption> crime Detail </caption>
  <thead>
    <tr>
      <th>id</th> <th>75</th>
    </tr>
  </thead>
    <tr>
    <td> Date </td> <td>19871031</td>
  </tr>
  <tr>
    <td> location </td> <td>Miami Mansion, Coconut Grove</td>
  </tr>
  <tr>
    <td> description </td> <td>During a masked ball, a body was found in the garden. <br/>Witnesses mentioned a hotel booking and suspicious phone activity. </td>
  </tr>
  
</table>


</details>


* Witness information
```sql
SELECT c.id, c.date, 
w.witness_id, clue 
FROM crime_scene c JOIN witness_statements w
ON c.id = w.crime_scene_id
WHERE c.id = 75
;
```

|id|date|witness_id|clue|
|:----|:----|:----|:----|
|75|19871031|37|I overheard a booking at The Grand Regency.|
|75|19871031|42|I noticed someone at the front desk discussing Room 707 for a reservation made yesterday.|


* Who are the two people mentioned above?
```SQL
SELECT p.*, w.clue 
FROM person p JOIN witness_statements w
ON p.id = w.witness_id
WHERE w.witness_id IN (34, 42)
;
```
|id|name|occupation|address|clue|
|:----|:----|:----|:----|:----|
|34|Susan Scott|Psychologist|861 Forest Drive|While walking home, I saw someone throwing what looked like documents into a dumpster behind the building.|
|34|Susan Scott|Psychologist|861 Forest Drive|While delivering packages, I noticed the side door had fresh scratch marks around the lock.|
|34|Susan Scott|Psychologist|861 Forest Drive|I noticed the security lights were deliberately covered with some kind of dark material.|
|34|Susan Scott|Psychologist|861 Forest Drive|From my apartment, I saw flashlights moving through the building long after closing.|
|34|Susan Scott|Psychologist|861 Forest Drive|I saw unusual activity near the ventilation system access points.|
|34|Susan Scott|Psychologist|861 Forest Drive|During my rounds, I found evidence of someone monitoring staff movements.|
|34|Susan Scott|Psychologist|861 Forest Drive|I heard coded radio communications coming from multiple directions.|
|34|Susan Scott|Psychologist|861 Forest Drive|While working, I found evidence of systematic security breaches.|
|34|Susan Scott|Psychologist|861 Forest Drive|I noticed unusual activity in typically restricted areas of the building.|
|42|Sharon Phillips|Marketing Manager|849 Ashwood Court|I noticed someone at the front desk discussing Room 707 for a reservation made yesterday.|





---
