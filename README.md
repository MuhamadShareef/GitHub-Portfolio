# GitHub-Portfolio

Muhamad Shareef
Data Analyst 
11/11/2024


# Case Study: How does a bike-share navigate speedy success? 



## Introduction 

### Step 1: Ask

### Step 2: Prepare

### Step 3: Process

### Step 4: Analyze

### Step 5: Share

### Step 6: Act



## Quick links:
01-Data Combining.sql

02- Data Exploration.sql

03- Data Cleaning.sql

04- Data Analysis.sql

## Introduction 
In this case study, I’m going to be solving many real world scenarios a data analyst would solve. I’ll be working for Cyclistic, a fictional bike-share company, collaborating with various stakeholders.
The objective of this case study is to answer key business questions using the six steps of the data analysis process: Ask, Prepare, Process, Analyze, Share, and Act. To stay on track, I’ll follow the Case Study Roadmap, which will guide me through the process with guiding questions and key tasks.


## Scenario
As a junior data analyst on the marketing analytics team at Cyclistic, a bike-share company based in Chicago, I’ve been tasked with answering an important business question:
How can we convert casual riders into annual members?
The director of marketing, Lily Moreno, believes that the future success of the company depends on maximizing the number of annual memberships. To support this vision, my team wants to understand how casual riders and annual members use Cyclistic bikes differently. The insights we uncover will be used to create a targeted marketing strategy aimed at converting casual riders into annual members.
However, before implementing any strategies, I need to provide compelling data insights and professional visualizations to get approval from the Cyclistic Executive Team.


## Key Stakeholders
Here are the main characters and stakeholders involved:
Lily Moreno: Director of Marketing (Primary Stakeholder)
Cyclistic Executive Team: (Primary Stakeholders)
Cyclistic Marketing Analytics Team: (Secondary Stakeholders)


## Step 1: Ask
Problem Statement
The primary question we’re trying to solve is: How can we convert casual riders into annual members?
To guide the development of the marketing program, we will focus on answering the following questions:
How do annual members and casual riders use Cyclistic bikes differently?
Why would casual riders choose to purchase Cyclistic annual memberships?
How can Cyclistic use digital media to influence casual riders to become members?
Guiding Objective
The main goal is to build a profile for annual members and determine the best marketing strategies to convert casual riders. These insights will help the marketing team increase annual memberships.
Key Tasks
Clearly define the business task.
Identify and understand the key stakeholders.
Deliverable
A clear, well-defined statement of the business task, supported by insights into the differences between casual riders and annual members, as well as strategies for using digital media to influence behavior.





## Step 2: Prepare
To uncover these insights, I’ll be using Cyclistic’s historical trip data. This data, covering the last 12 months, is publicly available and provided by Motivate International Inc. under an open license. The data allows me to explore customer usage patterns, helping identify trends and differences between casual riders and annual members. I'll use the Case Study Roadmap to organize and clean the data systematically.

**Case Study Roadmap – Prepare
Guiding Questions**
Where is your data located?
The data is stored in a publicly accessible location and can be downloaded directly from Cyclistic’s partner site here.
How is the data organized?
The dataset is organized in CSV files, with each file representing trip data for a specific month. Each file contains columns such as trip start time, end time, ride duration, starting station, ending station, and rider type (casual or member).
Are there issues with bias or credibility in this data? Does your data ROCCC?
The data is provided by a reputable company, Motivate International Inc., ensuring credibility. However, potential biases may exist, such as underrepresentation of certain groups or missing data for specific timeframes or stations. I will evaluate the data to ensure it meets ROCCC standards (Reliable, Original, Comprehensive, Current, and Cited).
How are you addressing licensing, privacy, security, and accessibility?
The dataset is shared under an open license, allowing public use. Privacy concerns are minimal, as the data is aggregated and anonymized. I will handle the data responsibly and ensure it remains secure throughout the analysis process.
How did you verify the data’s integrity?
I’ll review the dataset for consistency by checking for null values, duplicates, and outliers. I’ll also cross-reference the file metadata (e.g., date ranges) to ensure completeness.
How does it help you answer your question?
The dataset contains information about ride patterns, durations, and rider types, which directly aligns with the questions I’m answering, such as differences in usage between casual riders and annual members.
Are there any problems with the data?
Possible issues include missing data for certain trips, errors in ride duration (e.g., negative or unrealistically long times), and discrepancies in station names. These issues will be addressed during the cleaning process.

