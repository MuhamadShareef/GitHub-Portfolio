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

**Lily Moreno:** Director of Marketing (Primary Stakeholder)

**Cyclistic Executive Team:** (Primary Stakeholders)

**Cyclistic Marketing Analytics Team:** (Secondary Stakeholders)


## Step 1: Ask
**Problem Statement**

The primary question we’re trying to solve is: How can we convert casual riders into annual members?

To guide the development of the marketing program, we will focus on answering the following questions:

**1.** How do annual members and casual riders use Cyclistic bikes differently?

**2.** Why would casual riders choose to purchase Cyclistic annual memberships?

**3.** How can Cyclistic use digital media to influence casual riders to become members?
   
**Guiding Objective**

The main goal is to build a profile for annual members and determine the best marketing strategies to convert casual riders. These insights will help the marketing team increase annual memberships.



**Key Tasks**
- Clearly define the business task.
- Identify and understand the key stakeholders.

  


**Deliverable**
A clear, well-defined statement of the business task, supported by insights into the differences between casual riders and annual members, as well as strategies for using digital media to influence behavior.





## Step 2: Prepare

To uncover these insights, I’ll be using Cyclistic’s **historical trip data**. This data, covering the last 12 months, is publicly available and provided by Motivate International Inc. under an open license. The data allows me to explore customer usage patterns, helping identify trends and differences between casual riders and annual members. I'll use the Case Study Roadmap to organize and clean the data systematically.


**Case Study Roadmap – Prepare**

**Guiding Questions**

**1- Where is your data located?**

The data is stored in a publicly accessible location and can be downloaded directly from Cyclistic’s partner site here.

**2- How is the data organized?**

The dataset is organized in CSV files, with each file representing trip data for a specific month. Each file contains columns such as trip start time, end time, ride duration, starting station, ending station, and rider type (casual or member).

**3- Are there issues with bias or credibility in this data? Does your data ROCCC?**

The data is provided by a reputable company, Motivate International Inc., ensuring credibility. However, potential biases may exist, such as underrepresentation of certain groups or missing data for specific timeframes or stations. I will evaluate the data to ensure it meets ROCCC standards (Reliable, Original, Comprehensive, Current, and Cited).

**4- How are you addressing licensing, privacy, security, and accessibility?**

The dataset is shared under an open license, allowing public use. Privacy concerns are minimal, as the data is aggregated and anonymized. I will handle the data responsibly and ensure it remains secure throughout the analysis process.

**5- How did you verify the data’s integrity?**

I’ll review the dataset for consistency by checking for null values, duplicates, and outliers. I’ll also cross-reference the file metadata (e.g., date ranges) to ensure completeness.

**6- How does it help you answer your question?**

The dataset contains information about ride patterns, durations, and rider types, which directly aligns with the questions I’m answering, such as differences in usage between casual riders and annual members.

**7- Are there any problems with the data?**

Possible issues include missing data for certain trips, errors in ride duration (e.g., negative or unrealistically long times), and discrepancies in station names. These issues will be addressed during the cleaning process.



**Key Tasks**
   - **Download and store data appropriately.**

   I’ve downloaded the last 12 months of Cyclistic trip data and organized it into a dedicated folder for easy access.

   - **Identify how it’s organized.**

   The data is in monthly CSV files, structured in rows and columns with consistent headers.
   

   - **Sort and filter the data.**

   I’ll sort and filter the data to focus on relevant information, such as rider type and trip durations.
   

   - **Determine the credibility of the data.**

   After reviewing its source and structure, I’ve confirmed that the data is credible and suitable for analysis.



**Deliverable**

I’ll provide a description of the data sources used:

- **Source:** Cyclistic trip data from Motivate International Inc.

- **Format:** Monthly CSV files covering the last 12 months.

- **Content:** Includes columns such as trip start time, end time, duration, starting station, ending station, and rider type (casual or member).



## Step 3. Process (Data Cleaning)
Reference: 01-Data Combining.sql

**Goal:** To prepare the data for analysis by ensuring accuracy, consistency, and completeness.

**1- Merging All Tables in BigQuery**

Since we are dealing with hundreds of thousands of rows, we cannot utilize Google sheets so we will do all of our analysis with SQL. Now that the tables are uploaded to BigQuery, we can start to merge them. 

**2- Steps to Resolve Incompatible Column Types**

We need to make sure all the columns are formatted correctly to ensure a smooth combining of 12 sheets into one table. I checked column types in each table. I inspected the schema of all 12 tables to identify the columns causing a mismatch. 

**3- Standardize Data Types**

Once the problem was identified as a mismatch in the SCHEMA between tables, I standardized the data types using CAST function then a UNION ALL query to tie everything together. 

**4- Ensuring uniformity across all tables**

To make the query more efficient and comprehensive, especially considering variations in column types (like INTEGER vs. STRING for start_station_id and end_station_id), I ensured uniformity across all tables. 

Ensured all date and time columns are in the correct format and timezone to avoid inconsistencies during the analysis phase. Standardizing these formats will make the analysis process more reliable and easier to perform.

