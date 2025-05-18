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

---

