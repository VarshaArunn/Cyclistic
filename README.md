# Cyclistic

## Introduction
Highlighted in this case study are the competencies acquired through the Google Data Analytics Professional Certificate Course. Leveraging these skills, I intend to proficiently execute the responsibilities of a data analyst at the hypothetical bike-share enterprise,***Cyclistic***.  Adhering to the structured data analysis framework of
**Ask, Prepare, Process, Analyze, Share,** and **Act**, I am poised to successfully address the business challenges at hand and contribute to informed decision-making within the organization.

### Scenario
Cyclistic's Director of Marketing, Lily Moreno, posits that the pivotal determinant of the company's forthcoming triumph lies in the optimization of annual memberships. Consequently, our team endeavors to gain comprehensive insights into the distinctive usage patterns of Cyclistic bikes by casual riders and annual members. Armed with these insights, we aim to formulate a novel marketing strategy aimed at transitioning casual riders into committed annual members. However, the ultimate endorsement of our proposals by Cyclistic executives hinges upon the substantiation of our recommendations through compelling data insights and sophisticated data visualizations.

### About the Company
Since its successful launch in 2016, Cyclistic has expanded its bike-share program to encompass a fleet of 5,824 geotracked bicycles distributed across 692 stations throughout Chicago. Distinguished by its user-friendly model, cyclists can unlock bikes from one station and conveniently return them to any other station within the network at their convenience.

Central to Cyclistic's appeal is its flexible pricing structure, offering single-ride passes, full-day passes, and annual memberships. Casual riders, defined as those opting for single-ride or full-day passes, coexist with Cyclistic members who commit to annual memberships. Financial analysis by Cyclistic's finance team indicates that annual members significantly contribute to the company's profitability, prompting Director of Marketing Lily Moreno to target the conversion of casual riders into members.

With a clear goal in mind, Moreno aims to devise effective marketing strategies tailored to achieve this conversion. To inform their approach, Moreno and her team are keen on delving into Cyclistic's historical bike trip data, seeking valuable insights into usage patterns and trends.
## Ask

### Business Task
Examine Cyclistic's 2022 trip data to discern the distinct usage patterns of casual riders and annual members, providing crucial insights that will inform the marketing team's strategy formulation for the upcoming campaign.

### Stakeholders

**Lily Moreno**: Director of Marketing. Moreno oversees the conception and execution of campaigns and initiatives to promote the bike-share program, encompassing various channels such as email, social media, and other platforms.

**Cyclistic marketing analytics team**: A dedicated team of data analysts is tasked with the collection, analysis, and reporting of data pivotal to shaping Cyclistic's marketing strategy.
**Cyclistic executive team**: The discerning executive team, known for their meticulous attention to detail, will make the ultimate decision regarding the approval of the proposed marketing program.

## Prepare
The initial phase of my preparatory process involves the comprehensive downloading of all requisite data for analysis. Specifically, we will procure the Cyclistic trip data for the year 2022, downloading it in 12 distinct .csv files corresponding to each month. These files will be systematically stored in a designated folder. It's important to note that the data has been graciously provided by Motivate International Inc. under this [license](https://ride.divvybikes.com/data-license-agreement). 
## Process
### Data Cleaning
#### Excel
To begin the data cleaning process, I opened each .csv file in excel and did the following
* Checked for and removed any duplicates
* Used the **trim()** function to remove unneeded spaces
* Used the **weekday()** function to create a new column labeled **day_of_week** using (1-7) to represent (Sunday-Saturday)
* Created a new column labeled **ride_length** by subtracting the **started_at** column from the **ended_at** column
* Changed the time format to **37:30:55** to make it more readable
* Removed any rides under **1 minute** or longer than **24 hours** by sorting the speadsheet.

#### SQL
Due to the substantial size of each .csv file, I opted to transition to SQL for a more efficient cleaning and analysis process. However, the sandbox mode in BigQuery imposes a file upload limit of 100MB. Given that several files exceeded this limit, I addressed the issue by establishing a Google Cloud Storage bucket, allowing me to upload the larger files and subsequently import them into BigQuery.