**Key Tasks**
Download and store data appropriately.
I’ve downloaded the last 12 months of Cyclistic trip data and organized it into a dedicated folder for easy access.
Identify how it’s organized.
The data is in monthly CSV files, structured in rows and columns with consistent headers.
Sort and filter the data.
I’ll sort and filter the data to focus on relevant information, such as rider type and trip durations.
Determine the credibility of the data.
After reviewing its source and structure, I’ve confirmed that the data is credible and suitable for analysis.
Deliverable
I’ll provide a description of the data sources used:
Source: Cyclistic trip data from Motivate International Inc.
Format: Monthly CSV files covering the last 12 months.
Content: Includes columns such as trip start time, end time, duration, starting station, ending station, and rider type (casual or member).

## Step 3. Process (Data Cleaning)
Reference: 01-Data Combining.sql

**Goal:** To prepare the data for analysis by ensuring accuracy, consistency, and completeness.
**Merging All Tables in BigQuery**
Since we are dealing with hundreds of thousands of rows, we cannot utilize Google sheets so we will do all of our analysis with SQL. Now that the tables are uploaded to BigQuery, we can start to merge them. 

**Steps to Resolve Incompatible Column Types**
We need to make sure all the columns are formatted correctly to ensure a smooth combining of 12 sheets into one table. I checked column types in each table. I inspected the schema of all 12 tables to identify the columns causing a mismatch. 

**Standardize Data Types**
Once the problem was identified as a mismatch in the SCHEMA between tables, I standardized the data types using CAST function then a UNION ALL query to tie everything together. 

**Ensuring uniformity across all tables**
To make the query more efficient and comprehensive, especially considering variations in column types (like INTEGER vs. STRING for start_station_id and end_station_id), I ensured uniformity across all tables. 
Ensured all date and time columns are in the correct format and timezone to avoid inconsistencies during the analysis phase. Standardizing these formats will make the analysis process more reliable and easier to perform.
SELECT 
  CAST(ride_id AS STRING) AS ride_id,
  CAST(rideable_type AS STRING) AS rideable_type,
  TIMESTAMP(started_at) AS started_at,
  TIMESTAMP(ended_at) AS ended_at,
  CAST(start_station_name AS STRING) AS start_station_name,
  CAST(start_station_id AS STRING) AS start_station_id,
  CAST(end_station_name AS STRING) AS end_station_name,
  CAST(end_station_id AS STRING) AS end_station_id,
  CAST(start_lat AS FLOAT64) AS start_lat,
  CAST(start_lng AS FLOAT64) AS start_lng,
  CAST(end_lat AS FLOAT64) AS end_lat,
  CAST(end_lng AS FLOAT64) AS end_lng,
  CAST(member_casual AS STRING) AS member_casual
FROM `leafy-sanctuary-412122.cyclistic_data.cyclistic_data_2019_q010`

UNION ALL
-- Repeat for all remaining tables

**Additional Steps in Data Cleaning and Preparation**
Reference: 02- Data Exploration.sql 

**Checked the data types of all columns:** Ensured that column data types are consistent and align with the expected schema to avoid errors during merging or analysis. 
Counted NULL values for each column in the table: Identified missing data in each column to evaluate its impact on analysis and decide on appropriate handling methods.
**Removed rows with NULL values in key columns:** Deleted rows with missing values in essential columns, such as ride_id or start_station_id, to maintain the integrity and reliability of the dataset.
**Checked for duplicate rows:** Identified and removed duplicate entries to prevent overestimation or redundancy in the analysis.
Checked if all ride_id values have the same length: Verified the consistency of ride_id lengths to ensure that each ride is uniquely and correctly identified.
**Checked for unique types in rideable_type:** Analyzed the values in the rideable_type column to confirm that all ride types are valid and properly categorized.

