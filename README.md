# [Project 1 - Creating 2023 NFL Draft Rookie Grades Based on Measurables ](https://github.com/EvanWhittaker97/2023_NFL_Draft)

**Tools Used**
1. Python (pandas, numpy, scipy.stats)
2. Power BI

**Cleaning/Manipulation Code:**

[Repository](https://github.com/EvanWhittaker97/2023_NFL_Draft/blob/main/Data_Manipulation_Cleaning)

**Project Scope**

The goal of this project was to analyze the athleticism of NFL rookies in this upcoming 2023 draft. 

To accomplish this, I started by gathering data for different positions such as DL, EDGE, LB, OL, QB, RB, S, TE, and WR, and stored them in CSV files. Then, I used the Pandas library in Python to read the data from each CSV file into a DataFrame.

There wasn't a lot to clean in this data. However, I removed the players who didn't test in 3 or more of the athletic testing fields so an accurate grade could be determined. Furthermore, I wanted the height field to be something easier to quantify, so I converted the height from inches to feet. 

Next, I calculated the percentiles for each player's performance in the athletic tests, such as the 40-yard dash, vertical jump, and cone drill. The challenge was creating percentile grades by position. It was imperitive that I only compare apples to apples. For example, it wouldn't be fair to compare speed of a WR to the speed ot an OL. 

I then combined each position's CSV into one and loaded it into Power BI.

The Power BI dashboard was designed to be both appealing and interative. The goal was to create a dashboard that someone with no football knowledge could look at and understand exactly how athletic the prospect was. The user has the ability to filter players by position then select the specific player they want to see metrics and the final grade for. 

**Dashboard**

![](![image](https://user-images.githubusercontent.com/64989275/233793630-6ed77b3b-2f26-400d-b570-a6811a6aaa08.png))