![images](images/4-ensuring-uniformity-across-all-tables.PNG)


**Additional Steps in Data Cleaning and Preparation**

Reference: 02- Data Exploration.sql 

**Checked the data types of all columns:** 

Ensured that column data types are consistent and align with the expected schema to avoid errors during merging or analysis. 

**Counted NULL values for each column in the table:** 

Identified missing data in each column to evaluate its impact on analysis and decide on appropriate handling methods.

**Removed rows with NULL values in key columns:** 

Deleted rows with missing values in essential columns, such as ride_id or start_station_id, to maintain the integrity and reliability of the dataset.

**Checked for duplicate rows:** 

Identified and removed duplicate entries to prevent overestimation or redundancy in the analysis.

**Checked if all ride_id values have the same length:** 

Verified the consistency of ride_id lengths to ensure that each ride is uniquely and correctly identified.

**Checked for unique types in rideable_type:** 

Analyzed the values in the rideable_type column to confirm that all ride types are valid and properly categorized.

**Created and exported a clean data table**

Reference: 03- Data Cleaning.sql



## Step 4: Analyze (Data Analysis)
Reference: 04- Data Analysis.sql


**Goal:** To derive insights and meaningful conclusions from the clean dataset.

**Exploring Descriptive Statistics:**
I start by examining key metrics like the **average ride length, trip count**, and **ride type distribution**. This helps identify general trends and gives us a broad overview of the dataset.

**Analyzed the minimum and maximum dates in the dataset.**
**Results:**

![images](images/1-min-max-dates.png)



Min_date
Max_date
2020-04-01
2021-04-06




**How do annual members and casual riders use Cyclistic bikes differently?**

**Results:** 

![images](images/2-how-do-annual-members-and-casual-riders-use-Cyclistic-bikes-differently.png)

Casual Rider Average Time
Member Rider Average Time
42.8 minutes
11.42 minutes


**Explored whether casual riders are more likely to ride on weekends compared to members.**

I segmented the data by day of the week (weekdays vs. weekends) to uncover if casual riders tend to take longer trips on weekends compared to weekdays, and compare this to annual members’ behavior.

![images](images/3-explored-whether-casual-riders-are-more-likely-to-ride-on-weekends-compared-to-members.png)




**Comparative Analysis:**

I performed **group comparisons** between casual riders and annual members based on their trip characteristics.

**Trip length by rider** 

![images](images/4-trip-length-by-rider.png)


I separated data by **weekdays** and **weekends**, and compared the **average trip length** and **total rides** for each group. This analysis will allow us to assess whether casual riders have longer or shorter trips compared to members, and whether this behavior differs on weekends.

**Trip length by rider on weekends vs weekday** 

![images](images/5-trip-length-by-rider-on-weekends-vs-weekday.png)



**Total number of trips per month by Rider**

**Results in Tableau**  

![images](images/6-total-number-of-trips-per-month-by-rider.png)

As we can see, the most popular months are to no surprise, the summer months which start to peak around July and August. 


**Total number of trips per week**
Based on the analysis, the most popular week for riders is week 41. And we see the most popular weeks to ride on are between July through October. 

![images](images/7-total-number-of-trips-per-week-1.png)



![images](images/7-total-number-of-trips-per-week-2.png)


**Results in Tableau** 

![images](images/8-results-in-tableau-png.png)


**Analyzed peak hours of usage by rider type**

**Results:** 
Conducted a peak hour usage analysis to identify the most active hours for casual riders and annual members. By extracting the hour from trip start times and grouping data by rider type, I determined that casual riders peak between 4 PM and 7 PM, while members exhibit a similar pattern, with a more pronounced peak at 5 PM. This insight highlights differences in rider behavior and provides a foundation for targeted marketing or operational adjustments.

**Top Results:** 

![images](images/9-analyzed-peak-hours-of-usage-by-rider-type-png.png)

**Results in Tableau** 

![images](images/10-results-in-tableau-png.png)


**Average ride length per month**

**Results:** 
The analysis reveals interesting trends in average ride lengths across the months. The longest average ride lengths occur in July, which aligns with expectations due to the warm, summer weather encouraging outdoor activities. The trend begins to pick up in April, continues through May and June, and peaks in July. After July, ride lengths start to decline gradually as the year progresses into cooler months.


![images](images/11-average-ride-length-per-month-png.png)


**Results in Tableau**


![images](images/12-results-in-tableau-png.png)




**Average ride length per day of week**

**Results:** 
Ride lengths are longer during weekends, suggesting more recreational use of bikes, whereas weekdays see shorter, purpose-driven rides. These insights could inform targeted promotions or service adjustments based on rider behavior.

![images](images/13-average-ride-length-per-day-of-week-1-png.png)


![images](images/13-average-ride-length-per-day-of-week-2-png.png)


![images](images/13-average-ride-length-per-day-of-week-3-png.png)

**Results in Tableau** 

![images](images/13-results-in-tableau-png.png)


**Analyzed Popular Stations/Top Routes**
**Results in Tableau**

![images](images/14-analyzed-popular-stations-top-routes-1-png.png)