Upon uploading all twelve files, I amalgamated them into a singular table named **combined_data** using the **union** function in a consolidated query. Simultaneously, I excluded rows containing null values within the same query.

The outcome was a unified table containing impeccably cleaned data, ready for thorough analysis.

## Analyze
To begin the analysis phase, I wanted to reemphasize the business task ***How do casual riders and members use bikes differently?*** 

To answer this question, there were a few things that I identified that I could pull from the data. I wrote queries for the following:
* **Total # of trips per rider type**
* **Total # of trips per rider type per bike type**
* **Average ride length per rider type**
* **Total # of trips and average length of trip per rider type per month, day, and hour of day**
* **Most Popular Start and End Stations per rider type**

All SQL queries can be found [here](https://github.com/tuckertrost/Cyclistic-Case-Study/blob/main/DataAnalysis.sql)

After pulling the specified data with my queries, I noticed a few things right off the bat:
* Members had around a million more trips in 2022 than causl riders.
* Causal riders trips on average lasted around double the length of members
* The summer months had peak activity for both casual and member riders.

Now I had enough data that I could plug into tableau and create some visualzations and a dashboard.

## Share
The dashboard I created for this project can be found on tableau [here](https://public.tableau.com/app/profile/tucker.trost/viz/CyclisticCaseStudy-GoogleDataAnalysticsCertificate/CyclisticCaseStudy)

For my visualizations, I really wanted to emphasize only the data that illustrated the key differences between casual riders and members. To accomplish this, I found that a few of my queries were not crucial to anwering the business task.

I compile my dashboard, I included the following visualizations:
* **Trips per rider type**
* **Trips per Bike Type**
* **Average ride length per rider type**
* **Top Start and end stations**
* **Number of trips per month, day, and hour**

Here is a look at the dashboard

![Dashboard Screenshot](https://github.com/tuckertrost/Cyclistic-Case-Study/assets/132526212/313bb03e-d381-4a50-96d4-293f310e5de3)

Here is a summary of the key differences found between Members and Casual Riders:

**Members:**
* Members primarily use bikes for daily commutes to work, university, etc.
* Top bike stations are strategically located near colleges and office buildings downtown.
* Average ride length is shorter and consistent, indicating routine travel to familiar destinations.
* Peak months are from May to September, coinciding with favorable weather for bike usage.
* Peak activity occurs on weekdays during working and school hours, with spikes at 8 AM, 12 PM, and 5 PM.

**Casual Riders:**
* Casual riders use bikes for leisure and entertainment purposes.
* Top bike stations are located along the waterfront and near popular entertainment attractions.
* Casual riders have longer average ride lengths, using bikes for strolling and exploration.
* Peak months align with the warmer months of the year.
* Peak activity happens during weekends, with steady increases around noon, reaching the highest point at 5 PM.

**Comparison of Casual Riders and Members:**
* Casual riders use bikes for leisure, while members use them for daily commuting.
* Top station locations differ, with members favoring areas near colleges and office buildings, and casual riders near entertainment spots and waterfront.
* Average ride length varies, shorter and consistent for members, longer and more exploratory for casual riders.
* Peak months align with weather for both groups, but peak days differ - weekdays for members and weekends for casual riders.
* Activity spikes occur at different times of the day, with members commuting during work hours and casual riders using bikes mainly during leisure hours.

## Act
Based on my analysis, I came up with the following reccomendations that I believe will help the marketing team create an effective campaign to convert casual riders into members:

***1. Summer Adventure Membership:* Offer a seasonal membership for summer (May to August) tailored for casual riders, emphasizing bikes near waterfront attractions and entertainment spots.**

***2. Waterfront Wonders Promotion:* Advertise the campaign at water-adjacent bike stations popular among casual riders, showcasing the benefits of membership.**

***3. Weekend Explorer Discounts:* Provide exclusive discounts for weekends and longer rides to incentivize casual riders to become members and enjoy cost savings.**

By implementing these concise strategies, the marketing campaign can effectively convert casual riders into valued members, enriching their biking experience during the summer season.
