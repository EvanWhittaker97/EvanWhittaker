# [AWS EC2 Lifecycle Manager](https://github.com/EvanWhittaker97/AWS_Lifecycle_Manager)

**Tools Used**:
1. AWS
2. Python
3. JSON

**Project Scope:**

The scope of the AWS Lifecycle Manager project was to save my employer money on EC2 instances. In our use case, the VM's were being used to migrate data from legacy software to our software. Each VM was being used for one client only.

The challenge with this approach is that we incurred significant data storage costs. Furthermore, we were previously using Terraform - but if Terraform and EC2 (front end) didn't agree, all of the changes made in the front end would be overwritten the next time a commit was made. Not to mention we could not approve our own pull requests, so it wasn't incredibly efficient. 

**Process:**

1. Create tags for each instance that Lifecycle Manager could run on. For our environment, I used "DaysRemaining" (days until VM has a snapshot taken) and "ConversionComplete" (if the data has been migrated, change the value)
   
2. Implement the Lifecycle Manager Snapshot policy
   
   ![](https://raw.githubusercontent.com/EvanWhittaker97/AWS_Lifecycle_Manager/refs/heads/main/lifecycle.png)
   
3. Create an [IAM Role](https://github.com/EvanWhittaker97/AWS_Lifecycle_Manager/blob/main/IAM.txt) (JSON) that allows Lifecycle Manager and LAMBDA to create, delete and modify instances as well as log whenever they run
   
   ![](https://raw.githubusercontent.com/EvanWhittaker97/AWS_Lifecycle_Manager/refs/heads/main/log.png)
   
4. Develop a [LAMBDA script](https://github.com/EvanWhittaker97/AWS_Lifecycle_Manager/blob/main/TagAllVMs.txt) (Python) that applies the new tags to existing instances based on the associated volumes' creation date (ie. if older than specific date, DaysRemaining = 5, ConversionComplete = y)
   
5. Develop a [LAMBDA script](https://github.com/EvanWhittaker97/AWS_Lifecycle_Manager/blob/main/decrementDaysRemaining.txt) (Python) that decrement our DaysRemaining tag by 1 every 24 hours, but only where ConversionComplete = y
   
6. Develop a [LAMBDA script](https://github.com/EvanWhittaker97/AWS_Lifecycle_Manager/blob/main/deleteInstancesAfterSnapshot.txt) (Python) that deletes instances when DaysRemaining tag = -1
    
7. Use Amazon EventBridge to create a schedule for the decrementDaysRemaining and DeleteInstancesAfterSnapshot to run on that compliments the Lifecycle Manager schedule
   
   ![](https://raw.githubusercontent.com/EvanWhittaker97/AWS_Lifecycle_Manager/refs/heads/main/eventbridge.png)

**Challenges:**
- Ensuring that the order of operations was correct (decrementDays runs first, Lifecycle Manager runs second and deleteInstances runs third)
- Did not consider that these scripts would be running on every existing instance when allocating RAM for the initial snapshot purge
- Creating a new methodology for bulk creation of instances (solution was a PowerShell script that created instances based on an array of names)

**Results:**

- Cloud costs were reduced by over 50% for the team
- No longer dependant on another team member to approve pull requests
- Risk of manually deleting the incorrect instance became nearly non-existent
- Customer data was now accessible for 2 years (per Lifecycle policy) by simply restoring an instance from the snapshot 


# [US Super Store Sales Dashboard](https://github.com/EvanWhittaker97/SuperStore_Dashboard)

**Tools Used**:
1. Power BI
2. DAX Query
3. Power Query

**Power BI File Download:**

[Download](https://github.com/EvanWhittaker97/SuperStore_Dashboard/blob/main/dashboard.pbix)

**Project Scope:**

The scope of the US Super Store Dashboard project was to highlight the capabilities of Power BI. By harnessing this powerful, user-friendly tool, a dashboard was developed to effectively monitor sales metrics.

The first sheet of the dashboard emphasizes current metrics. It visualizes crucial figures such as Year-over-Year (YoY) Monthly Profit, Monthly Sales, and the distribution of Payment Methods. Moreover, it includes an interactive map with proportionally sized bubbles, displaying sales by each state. Hovering over any particular bubble reveals the name of the state, alongside the total sales and profit figures.

The second sheet leverages the robust forecasting capabilities inherent to Power BI. This sheet features two line charts, each projecting a forecast for the next 30 days of sales. To enable precise analysis, sliders have been incorporated with each line chart. This feature allows end-users to narrow their focus to specific date ranges, as and when further analysis is required.

Dashboards:

![](https://raw.githubusercontent.com/EvanWhittaker97/SuperStore_Dashboard/main/Dashboard_1.png)
![](https://raw.githubusercontent.com/EvanWhittaker97/SuperStore_Dashboard/main/Dashboard_2.png)

# [Credit Card Clustering Analysis](https://github.com/EvanWhittaker97/credit_card)

**Tools Used**
1. R
2. Excel

**Clustering Algorithm Code:**

[Repository](https://github.com/EvanWhittaker97/credit_card/blob/main/github_code.r)

**Data Source:**

https://www.kaggle.com/datasets/arjunbhasin2013/ccdata

**Project Scope:**

The scope of this project was to perform a k-means clustering algorithm on the credit card data set to reveal trends in the data. The focus was specifically on conducting exploratory data analysis, customer segmentation and potentially reveal cardholder behavior. I removed the upper/lower 1% of the data to ensure outliers were managed. 

**K-Means Output:**

First, I determined the optimal number of clusters using the elbow method. As you can see below, the elbow indicated that 4 clusters appeard to be the most optimal number:

![](https://raw.githubusercontent.com/EvanWhittaker97/credit_card/main/elbow_plot.png)

Then, after writing the k-means algorithm code, it unveiled the following clusters:

![](https://raw.githubusercontent.com/EvanWhittaker97/credit_card/main/clusters.png)

Once the clusters were determined, I added them back to the original dataset so I could conduct some basic exploratory analysis using Excel to demonstrate the power of clustering:

![](https://raw.githubusercontent.com/EvanWhittaker97/credit_card/main/Average_Cash_Advance_Frequency.png)
![](https://raw.githubusercontent.com/EvanWhittaker97/credit_card/main/average_balance.png)
![](https://raw.githubusercontent.com/EvanWhittaker97/credit_card/main/average_tenure.png)

As you can see, it appears that the 3rd cluster has some concerning findings. The cardholders in the 3rd cluster have the highest frequency of cash advances by a significant margin. If there's one important thing to know, cash advances are detrimental to your credit!

Given this finding, I decided to look into the average balance outstanding for each cluster. Unsurprisingly, the 3rd cluster has the largest outstanding balance on their cards by nearly $1000.00. Finally, I wanted to determine the loyalty of these cardholders. 

Often times, cardholders with these financial habits won't spend a ton of time with a single provider. I decided to visualize the average tenure by cluster. Although the 3rd cluster did have the shortest tenure with the card provider, it appears that the tenure wasn't short enough for the findings to be conclusive. Nontheless, further exploratory data analysis on the 3rd cluster would certainly shed light on their lacklustre creditworthiness. 

# [Creating 2023 NFL Draft Rookie Grades Based on Measurables ](https://github.com/EvanWhittaker97/2023_NFL_Draft)

**Tools Used**
1. Python
2. Power BI
3. Power Query

**Cleaning/Manipulation Code:**

[Repository](https://github.com/EvanWhittaker97/2023_NFL_Draft/blob/main/Data_Manipulation_Cleaning)

**Project Scope**

The goal of this project was to analyze the athleticism of NFL rookies in this upcoming 2023 draft. 

To accomplish this, I started by gathering data for different positions such as DL, EDGE, LB, OL, QB, RB, S, TE, and WR, and stored them in CSV files. Then, I used the Pandas library in Python to read the data from each CSV file into a DataFrame.

There wasn't a lot to clean in this data. However, I removed the players who didn't test in 3 or more of the athletic testing fields so an accurate grade could be determined. Furthermore, I wanted the height field to be something easier to quantify, so I converted the height from inches to feet. 

Next, I calculated the percentiles for each player's performance in the athletic tests, such as the 40-yard dash, vertical jump, and cone drill. The challenge was creating percentile grades by position. It was imperitive that I only compare apples to apples. For example, it wouldn't be fair to compare speed of a WR to the speed to an OL. 

I then combined each position's CSV into one and loaded it into Power BI.

The Power BI dashboard was designed to be both appealing and interative. The goal was to create a dashboard that someone with no football knowledge could look at and understand exactly how athletic the prospect was. The user has the ability to filter players by position then select the specific player they want to see metrics and the final grade for. 

**Dashboard**

![](https://raw.githubusercontent.com/EvanWhittaker97/2023_NFL_Draft/main/player_profile.png)