![images](images/14-analyzed-popular-stations-top-routes-2-png.png)



**Rider Type: Member**
**Top 10 Most Popular Stations/Routes** 


![images](images/15-top-10-most-popular-stations-routes-png.png)


**Result in Tableau**:
Top Stations by Number of Rides (Horizontal Bar Chart)

![images](images/16-results-in-tableau-top-stations-by-number-of-rides-horizontal-bar-chart-png.png)



**Rider Type: Casual**
**Top 10 Most Popular Stations/Routes** 


![images](images/17-top-10-most-popular-stations-routes-casual-png.png)


**Results in Tableau**:

![images](images/17-result-in-tableau-png.png)





**Aggregate Popular Routes**
Combined start and end station names into a single route and analyzed their popularity.


**Results in Tableau**:

![images](images/18-aggregate-popular-routes-results-in-tableau-png.png)


**Summarize Results by Start Station**

Aggregated the data to see the total rides originating or ending at each station.


**Results in Tableau**:

![images](images/19-summarize-results-by-start-station-results-in-tableau-png.png)


**Summarize Results by End Station** 


**Results in Tableau**:

![images](images/20-summarize-results-by-end-station-results-in-tableau-png.png)


## Step 5: Share 

- **SQL Query:** [insert-link]
- **Data Visualization:** [insert-link]

Now that the data is processed, cleaned, and analyzed we can share our findings. I queried multiple data sets for the analysis and visualized them in Tableau. To answer the main question: How do annual members and casual riders use Cyclistic bikes differently?

## Key Insights: How Casual Riders and Annual Members Use Cyclistic Bikes Differently

**- Ride Duration:**
Casual riders have significantly longer average trip durations (42.8 minutes) compared to annual members (11.42 minutes). This suggests casual riders may use bikes for recreational purposes, while members use them for commuting or short trips.

**- Day and Time Preferences:**

Casual riders are more active on weekends, aligning with leisure activities.
Members ride consistently throughout the week, peaking during commuting hours (e.g., 5 PM).

**- Seasonal Trends:**

Both groups ride more frequently during summer (June–August), but casual riders exhibit sharper increases, likely driven by favorable weather for recreation.

**- Top Stations and Routes:**

Casual riders favor stations near tourist spots or recreational areas, while members prefer stations near transit hubs or workplaces.

**- Peak Usage Hours:**

Casual riders’ trips peak between 4 PM and 7 PM, which overlaps with members’ peak usage. However, members exhibit a sharper peak at 5 PM, likely tied to commuting patterns.

**- Recurring Behavior:**

Members exhibit consistent behavior in ride frequency and timing, indicating habitual use, while casual riders demonstrate irregular, event-driven patterns.

![images](images/21-6-recurring-behavior-png.png)


## Step 6: Act 

**Actionable Recommendations**

**1- Targeted Marketing Strategies:**

- **Recreational Appeal:** Promote membership benefits for weekend riders, such as discounts for long rides or family packages.

- **Seasonal Campaigns:** Run summer promotions emphasizing cost savings with annual memberships compared to single-use pricing.

**2- Digital Media Strategies:**

- **Geotargeted Ads:** Advertise near popular tourist locations and recreational hotspots highlighting the convenience and savings of becoming a member.

- **Social Proof:** Use testimonials or success stories of casual riders who transitioned to memberships for cost savings and added benefits.

**3- Personalized Membership Offers:**
- Offer trial memberships with incentives, such as the first month free or free weekend rides for casual riders who register during peak seasons.

- Implement referral programs where existing members receive perks for converting casual riders to members.

**4- Operational Enhancements:**

- **Weekend Promotions:** Provide discounts or promotional offers during weekends to nudge casual riders toward memberships.

- **Station Placement:** Expand stations in areas frequented by casual riders and offer exclusive member perks at those locations.

**5- Behavioral Nudges:**

- **Ride Analytics:** Show casual riders data about their total spending and potential savings as members after completing a ride.

- **Gamification:** Introduce milestones or rewards for casual riders who increase their ride frequency, linking these achievements to discounted memberships.


**Next Steps**

**1- Share Findings:**

- Present these insights and recommendations to the Cyclistic Executive Team using professional visualizations in Tableau.
- Highlight the potential ROI of converting casual riders into annual members using usage trends and financial implications.

**2- Implement A/B Testing:**

- Test different marketing messages and promotional offers to determine the most effective strategies for casual rider conversion.

**3- Monitor and Evaluate:**

- Track the impact of implemented strategies using KPIs like the conversion rate of casual riders to annual members and overall membership growth.

**Executive Summary**

The data reveals that casual riders primarily use Cyclistic bikes for recreational purposes, while annual members use them for daily commuting. To convert casual riders into members, the company should emphasize cost savings, convenience, and exclusive perks through targeted campaigns and operational adjustments. These strategies align with observed rider behavior, ensuring a higher likelihood of adoption.

By addressing these key areas, Cyclistic can capitalize on its data-driven insights to increase annual memberships, ensuring sustainable growth and success.
