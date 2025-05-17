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
* check first name ends with "an" : 5 Person
```sql
SELECT g.id, name, occupation, invitation_code, confession
FROM guest g JOIN final_interviews f
ON g.id = f.guest_id
WHERE name LIKE '%an %'
;
```
|id|name|occupation|invitation_code|confession|
|:----|:----|:----|:----|:----|
|14|Ethan Taylor|Financial Analyst|VIP-B|This is a mistake. Im not the type of person who would kill.|
|22|Sebastian Lewis|Music Producer|VIP-R|Im a vegetarian for crying out loud. I wouldnt kill anyone!|
|40|Julian Wood|Sports Team Owner|VIP-R|Im completely innocent. I would never kill another person.|
|60|Roman Fisher|Nightclub Owner|VIP-G|Youre barking up the wrong tree. I wouldnt kill anybody.|
|116|Vivian Nair|Consultant|VIP-R|Check my work computer logs. I would never commit such a horrible act.|
---
🧐 Confession of 2 persons include 'computer'. First of all, it can be clue.  
192:	Phoenix Pitts  
116:	Vivian Nair (She is a Consultant)  
* check these 2 person
```sql
SELECT a.guest_id, note AS attire, 
confession AS finalanswer, w.clue
FROM attire_registry a JOIN final_interviews f
ON a.guest_id = f.guest_id
JOIN witness_statements w
ON a.guest_id = w.guest_id
WHERE a.guest_id IN (192, 116)
;
```
|guest_id|attire|finalanswer|clue|
|:----|:----|:----|:----|
|116|blue velvet dress, pearl choker|Check my work computer logs. I would never commit such a horrible act.|I saw someone holding an invitation ending with "-R". He was wearing a navy suit and a white tie.|
---
👤 Who is a guy who worn a navy suit and a white tie?
```SQL
SELECT g.id, name, occupation, note, confession, clue
FROM guest g JOIN attire_registry a
ON g.id = a.guest_id
JOIN final_interviews f
ON g.id = f.guest_id
JOIN witness_statements w
ON g.id = w.guest_id
WHERE note LIKE '%navy%' AND note LIKE '%White%'
;
```
|id|name|occupation|note|confession|clue|
|:----|:----|:----|:----|:----|:----|
|167|Luna Dalton|Fashion Designer|navy suit, white tie|I was at a photography workshop. I capture life, not take it.|During my evening jog, I noticed a black van parked outside with its lights off for over two hours.|

* ❓ But his name is not including '-R'.
---
* Other perspective
* 👤 Who is a person who has an invitation ending with "-R"?
```sql
SELECT g.id, name, occupation, invitation_code, note
FROM guest g JOIN attire_registry a
ON g.id = a.guest_id
WHERE a.note LIKE '%navy suit%'
AND a.note LIKE '%white tie%'
AND g.invitation_code LIKE '%R'
;
```
|id|name|occupation|invitation_code|note|
|:----|:----|:----|:----|:----|
|105|Mike Manning|Wealth Reallocation Expert|VIP-R|navy suit, white tie|
    
* 👤 Who is 'Mike Manning'?
```sql
SELECT g.id, name, occupation, invitation_code, note, confession
FROM guest g JOIN attire_registry a
ON g.id = a.guest_id
JOIN final_interviews f
ON g.id = f.guest_id
WHERE g.id = 105
;
```

