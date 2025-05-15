### Case #006: The Vanishing Diamond
At Miami’s prestigious Fontainebleau Hotel charity gala, the famous “Heart of Atlantis” diamond necklace suddenly disappeared from its display.
  
#### Objectives
1. Find who stole the diamond.
---
#### Table
* crime_scene
* guest
* witness_statements
* attire_registry
* marina_rentals
* final_interviews
---
Precheck
```SQL
SELECT *
FROM crime_scene
WHERE location LIKE ('%Fontainebleau%')
;
```

<details open><summary> crime </summary>

  
<table>
  <caption> crime Detail </caption>
  <thead>
    <tr>
      <th>id</th> <th>48</th>
    </tr>
  </thead>
    <tr>
    <td> Date </td> <td>19870520</td>
  </tr>
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
id	date	location	description
48	19870520	Fontainebleau Hotel	The Heart of Atlantis necklace disappeared. Many guests were questioned but only two of them gave valuable clues. One of them is a really famous actor. The other one is a woman who works as a consultant for a big company and her first name ends with "an".