**Created and exported a clean data table**
Reference: 03- Data Cleaning.sql

## Step 4: Analyze (Data Analysis)
Reference: 04- Data Analysis.sql
**Goal:** To derive insights and meaningful conclusions from the clean dataset.

**Exploring Descriptive Statistics:**
I start by examining key metrics like the **average ride length, trip count**, and **ride type distribution**. This helps identify general trends and gives us a broad overview of the dataset.

**Analyzed the minimum and maximum dates in the dataset.**
**Results:**


Min_date
Max_date
2020-04-01
2021-04-06




**How do annual members and casual riders use Cyclistic bikes differently?**

**Results:** 


Casual Rider Average Time
Member Rider Average Time
42.8 minutes
11.42 minutes


**Explored whether casual riders are more likely to ride on weekends compared to members.**
I segmented the data by day of the week (weekdays vs. weekends) to uncover if casual riders tend to take longer trips on weekends compared to weekdays, and compare this to annual members’ behavior.


rider_type
day_type
total_rides
Casual
Weekday
831,614
Member
Weekday
1,468,833
Member
Weekend
590,539
Casual
Weekend
598,762



**Comparative Analysis:**
I performed **group comparisons** between casual riders and annual members based on their trip characteristics.

**Trip length by rider** 

rider_type
avg_trip_length_minutes
max_trip_length_minutes
min_trip_length_minutes
total_trips
Casual
45.4
55683
1
1,334,151
Member
15.7
58720
1
1,907,130


I separated data by **weekdays** and **weekends**, and compared the **average trip length** and **total rides** for each group. This analysis will allow us to assess whether casual riders have longer or shorter trips compared to members, and whether this behavior differs on weekends.

**Trip length by rider on weekends vs weekday** 

rider_type
day_type
avg_trip_length_minutes
max_trip_length_minutes
min_trip_length_minutes
total_trips
Casual
Weekend
48.9
51145
1
563,894
Member
Weekend
17.7
58720
1
545,940
Casual
Weekday
42.9
55683
1
770,257
Member
Weekday
14.9
41271
1
1,361,190



**Total number of trips per month by Rider**

**Results in Tableau**  



As we can see, the most popular months are to no surprise, the summer months which start to peak around July and August. 


**Total number of trips per week**
Based on the analysis, the most popular week for riders is week 41. And we see the most popular weeks to ride on are between July through October. 

trip_year
trip_week
total_trips
2020
41
86583
2020
42
55374
2020
43
52797
2020
44
77732
2020
45
64191
2020
46
44022
2020
47
28715
2020
48
32120
2020
49
29703
2020
50
27780
2020
51
20027
2020
52
12410
2021
0
2876
2021
1
22726
2021
2
22961
2021
3
19528
2021
4
15050
2021
5
9306
2021
6
6942
2021
7
3820
2021
8
20274
2021
9
29320



day_of_week
rider_type
total_trips
Sunday
casual
250344
Sunday
member
251416
Monday
casual
142332
Monday
member
252664
Tuesday
casual
136588
Tuesday
member
269439
Wednesday
casual
148641
Wednesday
member
289401
Thursday
casual
156446
Thursday
member
284598
Friday
casual
197030
Friday
member
290165
Saturday
casual
319858
Saturday
member
305769



**Results in Tableau:** 




**Analyzed peak hours of usage by rider type**

**Results:** 
Conducted a peak hour usage analysis to identify the most active hours for casual riders and annual members. By extracting the hour from trip start times and grouping data by rider type, I determined that casual riders peak between 4 PM and 7 PM, while members exhibit a similar pattern, with a more pronounced peak at 5 PM. This insight highlights differences in rider behavior and provides a foundation for targeted marketing or operational adjustments.

**Top Results:** 
Member Riders
hour_of_day
rider_type
ride_count
17
member
205463
18
member
178600
16
member
171213
15
member
142325
12
member
128790
13
member
128010
14
member
127866


Casual Riders
hour_of_day
rider_type
ride_count
17
casual
133180
18
casual
120467
16
casual
119631
15
casual
112816
14
casual
107190
13
casual
101074
12
casual
92961

