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
    <td> location </td> <td>Fontainebleau Hotel</td>
  </tr>
  <tr>
    <td> description </td> <td>The Heart of Atlantis necklace disappeared. </td>
  </tr>
    <tr>
    <td> suspection </td> <td>Many guests were questioned but only two of them gave valuable clues. </br> One of them is a really famous actor. The other one is a woman who works as a consultant for a big company and her first name ends with "an".</td>
  </tr>
</table>
</details>

---
* check 'actor' : 5 Person
```sql
SELECT *
FROM guest g JOIN final_interviews f
ON g.id = f.guest_id
WHERE occupation LIKE '%actor%'
;
```
|id|name|occupation|invitation_code|confession|
|:----|:----|:----|:----|:----|
|43|Ruby Baker|Actor|VIP-R|Youve got the wrong person. Im not someone who would kill.|
|129|Clint Eastwood|Actor|VIP-G|I was taking care of my sick mother. I would never commit murder.|
|164|River Bowers|Actor|VIP-B|My gym trainer can verify my presence. Im innocent of this charge.|
|189|Sage Dillon|Actor|VIP-G|I was at an art gallery opening. I appreciate life too much to take it.|
|192|Phoenix Pitts|Actor|VIP-G|Check my computer login records. I couldnt have done this.|
---
* check first name ends with "an"
```sql
SELECT g.id, name, occupation, invitation_code, confession
FROM guest g JOIN final_interviews f
ON g.id = f.guest_id
WHERE name LIKE '%an %'
;
```
