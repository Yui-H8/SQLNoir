### Case #001: The Vanishing Briefcase
Set in the gritty 1980s, a valuable briefcase has disappeared from the Blue Note Lounge.   
A witness reported that a man in a trench coat was seen fleeing the scene.   
Investigate the crime scene, review the list of suspects, and examine interview transcripts to reveal the culprit.
  
#### Objectives
1. Retrieve the correct crime scene details to gather the key clue.
2. Identify the suspect whose profile matches the witness description.
3. Verify the suspect using their interview transcript.
---
```SQL
SELECT *
FROM suspects s
JOIN interviews i ON s.id = i.suspect_id 
WHERE attire = "trench coat"
AND scar = "left cheek"
AND transcript IS NOT NULL

/*
SELECT *
FROM crime_scene
WHERE date BETWEEN 19800101 AND 19891231
AND location LIKE "%Lounge"
*/
```