**Results in Tableau:** 




**Average ride length per month**

**Results:** 
The analysis reveals interesting trends in average ride lengths across the months. The longest average ride lengths occur in July, which aligns with expectations due to the warm, summer weather encouraging outdoor activities. The trend begins to pick up in April, continues through May and June, and peaks in July. After July, ride lengths start to decline gradually as the year progresses into cooler months.


month_name
month_number
rider_type
avg_ride_length_minutes
total_trips
Jan
1
member
11.67
68039
casual
26.07
14583
Feb
2
member
14.54
33793
casual
47.22
8508
Mar
3
member
13.35
128349
casual
38.28
75059
Apr
4
member
21.16
60236
casual
72.44
23427
May
5
casual
50.48
86072
member
19.38
111447
Jun
6
casual
51.15
153113
member
18.32
184996
Jul
7
member
17.35
276181
casual
59.23
266156
Aug
8
member
16.36
318257
casual
44.37
278085
Sep
9
member
15.03
278976
casual
38.39
212122
Oct
10
member
13.66
211708
casual
31.25
120597
Nov
11
casual
33.33
72115
member
13.18
147089
Dec
12
casual
27.33
24314
member
11.99
88059



**Results in Tableau:**







**Average ride length per day of week**

**Results:** 
Ride lengths are longer during weekends, suggesting more recreational use of bikes, whereas weekdays see shorter, purpose-driven rides. These insights could inform targeted promotions or service adjustments based on rider behavior.

day_of_week
avg_ride_length_minutes
Sunday
34.56
Monday
25.91
Tuesday
23.55
Wednesday
23.66
Thursday
25.01
Friday
26.63
Saturday
32.76







**Results in Tableau:** 




**Analyzed Popular Stations/Top Routes**
**Results in Tableau**:




**Results:** 
1. Aggregate by Top Stations or Routes: results-20241112-133926


**Analyze by Rider Type: Member
Results:** 
2. Analyze by Rider Type: Member - results-20241112-134338


**Rider Type: Member**
**Top 10 Most Popular Stations/Routes** 
Rider Type: Member
start_station_name
end_station_name
number_of_rides
MLK Jr Dr & 29th St
State St & 33rd St
1259
State St & 33rd St
MLK Jr Dr & 29th St
1119
Clark St & Elm St
Clark St & Elm St
1100
Lake Shore Dr & Wellington Ave
Lake Shore Dr & Wellington Ave
1080
Lakefront Trail & Bryn Mawr Ave
Lakefront Trail & Bryn Mawr Ave
1043
Lake Shore Dr & Belmont Ave
Lake Shore Dr & Belmont Ave
1033
Burnham Harbor
Burnham Harbor
1026
Theater on the Lake
Theater on the Lake
983
Dearborn St & Erie St
Dearborn St & Erie St
971
Lake Shore Dr & North Blvd
Lake Shore Dr & North Blvd
965



**Result in Tableau**:
Top Stations by Number of Rides (Horizontal Bar Chart)







**Analyze by Rider Type: Casual
Results:**
2. Analyze by Rider Type: Casual - results-20241112-134713


**Rider Type: Casual**
**Top 10 Most Popular Stations/Routes** 


Rider Type: Casual
start_station_name
end_station_name
number_of_rides
Streeter Dr & Grand Ave
Streeter Dr & Grand Ave
6093
Lake Shore Dr & Monroe St
Lake Shore Dr & Monroe St
5934
Millennium Park
Millennium Park
4998
Buckingham Fountain
Buckingham Fountain
4844
Indiana Ave & Roosevelt Rd
Indiana Ave & Roosevelt Rd
3887
Michigan Ave & Oak St
Michigan Ave & Oak St
3576
Fort Dearborn Dr & 31st St
Fort Dearborn Dr & 31st St
3161
Michigan Ave & 8th St
Michigan Ave & 8th St
3134
Shore Dr & 55th St
Shore Dr & 55th St
2993
Theater on the Lake
Theater on the Lake
2878



**Results in Tableau**:







**Aggregate Popular Routes**
Combined start and end station names into a single route and analyzed their popularity.
Results: 
3. Aggregate Popular Routes: results-20241112-134927
**Results in Tableau**:



**Summarize Results by Start Station**

Aggregated the data to see the total rides originating or ending at each station.
Results: 
4. Summarize Results by Start Station: results-20241112-135208
Tableau:




**Summarize Results by End Station 
Results:**
4. Summarize Results by End Station: results-20241112-135432
**Results in Tableau**:



## Step 5: Share 
**SQL Query:**
**Data Visualization:** 

Now that the data is processed, cleaned, and analyzed we can share our findings. I queried multiple data sets for the analysis and visualized them in Tableau. To answer the main question: How do annual members and casual riders use Cyclistic bikes differently?

## Key Insights: How Casual Riders and Annual Members Use Cyclistic Bikes Differently
**Ride Duration:**
Casual riders have significantly longer average trip durations (42.8 minutes) compared to annual members (11.42 minutes). This suggests casual riders may use bikes for recreational purposes, while members use them for commuting or short trips.
**Day and Time Preferences:**
Casual riders are more active on weekends, aligning with leisure activities.
Members ride consistently throughout the week, peaking during commuting hours (e.g., 5 PM).
**Seasonal Trends:**
Both groups ride more frequently during summer (June–August), but casual riders exhibit sharper increases, likely driven by favorable weather for recreation.
**Top Stations and Routes:**
Casual riders favor stations near tourist spots or recreational areas, while members prefer stations near transit hubs or workplaces.
**Peak Usage Hours:**
Casual riders’ trips peak between 4 PM and 7 PM, which overlaps with members’ peak usage. However, members exhibit a sharper peak at 5 PM, likely tied to commuting patterns.
**Recurring Behavior:**
Members exhibit consistent behavior in ride frequency and timing, indicating habitual use, while casual riders demonstrate irregular, event-driven patterns.


## Step 6: Act 
**Actionable Recommendations**
**Targeted Marketing Strategies:**
**Recreational Appeal:** Promote membership benefits for weekend riders, such as discounts for long rides or family packages.
**Seasonal Campaigns:** Run summer promotions emphasizing cost savings with annual memberships compared to single-use pricing.
**Digital Media Strategies:**
**Geotargeted Ads:** Advertise near popular tourist locations and recreational hotspots highlighting the convenience and savings of becoming a member.
**Social Proof:** Use testimonials or success stories of casual riders who transitioned to memberships for cost savings and added benefits.
**Personalized Membership Offers:**
Offer trial memberships with incentives, such as the first month free or free weekend rides for casual riders who register during peak seasons.
Implement referral programs where existing members receive perks for converting casual riders to members.
**Operational Enhancements:**
**Weekend Promotions:** Provide discounts or promotional offers during weekends to nudge casual riders toward memberships.
**Station Placement:** Expand stations in areas frequented by casual riders and offer exclusive member perks at those locations.
**Behavioral Nudges:**
**Ride Analytics:** Show casual riders data about their total spending and potential savings as members after completing a ride.
**Gamification:** Introduce milestones or rewards for casual riders who increase their ride frequency, linking these achievements to discounted memberships.


**Next Steps**
**Share Findings:**
Present these insights and recommendations to the Cyclistic Executive Team using professional visualizations in Tableau.
Highlight the potential ROI of converting casual riders into annual members using usage trends and financial implications.
**Implement A/B Testing:**
Test different marketing messages and promotional offers to determine the most effective strategies for casual rider conversion.
**Monitor and Evaluate:**
Track the impact of implemented strategies using KPIs like the conversion rate of casual riders to annual members and overall membership growth.

**Executive Summary**
The data reveals that casual riders primarily use Cyclistic bikes for recreational purposes, while annual members use them for daily commuting. To convert casual riders into members, the company should emphasize cost savings, convenience, and exclusive perks through targeted campaigns and operational adjustments. These strategies align with observed rider behavior, ensuring a higher likelihood of adoption.
By addressing these key areas, Cyclistic can capitalize on its data-driven insights to increase annual memberships, ensuring sustainable growth and success.
