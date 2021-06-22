# Football Coaches Salaries

## High Level Overview 

I was provided with footbal coaches data that included salary and school information. I acquired additional data such as football players graduation rates from 2006 Cohort, recorded wins from all historical played games, and stadium size capacity for each school by webscraping using Python. 
* Coaches Data: includes football coaches' salaries, bonuses, school, team, buyout, assistant pay
* Graduation Rates: obtained 2006 Cohort data from https://web3.ncaa.org/aprsearch/gsrsearch by entering search criteria and saving html to local drive for access
* Recorded Wins: obtained from Wikipedia https://en.wikipedia.org/wiki/NCAA_Division_I_FBS_football_win-loss_records
* Stadium Size: obtained from Wikipedia http://en.wikipedia.org/wiki/List_of_American_football_stadiums_by_capacity 
* Team Names: obtained list of team names as different sites had different spelling conventions from Wikipedia https://en.wikipedia.org/wiki/List_of_NCAA_Division_I_FBS_football_programs

After acquiring the supporting data and combining it with the coaches dataset, I analyzed if there were any patterns amongst the variables with a football coaches' salary. Since we were only interested in the salary not including bonuses, I only used TotalPay variable and did not consider adding in the bonus metrics. Therefore, in the regression models, I used TotalPay as the output variable when testing different sets of input variables to find the best model. 

## Project Objectives
* Build model to predict salary for football coaches
* Understand effect of graduation rate on projected salary for football coaches
* Identify single biggest impact on salary size


## Data Analysis

