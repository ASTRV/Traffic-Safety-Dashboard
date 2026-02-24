# Traffic-Control-Dashboard
###Project detailing the cleanup of Traffic Safety data and visualizing the same data in a dashboard.

The NYC traffic accident data between Jan 1st, 2021 to April 9th, 2023 is organized into a table that is sorted out and properly set up inside of Power Query. 
-	Columns with missing/blank information were replaced and filled with “Unspecified” values. 
-	Additional columns were added for the dates to be organized by seasons based on the dates that incidents occurred on.
-	
<img width="1673" height="846" alt="A1" src="https://github.com/user-attachments/assets/3f346abb-33fc-4495-8351-9a9465bca4b5" />

With the organized data, the information is compiled together in order to find specific information to provide better visualization on the dashboard
-	The monthly vs yearly collision trend is set from 2021-2023 to find largest number of collisions that occurred within a specific month in a year:
o	="Year/Month Collision Peaks:"&CHAR(10)&"🟥2021: "&INDEX(P6:P17,MATCH(MAX(Q6:Q17),Q6:Q17,0))&" ("&TEXT(MAX(Q6:Q17),"#,##")&" collision)"&CHAR(10)&"🟧2022: "&INDEX(P6:P17,MATCH(MAX(R6:R17),R6:R17,0))&" ("&TEXT(MAX(R6:R17),"#,##")&" collision)" &CHAR(10) &"⬜2023: "&INDEX(P8:P19,MATCH(MAX(S6:S8),S6:S8,0))&" ("& TEXT(MAX(S6:S8),"#,##")&" collision)"
The same function is repeated but to locate the Total Collisions by the year versus YoY:
o	="YoY Change Summary:"&CHAR(10)&"⬛ 2022 "&TEXT(AE13,"0.0%")&IF(AC13>0," Increase","Drop")&" vs 2021"&CHAR(10)&"⬛ 2022 "&TEXT(AE13,"0.0%")&IF(AC13>0," Increase","Drop")&" vs 2021"& CHAR(10)&" (2023 drop likely dure to incomplete data)"
The top 10 contributing factors by total collisions is calculated in a similar fashion but visualized by data bars:
o	="Collision Cause Summary:"&CHAR(10)&CHAR(10)&"⬛ Most Common Factor: "&INDEX(AP17:AP26,MATCH(MAX(AQ17:AQ26),AQ17:AQ26,0))& " ("& TEXT(MAX(AQ17:AQ26),"#,##")&" collisions)"&CHAR(10)&"⬛ Most Common Dangerous Factor: "&INDEX(AP17:AP26,MATCH(MAX(AS17:AS26),AS17:AS26,0))& " ("& TEXT(MAX(AS17:AS26),"0.00%")&" collisions)"
To better understand the next steps to take based on the contributing factors, a recommendation button is added. This is set up through the VBA window where a macro module is created to allow more information to show for recommended precautions:
