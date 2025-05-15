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