First, I looked at the summary statistics of the data after I had cleansed it of missing values and variables that did not add value. I converted TotalPay by dividing it into a million and Stadium Capacity by dividing it into a thousand. Below shows a summary of key numerical variables I was interested in using in my model. Overall, I have 104 records in my dataset. The range of TotalPay_Mil goes from $0.4M to $8.3M with a mean of $2.7M, which are paid to football coaches as an annual salary.
#### Summary Statistics
![image](https://user-images.githubusercontent.com/51731430/122981463-654f9400-d35f-11eb-8efb-1a26d9494d89.png)


Then, I wanted to understand how many schools were in each Conference since it was a variable of interest too. Overall, it looks like ACC, SEC, and Big Ten have the most schools participating in their conference while Ind. has the fewest number of schools participating. 
#### Number of Schools in each Conference
![image](https://user-images.githubusercontent.com/51731430/122981392-51a42d80-d35f-11eb-8640-033f99570e32.png)

Next, I used a correlation heat map and scatter plot matrix to review the relationships amongst the numerical variables. Focusing on TotalPay, it had strong relationships with Stadium Capacity and the record variables such as Win_Pct, Won, Loss, Tied, Total Games, and Years Played.  Looking at these variables, they also have some strong to decent correlations amongst each other such as Win_Pct and Win since they are variables that rely on each other. The record variables had strong correlations with each other because they are dependent on each other and derived from each other.  Out of the record variables, I decided to use Win_Pct to further analyze and dropped Won, Loss, and Tied. Looking at the scatterplot matrix, I also decided to drop Total_Games and Years_Played because the distribution of the dataset was very concentrated together with low variation.  

Therefore, in addition to Win_Pct, I also wanted to continue reviewing GSR, FGR, and Stadium Capacity, even though there were significant correlations amongst each other, in order to determine which ones were the best ones to use in modeling. 
#### Correlation Heat Map
![image](https://user-images.githubusercontent.com/51731430/122981309-3802e600-d35f-11eb-868e-495ae4bc0a58.png)

#### Scatter Plot Matrix
![image](https://user-images.githubusercontent.com/51731430/122981285-31746e80-d35f-11eb-9f5b-6d438033f0ac.png)


Next, I used boxplots to review each interested variable by Conference. TotalPay, Stadium Capacity, and Win_Pct had the most variation amongst the different Conferences. GSR and FSR had some variation but less compared to the others variables. 
#### Boxplots by Conference
###### Total Pay by Conference
![image](https://user-images.githubusercontent.com/51731430/122982479-89f83b80-d360-11eb-9916-18ac559e3044.png)
###### Stadium Capacity by Conference
![image](https://user-images.githubusercontent.com/51731430/122982373-68974f80-d360-11eb-8e98-fbcebc0014bc.png)
###### Winning Rate by Conference
![image](https://user-images.githubusercontent.com/51731430/122982422-764cd500-d360-11eb-86f5-3376c4ca345b.png)
###### Graduation Success Rate (GSR) by Conference
![image](https://user-images.githubusercontent.com/51731430/122982388-6c2ad680-d360-11eb-94a9-00502f96f635.png)
###### Federal Graduation Rate (FGR) by Conference
![image](https://user-images.githubusercontent.com/51731430/122982404-71882100-d360-11eb-9deb-177f7fd59967.png)


Then, I used 3-dimensional scatter plots to review each interested variable in relationship to TotalPay by Conference. Similarly seen in boxplots and scatter plot matrix, there seems to be more distinct positive trend with Win_Pct and TotalPay and Stadium Capacity and TotalPay amongst the different conferences. For GSR and FGR, there are a few conferences that show a more distinct relationship with Total Pay such as Pac-12 conference but very few. 
###### Stadium Capacity by Conference
![image](https://user-images.githubusercontent.com/51731430/122982584-a85e3700-d360-11eb-8884-ff3da84ed7f3.png)
###### Winning Rate by Conference
![image](https://user-images.githubusercontent.com/51731430/122982726-d6437b80-d360-11eb-962c-5060df743cbb.png)
###### Federal Graduation Rate (FGR) by Conference
![image](https://user-images.githubusercontent.com/51731430/122982742-dc395c80-d360-11eb-9b73-c0be044ecd83.png)
###### Graduation Success Rate (GSR) by Conference
![image](https://user-images.githubusercontent.com/51731430/122982816-f115f000-d360-11eb-9866-7c0094c89983.png)


## Regression Models
Below are the different regression models I ran using the output variable as Total Pay and different variations of the key variables I was interested in as the input variables Conference, Stadium Capacity, Win_Pct, GSR, and FGR. The two best models were Model 4 and Model 5 since they had variables with significant p-values and no multicollinearity.  I decided that the best model between these two were Model 5 Conference + Win_Pct at Adjusted R square of 0.734. 
###### Regressions Performance Summary
![image](https://user-images.githubusercontent.com/51731430/122990931-178c5900-d36a-11eb-80af-2c80111872eb.png)
###### Model 5 Regression Summary
![image](https://user-images.githubusercontent.com/51731430/122990979-2115c100-d36a-11eb-97db-5fafabc6bf76.png)

## Questions Answered

What is the recommended salary for the Syracuse football coach? 
* Based on Model 5, recommended salary for the Syracuse football coach would be $3.495M. 

What would his salary be if we were still in the Big East? 
* I would not be able to determine the salary of Big East with this model because they were not considered in the dataset. I would need to incorporate schools from the Big East in the dataset and re-run the model to recommend a salary. 

What if we went to the Big Ten? 
* Using the average Win_Pct for Big Ten in the model, the recommended salary would be $4.441M if they went to the Big Ten. 

What schools did we drop from our data, and why? 
* Below lists the school I dropped and the reasons why, which was mostly due to no data available from stadium, graduation, and total pay. 
 ![image](https://user-images.githubusercontent.com/51731430/122993175-9f736280-d36c-11eb-8f85-479bdec69fd7.png)
 
What effect does graduation rate have on the projected salary? 
* In Model 5, I didn’t include either of the graduation rates because their p-values were greater than my threshold of 0.10 as seen in Model 6 and Model 7. Regardless, in both of the models, the GSR and FGR graduation rates had a small impact to projected salary compared to the other variables based on their coefficients. GSR in Model 6 had coefficient of 0.0068, and FGR in Model 7 had a coefficient of 0.0145. This means the max GSR could have on salary is $6800 assuming GSR is 100%, and the max FGR could have on salary is $14500 assuming FGR is 100%, which are considered a small impact considering the magnitude of the salaries. 

How good is our model? 
* Model 5 has an Adjusted R square of 0.734, which is good because our model can account for about 73.4% of the variation in our dataset. In addition, Win_Pct has a low p-value and therefore significant. 

What is the single biggest impact on salary size?
* Conference was the single biggest impact on salary size. I ran the model with only Conference (Model 6), and it had an Adjusted R square of 0.616, which accounts for most of the R-Square we had in Model 5 the final model with Win_Pct added.
















