INTRODUCTION

Have you ever wondered what really goes wrong when a plane crashes? We did. So for our Capstone 46 project at Vephla University, my group (Group 6) decided to dig into more than 100 years of aeroplane crash records to find out.
The dataset is a record of global aeroplane crashes from 2 May 1918 to 3 June 2022. After cleaning, it holds 28,457 accidents, and we kept 18 columns to work with. Each row is one accident. It tells us when and where the crash happened, the aircraft and the operator, the phase of flight, the crash site, how many people were on board, how many died, and the cause. The data came from [https://www.kaggle.com/datasets/abeperez/historical-plane-crash-data].
Here is what the data holds at a glance:
•	28,457 accidents recorded across 1,120 different aircraft and 8,960 operators
•	About 159,000 people died, and about 147,000 survived
•	11,811 accidents had no casualties at all
•	About 67% of the accidents involved civilian operators and 33% involved military ones
•	Human factors were the biggest known cause, at 34.79%. But 31.47% of the causes are listed as Unknown, so the real picture may be different
Our goal was to answer simple questions. Where do crashes happen most? Which part of a flight is the most dangerous? Which kinds of flights and which regions lose the most lives? And has flying become safer over time?
We used two tools. Excel helped us clean the data: we removed 79 duplicates, replaced missing values, fixed spellings and grouped similar entries together. Power BI helped us build the data model (one central fact table and five dimension tables plus a date table), and then build the dashboards.
Our work follows five parts: the pre-analysis (what we expected to find), the in-analysis (what the charts show), the observations, our recommendations, and the limitations. The data was not perfect. It had many missing values, so we tell you clearly where we had to be careful.



PRE-ANALYSIS
1. Project Context
Data Story: The dataset used is a historical record of global airplane crashes from 1918 to 2022. It captures details such as:
•	Flight conditions (date, time, aircraft type, operator, phase of flight, location)
•	Crash outcomes (survival status, fatalities, cause)
•	Contextual factors (technical, human, environmental causes)
Industry Type: Military/commercial aviation and manufacturing & engineering.
Stakeholders:
•	Aviation Manufacturers & Regulators
•	Airline Operators
•	The Public
•	Researchers
Definition of Success: Reduced accident frequency and improved survival rates, in order to gain public confidence and enable growth and advancement within the aviation industry.
2. Data Structure
Independent Variables:
•	Date, Time, Aircraft, Operator, Registration, Flight Phase, Flight Type, Flight Category, Crash Site, Schedule, MSN, YOM, Flight No., Crash Location, Country, Region, Crash Cause, Crew on Board, Pax on Board
Dependent Variables:
•	Survival Status, Crew Fatalities, Crew Fatality Discrepancy, Pax Fatalities, Pax Fatality Discrepancy, Other Fatalities, Total Fatalities, Circumstances
3. Potential Questions
•	Which aircraft models had the highest frequency of technical failures?
•	Were technical failures more common during takeoff, flight, or landing phases?
•	Were training flights more prone to human factor accidents than operational or postal flights?
•	Did human factor accidents result in higher or lower fatality rates compared to technical failures?
•	How often did weather (fog, storms, crosswinds) contribute to crashes, and which regions were most affected?
•	Which flight type has the highest survival likelihood?
•	Which flight type has the highest fatalities per crash?
•	Which aircraft type (DH.4, Avro 504, Handley Page, Blackburn Kangaroo, etc.) had the highest accident rate overall?
•	What region and country has the highest fatalities?
•	How many fatalities occur outside the aircraft?
•	Which regions experience the highest number of aircraft accidents?
•	Which flight categories and flight types are most affected by accidents and fatalities?
•	Which crash sites have the highest fatality impact?
•	How many accidents occurred with no casualties?
•	Comparative analysis of crew and passengers on board with crew and passenger fatalities.
4. Potential Insights
•	Models with older rotary engines could be disproportionately represented, as rotary engines were notoriously temperamental and prone to fuel and/or oil failures.
•	Technical failures may produce higher fatality rates because they can be sudden and unrecoverable, while human factor accidents might allow more reaction time, leading to survivable crash landings in some cases.
•	Weather related crashes may cluster seasonally, with winter months showing higher incident rates.
•	Passenger flights might have better survival due to more careful pre flight checks driven by commercial accountability. They almost certainly show the highest fatalities per crash due to higher occupancy.
•	Great Britain is most likely to top the list with the highest fatalities since it was the most active early aviation hub with the highest flight volume in the dataset period.
•	Regions with poor infrastructure and limited emergency response would likely show higher fatality to accident ratios even with fewer total crashes.
 
METHODOLOGY
●	Excel was used for data extraction and cleaning.
●	Power BI was used for data modelling, data visualization and uncovering data insights.
Data cleaning
                                            
Day 1 – Initial Observation
•	Reviewed the dataset to understand its structure and alignment with the task.
•	Dataset contained 24 columns and 28,537 rows(plus header), spanning years 1918–2022.
•	Selected 18 relevant columns for analysis.

Day 2 – Pre processing
•	Duplicated the dataset to maintain a before and after reference.
•	Checked for duplicates: 79 found.
•	Checked for blanks: none found.
•	Standardized missing values: 
o	Text fields: replaced NA with “Unknown”.
o	Numeric fields: replaced NA with 0.
•	Corrected column headings for clarity.
•	Converted date format using: =TEXT(A2,"dd/mm/yyyy")

Day 3 – Column Cleaning & Categorization
•	Created a data dictionary.
•	Renamed Survivors column to Survival Status. 
•	Replaced NA with Unknown (~1,288 replacements).
•	We applied this formular to come up with a more understandable column as Yes and No did not appear clear enough =IF(H2="Yes","Survival",IF(H2="No","Non-Survival","Unknown"))
•	Categorized Flight Type into broader groups (Environmental, Private, Humanitarian, G&D, Operational, Commercial, Unknown) using nested IF logic. =IF(OR(G2="Aerial photography",G2="Cinematography",G2="Geographical/geophysical/scientific",G2="Meteorological/weather",G2="Spraying (Agricultural)",G2="Topographic"),"Environmental",IF(OR(G2="Aerobatic",G2="Private",G2="Skydiving/paratroopers"),"Private",IF(OR(G2="Ambulance",G2="Fire fighting",G2="Humanitarian",G2="Refueling"),"Humanitarian",IF(OR(G2="Bombing",G2="Illegal (Smuggling)",G2="Military",G2="Millitary",G2="Supply",G2="Survey"),"G & D",IF(OR(G2="Calibration",G2="Demonstration",G2="Ferry",G2="Positioning",G2="Test",G2="Training"),"Operational",IF(OR(G2="Cargo",G2="Non scheduled revenue flight",G2="Delivery",G2="Executive/corporate/business",G2="Postal (mail)",G2="Scheduled revenue flight"),"Commercial","Unknown"))))))

•	Cleaned Flight Phase column: 
o	Replaced NA with Unknown (~631).
o	Removed redundant entries like (Climb) (~6,040) and (Descent/Approach) (~10,005).
•	Cleaned Crash Site column: 
o	Replaced NA with Unknown (~378).
o	Standardized entries: “<10km from airport” → Airport (~13,651), “Lake/Sea/Ocean/River” → Ocean (~3,844).
o	Trimmed spaces using =TRIM(I2).
•	Region column: replaced 1 NA with Unknown.
•	Crash Cause column: grouped Terrorism Act, Hijacking, Sabotage into Terrorism (~1,258 replacements).

Day 4 – Final Adjustments
•	Replaced NA in columns Q–U with Unknown (~9 replacements).
•	Simplified Flight Type entries (e.g., “Survey/Patrol/Reconnaissance” → Survey ~894 replacements).
•	Created a new Flight Category column to complement Flight Type.
•	Edited Crash Cause column for consistency and readability.

Screenshots 
          


Constraints & Challenges
•	High volume of NA values in numeric columns (crew, pax, MSN, time).
•	Logical inconsistencies: 
o	Crew fatalities > Crew on board.
o	Passenger fatalities > Passengers on board.
•	Time column contained numerous NA and incorrect entries.
•	MSN column had extensive missing values.
•	Replacing NA with 0 in numeric fields did not fully resolve issues and sometimes introduced inconsistencies.

Data modelling
A star schema was created in power query by breaking down a large dataset with 27 columns and 28,457 rows into 6 dimensional tables (i.e., Dim-Location, Dim-Operator, Dim-Aircraft, Dim-FlightDetails and Dim-CrashCause) and a central fact table. The Dim-Date table was created using DAX formula.
All the relationships created between the fact table and the dimensional tables were many to one (*:1) as observed in the model view. This process highlighted inconsistencies within the tables, such as duplicates, after generating the fact table, therefore enhancing data quality.

 
Creation of the Dim-Date table using DAX

Creation of fact and dimensional tables in power query editor while using the final data as the reference.
The star schema: Central fact table surrounded by dimensional tables with a many to one (*:1) relationship.


Data Visualization
The dashboard provides a consolidated analysis of the global airplane crashes between 2,may,1918 to 3,june,2022. Highlighting the root causes: human, environmental and technical and the change in survival rate and accidents occurrence over time.


KEY INSIGHTS
Total accidents - 28,457
Total fatalities - 159,000
Total survivors - 147,000
Total accidents with no casualties - 11,811
Total aircraft - 1,120
The northern america region had the highest accidents (8179)
Human factors led as the main cause of global crashes with 34.79%

IN-ANALYSIS

Aircraft Accident Distribution by Operator Type

Key Observation: Civilian-operated aircraft account for a significantly higher number of accidents (19,026) compared to military operations (9,431). This indicates that civilian aviation contributes the majority of recorded incidents, likely due to higher flight frequency and broader commercial activity.
Additionally, military accidents, while fewer, may involve different operational conditions such as training exercises or defense missions, which could influence risk patterns differently from civilian aviation.

Trends in Aircraft Accidents and Survivors by Decade (1910 - 2020)

Key Observations: There’s a clear historical pattern in both accident frequency and survival outcomes:
●	Rapid Growth Phase (1910–1940):
Accidents increased sharply, peaking in the 1940s (5,493 cases). 
●	Decline in Accidents Post-1940s:
After the 1940s peak, accident counts show a steady decline, dropping to 265 in the 2020s. 
●	Survivability Has Improved Over Time:
Despite fewer accidents in later decades, total survivors increased significantly, peaking in the 1990s (24,010 survivors).
●	 Modern Era (2000s–2020s):
Both accidents and survivors are declining, which reflects.

Distribution of Aircraft Accidents by Crash Cause

Key Observations: The majority of aircraft accidents are not caused by external threats but by human and operational factors.
●	Human Factors dominate aviation accidents
With 9,901 incidents, human-related issues are the leading cause. This highlights that despite technological advancements.
●	High proportion of Unknown causes
A significant number (8,956 cases) fall under unknown causes, suggesting: Incomplete investigations, Poor historical data recording, and Limitations in early aviation analysis
●	Technical Failures are a major contributor
With 6,193 incidents, mechanical and system failures are the third leading cause, reinforcing the importance of regular maintenance, engineering improvements, safety checks
●	Weather-related accidents are relatively lower
Only 1,524 cases, indicating that modern forecasting systems are effective and Pilots are better trained to avoid hazardous conditions.
●	Terrorism and other causes are minimal but impactful
Though lower in count (1,258 and 625 respectively), these incidents are often:
○	High severity
○	High fatality events
○	Critical for aviation security policies

Aircraft Accidents by Flight Phase

Key Observations: Aircraft accidents are heavily concentrated in high-intensity operational phases (flight, landing, and takeoff):
●	Most accidents occur during active flight
The Flight phase (11,435 cases) has the highest number of accidents, indicating risks associated with: Cruise operations, Mid-air system failures, and Weather encounters.
●	Landing is a critical high-risk phase
With 10,005 incidents, landing is nearly as risky as in-flight operations. This is expected because landing involves: High pilot workload, Precision handling, and Environmental factors (runway conditions, visibility)
●	Takeoff also shows significant risk
At 6,040 cases, takeoff remains a dangerous phase due to: Mechanical strain on aircraft, Limited time to react to failures and High speed and low altitude conditions.
●	Minimal accidents during ground operations
Taxiing (236) and parking (110) have very low incident counts, suggesting: Lower operational complexity and Reduced severity environments.
●	Unknown category is negligible but notable
631 cases lack phase classification, indicating minor data gaps.

Seasonal Distribution of Aircraft Fatalities

Key Observations: Aircraft fatalities are relatively evenly distributed across seasons, but slightly higher during periods of weather transition and extremes, suggesting environmental conditions subtly influence accident severity rather than frequency alone.
●	Autumn records the highest fatalities
With 41,390 deaths, autumn stands out as the most fatal season. This may be linked to: Increased weather variability, Transitional atmospheric conditions.
●	Winter and Summer show nearly identical impact
Winter (40,461) and Summer (40,410) have almost equal fatality levels, indicating that: Extreme weather (winter storms, summer turbulence) plays a role, Risk is relatively consistent across these seasons.
●	Spring has the lowest fatalities
At 36,258, spring appears to be the safest season comparatively, possibly due to: Milder and more stable weather conditions

Aircraft Accidents and Fatalities by Flight Type

Key Observations: Commercial aviation accidents may occur less frequently relative to total global flights, but they produce the highest fatality impact due to passenger volume, while military and training operations reflect higher operational risk environments.
●	Scheduled Revenue Flights record the highest fatalities
Although accounting for 6,015 accidents, scheduled commercial flights resulted in the highest number of deaths (74,743 fatalities).
This is likely because commercial aircraft typically carry a large number of passengers, making accidents more catastrophic.
●	Military operations show high accident frequency
Military flights recorded 4,625 accidents and 28,423 fatalities, reflecting the risks associated with combat missions, training exercises and specialized operations.
●	Training flights have moderate accidents but lower fatalities
With 3,289 accidents and 8,873 fatalities, training flights experience frequent incidents, but fatalities remain relatively lower due to smaller aircraft sizes, controlled training environments.
●	Cargo flights have comparatively lower fatalities
Despite 2,812 accidents, cargo flights recorded only 5,865 fatalities, likely because fewer onboard personnel are involved, passenger absence reduces casualty counts.
●	Charter/Taxi flights show high fatality impact relative to accidents
Non-scheduled revenue flights had 1,830 accidents but a notable 15,478 fatalities, suggesting potential safety inconsistencies and smaller operators with varying safety standards.

Aircraft Accidents and Fatalities by Flight Category

Key Observations: Commercial aviation dominates both accident occurrence and fatality counts, emphasizing the importance of maintaining strict safety standards in high-passenger operations, while private and operational flights reveal that aviation risk extends beyond commercial travel.
●	Commercial flights account for the highest fatalities
Commercial operations recorded 10,563 accidents and the highest fatality total (83,726 deaths). This highlights the significant impact of commercial aviation incidents due to high passenger capacity, frequent global operations.
●	G & D flights show substantial accident impact
With 6,827 accidents and 37,433 fatalities, G & D operations represent the second most affected category, indicating elevated operational risks.
●	Operational flights have high accident frequency but lower fatalities
Although 5,148 accidents were recorded, fatalities (12,451) are comparatively lower, suggesting smaller aircraft usage, reduced passenger involvement.
●	Private aviation presents moderate but notable risk
Private flights experienced 4,795 accidents and 21,931 fatalities, showing that non-commercial aviation still contributes significantly to overall aviation risk.
●	Environmental and Humanitarian flights show the lowest impact
These categories recorded the fewest accidents and fatalities, Environmental: 616 accidents, 797 fatalities and Humanitarian: 508 accidents, 2,181 fatalities. This may reflect: lower flight volumes, specialized operational planning.

Aircraft Accidents and Fatalities by Crash Site

Key Observations: While airports experience the highest number of aircraft accidents, crashes in mountainous regions, oceans, and cities tend to be far more severe, especially in terms of fatalities and collateral damage on the ground.
●	Airports record the highest number of accidents
Airports account for 13,561 accidents, making them the most common crash site. However, fatalities (54,471) are relatively proportional compared to the accident volume, likely because emergency response teams are readily available, accidents often occur during landing or takeoff phases.
●	Mountain crashes are the deadliest
Although mountains recorded only 3,429 accidents, they resulted in 37,947 fatalities, indicating an extremely high fatality severity. Possible reasons include: difficult terrain, harsh weather conditions, limited rescue accessibility.
●	Ocean crashes show high fatality impact
Ocean incidents (3,844 accidents) caused 25,009 fatalities, suggesting: lower survival chances, delayed rescue operations.
●	City crashes have the highest ground fatalities
Despite only 536 accidents, crashes in cities caused 2,486 ground fatalities, far exceeding other locations. This highlights the danger of aviation accidents in densely populated areas.
●	Plain valleys show moderate accident and fatality levels
With 6,504 accidents and 30,199 fatalities, these areas remain significant crash zones, likely due to emergency landings or uncontrolled descents.
●	Desert and unknown locations contribute minimally
These categories recorded the lowest accident and fatality counts.

Regional Distribution of Aircraft Accidents and Fatalities

Key Observations: Regions with the highest accident frequency are not always the deadliest. While North America records the most incidents, Asia experiences the highest fatality burden, suggesting differences in aircraft capacity, infrastructure, operational conditions, or accident severity.
●	Asia records the highest fatalities despite fewer accidents
Asia experienced 50,275 fatalities from 5,680 accidents, making it the deadliest region overall. This suggests that accidents in the region may involve: high-capacity aircraft, severe crash outcomes.
●	North America has the highest accident count
With 8,179 accidents, North America recorded the largest number of incidents, but fatalities (28,618) are lower than Asia and Europe. This may indicate: stronger safety systems, better emergency response and survivability.
●	Europe shows high fatalities with moderate accident frequency
Europe recorded 31,493 fatalities across 6,662 accidents, reflecting significant aviation activity and several high-impact incidents.
●	South America and Africa show notable fatality levels
Although accident counts are lower: South America → 16,478 fatalities, Africa → 15,018 fatalities. This may point to: infrastructure challenges, limited emergency response capacity in some regions.
●	Central America and Oceania have moderate aviation impact
Both regions recorded relatively lower accident and fatality figures compared to larger aviation markets.
●	Antarctica has the lowest aviation incident levels
Due to limited aviation activity, Antarctica recorded only 57 accidents and 329 fatalities.

OBSERVATIONS

●	A total of approximately 28,457 aviation accidents were recorded between 1918 and 2020.
●	These accidents resulted in an estimated 159,000 fatalities, highlighting the severe impact of such incidents.
●	The survival rate of about 48% indicates that nearly half of the recorded crashes had survivors.
●	Human factors account for the largest share of crashes (~35%), making them the leading cause of aviation accidents.
●	Approximately 66% of accidents involve civilian operators, while 34% are attributed to military operations.
●	Aviation fatalities increased steadily over the decades, reaching a peak in the late 20th century, followed by a decline in more recent years, suggesting improvements in safety measures.
●	Fatalities are relatively close across all seasons (Spring, Summer, Autumn, and Winter), indicating minimal seasonal impact on crash outcomes.
●	A significant number of accidents occur during critical flight phases, particularly takeoff and landing.
●	A total of about 219,000 passengers were onboard during recorded crashes, with passenger fatalities exceeding 104,000.
●	Over 86,000 crew members were involved in recorded incidents, with approximately 50,000 crew fatalities.
●	Ground fatalities remain relatively low at approximately 3,313 deaths, showing that most aviation-related fatalities occur onboard aircraft.
●	Scheduled commercial flights recorded the highest accident and fatality counts, reflecting the scale and frequency of global commercial aviation operations.
●	Military aviation also contributed significantly to total fatalities, indicating relatively high operational risk within military flight activities.
●	Commercial flight categories experienced the highest number of accident occurrences and fatalities compared to private, operational, humanitarian, and environmental flights.
●	North America recorded the highest accident frequency, followed by Europe and Asia, likely due to higher air traffic activity and reporting coverage.
●	Crashes occurring near airports and mountainous regions resulted in the highest fatality counts, highlighting the severity of accidents in these locations.
●	Accident sites such as oceans, valleys, and mountainous terrains showed high fatality impacts, likely due to difficult rescue and recovery operations.
●	Approximately 11,811 accidents recorded no casualties, indicating that a notable portion of aviation incidents were non-fatal. 

RECOMMENDATIONS

 Based on all analyses, here are strong, insight-driven recommendations:
1.	Strengthen Human Factor Risk Management
Since human factors are the leading cause of accidents, aviation stakeholders should:
●	Invest in advanced pilot training programs (simulations, emergency scenarios)
●	Implement fatigue management systems
●	Use AI-assisted decision support systems in cockpits
2.	Improve Aircraft Maintenance & Monitoring Systems
With technical failures ranking high, organizations should:
●	Adopt predictive maintenance using data analytics
●	Increase frequency of safety inspections
●	Integrate real-time aircraft health monitoring systems
3.	Focus on High-Risk Flight Phases 
Since most accidents occur during these phases:
●	Enhance landing and takeoff safety protocols
●	Upgrade runway infrastructure and navigation systems
●	Provide phase-specific pilot training
4. 	Enhance Weather Monitoring & Response Systems
Although weather-related accidents are fewer, they still contribute to fatalities:
●	Improve real-time weather tracking systems
●	Provide better pilot-weather communication tools
●	Enforce stricter no-fly policies during extreme conditions
 5. 	Improve Data Collection & Investigation Processes
The high number of unknown causes indicates data gaps:
●	Standardize global accident reporting systems
●	Use data analytics and forensic tools for investigations
●	Encourage transparent reporting across aviation bodies
6. 	Enhance Civil Aviation Safety Regulations
Since civilian flights account for most accidents:
●	Strengthen commercial airline safety compliance
●	Increase regulatory audits and monitoring
●	Enforce international safety standards
7. 	Continue Investment in Safety Technology
The decline in accidents over decades shows progress. Sustain investment in:
●	Automation systems
●	Navigation technology
●	Safety engineering
8. 	Seasonal Risk Preparedness
With slightly higher fatalities in Autumn and Winter:
●	Develop season-specific safety strategies
●	Prepare for weather variability and extreme conditions
●	Increase operational vigilance during high-risk seasons

LIMITATIONS

Although the dataset was massive and had a lot of variables to work with, it contained a lot of missing values (N/A, unknown) in columns such as YOM and MSM which led to a limited analysis on regulatory changes over time.

CONCLUSION

Over the decades there has been a steady decrease in aircraft crashes worldwide with its all time lowest being in the 2010s and 2020s this is highly attributed by the advancement in technology, proactive regulatory frameworks and data driven investigations. This has in turn led to the sharp increase in survival rate
