### Case #003: The Miami Marina Murder
A body was found floating near the docks of Coral Bay Marina in the early hours of August 14, 1986.  
Your job detective is to find the murderer and bring them to justice.   
This case might require the use of JOINs, wildcard searches, and logical deduction. Get to work, detective.  

#### Objectives
1. Find the murderer. ( Start by finding the crime scene and go from there )
---
Precheck
* Find the murder
```sql
SELECT *
FROM crime_scene
WHERE  date = '19860814'
AND location = 'Coral Bay Marina'
;
```

<details open><summary> Murder　</summary>

<table>
  <caption>HTMLの要素</caption>
  <thead>
    <tr>
      <th>id</th> <th>43</th>
    </tr>
  </thead>
  <tr>
    <td> location </td> <td>Coral Bay Marina</td>
  </tr>
  <tr>
    <td> description </td> <td>The body of an unidentified man was found near the docks. Two people were seen nearby</td>
  </tr>
</table>

id: 43  
date: 	location	description
43	19860814	Coral Bay Marina	The body of an unidentified man was found near the docks. Two people were seen nearby: one who lives on 300ish "Ocean Drive" and another whose first name ends with "ul" and his last name ends with "ez".
Tab 2
Table View
Graph View

  
