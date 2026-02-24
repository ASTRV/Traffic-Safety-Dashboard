# Traffic-Control-Dashboard
### Project detailing the cleanup of Traffic Safety data and visualizing the same data in two dashboards.

The NYC traffic accident data between Jan 1st, 2021 to April 9th, 2023 is organized into a table that is sorted out and properly set up inside of Power Query.  

![WholeDash](https://github.com/user-attachments/assets/01fae30e-10a1-48d6-ad71-4945c576f83e)

-	Columns with missing/blank information were replaced and filled with “Unspecified” values.
<img width="1673" height="846" alt="A1" src="https://github.com/user-attachments/assets/3f346abb-33fc-4495-8351-9a9465bca4b5" />
<br></br>
Additional columns were added for the times to be organized by time intervals.
<img width="689" height="383" alt="A1_a" src="https://github.com/user-attachments/assets/b491a8b3-a64b-484e-a3e0-55d140db433b" />
<img width="194" height="385" alt="A1_a1" src="https://github.com/user-attachments/assets/e91916b9-38df-4ba7-b1bf-7c5f7861dda1" />  <br></br>

Steps above were repeated in order to organize dates by seasons.  
<img width="520" height="325" alt="A1_b" src="https://github.com/user-attachments/assets/13a5d7b5-a610-4408-bf84-279c47140b1e" />
<img width="194" height="326" alt="A2_b1" src="https://github.com/user-attachments/assets/5675462d-c1a4-4ad0-8556-ae0e1705ca32" />


With the organized data, the information is compiled together in order to find specific information to provide better visualization on the dashboard
-	The monthly vs yearly collision trend is set from 2021-2023 to find largest number of collisions that occurred within a specific month in a year:
<img width="413" height="224" alt="B1" src="https://github.com/user-attachments/assets/0f36e917-a4b8-4573-ab2e-3f307c089ae0" />

```
="Year/Month Collision Peaks:"&CHAR(10)&"🟥2021: "&INDEX(P6:P17,MATCH(MAX(Q6:Q17),Q6:Q17,0))&" ("&TEXT(MAX(Q6:Q17),"#,##")&" collision)"&CHAR(10)&"🟧2022: "&INDEX(P6:P17,MATCH(MAX(R6:R17),R6:R17,0))&" ("&TEXT(MAX(R6:R17),"#,##")&" collision)" &CHAR(10) &"⬜2023: "&INDEX(P8:P19,MATCH(MAX(S6:S8),S6:S8,0))&" ("& TEXT(MAX(S6:S8),"#,##")&" collision)"
```
<br></br>
The same function is repeated but to locate the Total Collisions by the year versus YoY:  
  
```
="YoY Change Summary:"&CHAR(10)&"⬛ 2022 "&TEXT(AE13,"0.0%")&IF(AC13>0," Increase","Drop")&" vs 2021"&CHAR(10)&"⬛ 2022 "&TEXT(AE13,"0.0%")&IF(AC13>0," Increase","Drop")&" vs 2021"& CHAR(10)&" (2023 drop likely dure to incomplete data)"
```
<img width="307" height="229" alt="B2" src="https://github.com/user-attachments/assets/2f9e718a-8c4c-4ccd-adfd-4bbf42b1f3c6" />
<br></br>
The top 10 contributing factors by total collisions is calculated in a similar fashion but visualized by data bars:  

```
="Collision Cause Summary:"&CHAR(10)&CHAR(10)&"⬛ Most Common Factor: "&INDEX(AP17:AP26,MATCH(MAX(AQ17:AQ26),AQ17:AQ26,0))& " ("& TEXT(MAX(AQ17:AQ26),"#,##")&" collisions)"&CHAR(10)&"⬛ Most Common Dangerous Factor: "&INDEX(AP17:AP26,MATCH(MAX(AS17:AS26),AS17:AS26,0))& " ("& TEXT(MAX(AS17:AS26),"0.00%")&" collisions)"
```

<img width="464" height="377" alt="B3" src="https://github.com/user-attachments/assets/944ed30d-81b0-4a55-bc1c-eb3df9ed74e9" />

<br></br>
To better understand the next steps to take to avoid collisions based on the contributing factors, a recommendation button is added. This is set up through the VBA window where a macro module is created to allow more information to show for recommended precautions:
<img width="338" height="160" alt="B4" src="https://github.com/user-attachments/assets/ea40a427-b2cf-40c8-89e4-4b06c92dece7" />

![B4_a](https://github.com/user-attachments/assets/665da750-12f3-46b9-9e56-675481e181e8)
- The same macros are duplicated then used for the Monthly vs Yearly Collision Trend.

Another macro was created for the Weekly vs Time Interval Collisions chart where the option to toggle the values shown on the hitmap was created. 
- A hitmap was created and a conditional graded color scale was added to sort out the information between the Time Interval and the Days of the Week.
<img width="440" height="192" alt="B5" src="https://github.com/user-attachments/assets/56624312-860c-482e-9991-67c7efe31922" />

![ToggleNumber](https://github.com/user-attachments/assets/fa29c5d5-f061-49c5-9fec-ac4adb09458c)

The rest of the information is visualized in bar charts with data retrieved from Roles (Motorists, Cyclists, and Pedestrians) and Weekly vs Time Interval Collisions (By Seasons).
- The information displayed determines the amount of accidents that caused either injuries or deaths per the role. The summary then states what the recommended action should be taken to prevent these types of collisions.
- The Weekly vs Time Interval Collision is also determined by the highest amount of collisions that occurred seasonal and by what values. The bar chart highlights what is the maximum count shown and a recommendation is displayed for what the best steps are to take in order to prevent more collisions from happening in Spring.

All of this data is categorized by the Boroughs in NYC (Bronx, Brooklyn, Manhattan, Queens, Staten Island, and any unspecified areas).
<br></br>
<img width="606" height="35" alt="B6" src="https://github.com/user-attachments/assets/65d250cf-a788-4482-9762-4c80128a4312" />
- The data provided for each borough is connected through all the charts in this 1st Dashboard through its PivotTables and PivotCharts. 
- Any Borough selected will properly display the sought-out information needed. 

<sub> Dataset from Maven Analytics </sub>
