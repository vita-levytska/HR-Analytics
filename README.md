# HR-Analytics Project


# The Problem

This project aims to examine the possible causes of employee attrition based on available data.  
Attrition of employees can lead to increase of costs, lack of knowledgeable employees, increase in resources for training and hiring new employees.  
Identifying possible causes of attrition can help pinpoint the employees who are more likely to resign.  

# Data
 
The data used for this project is from Kaggle. More information about the dataset can be found [here](https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset)

## Variable Descriptions

- **Age**: numerical	  
- **Attrition**: (response) Yes/No, categorical	  
- **BusinessTravel**: nominal, levels: 'Travel_Rarely', 'Travel_Frequently', 'Non-Travel'   
- **DailyRate**: numerical  
- **Department**: nominal, levels: 'Sales', 'Research & Development', 'Human Resources'  
- **DistanceFromHome**: numerical	  
- **Education**: ordinal, levels: 1 'Below College', 2 'College', 3 'Bachelor', 4 'Master', 5 'Doctor' (encoded as numbers 1-5)  
- **EducationField**: nominal, levels: 'Life Sciences', 'Other', 'Medical', 'Marketing', 'Technical Degree', 'Human Resources'	  
- **EmployeeCount**: number of employyes corresponding to employee number (it is 1 for each observation)  
- **EmployeeNumber**: unique employee identification, numerical  
- **EnvironmentSatisfaction**: ordinal, levels: 1 'Low', 2 'Medium', 3 'High', 4 'Very High' (encoded as numbers 1-4)  
- **Gender**: nominal, levels: Male, Female	  
- **HourlyRate**: numerical	  
- **JobInvolvement**: ordinal, levels: 1 'Low', 2 'Medium', 3 'High', 4 'Very High' (encoded as numbers 1-4)  
- **JobLevel**: ordinal, levels: 1, 2, 3, 4, 5	  
- **JobRole**: nominal, 'Sales Executive', 'Research Scientist', 'Laboratory Technician', 'Manufacturing Director', 'Healthcare Representative', 'Manager', 'Sales Representative', 'Research Director', 'Human Resources'	  
- **JobSatisfaction**: ordinal, levels: 1 'Low', 2 'Medium', 3 'High', 4 'Very High' (encoded as numbers 1-4)	  
- **MaritalStatus**: nominal, levels: 'Single', 'Married', 'Divorced'	  
- **MonthlyIncome**: numerical	  
- **MonthlyRate**: numerical  
- **NumCompaniesWorked**: numerical	  
- **Over18**: categorical, Yes/No (however, all employees were over 18)	  
- **OverTime**: categorical, Yes/No  
- **PercentSalaryHike**: numerical	  
- **PerformanceRating**: ordinal, levels: 1 'Low', 2 'Good', 3 'Excellent', 4 'Outstanding' (encoded as numbers 1-4)	 
- **RelationshipSatisfaction**: ordinal, levels: 1 'Low', 2 'Medium', 3 'High', 4 'Very High' (encoded as numbers 1-4)	 	
- **StandardHours**: numerical (80 hours for each employee)	  
- **StockOptionLevel**: ordinal, levels: 0-3	  
- **TotalWorkingYears**: numerical	  
- **TrainingTimesLastYear**: numerical		  
- **WorkLifeBalance**: ordinal, levels: 1 'Bad', 2 'Good', 3 'Better', 4 'Best' (encoded as numbers 1-4)	  
- **YearsAtCompany**: numerical		  
- **YearsInCurrentRole**: numerical		  
- **YearsSinceLastPromotion**: numerical		
- **YearsWithCurrManager**: numerical	  

# Exploratory Data Analysis

Exploratory Data Analysis can be found here: [HR-Analytics-EDA](https://github.com/vita-levytska/HR-Analytics/blob/main/HR-Analytics-Models.ipynb)   

First, the basic EDA was performed by getting data types, summary, checking for missing value, duplicates and checking if the dataset was balanced.   
Then EDA was divided into 4 parts:   

**1. Exploring Gender differences (EDA1)**      

This part of analysis aims to discover the gender differences for attrition. 
![EDA1](https://github.com/vita-levytska/HR-Analytics/blob/main/Visualizations/eda1_overtime.jpeg)

For those employees that left, overtime is independent of gender, and more employees that left did overtime, than those who stayed in the company. 

**2. Exploring Education Field differences (EDA2)**

This part aims to dicover some differences pertaining to  different fields to help us better understand the dynamics of attrition in each field represented here.    
![EDA2](https://github.com/vita-levytska/HR-Analytics/blob/main/Visualizations/eda2_years_curr_manager.jpeg)

We see a similar trend among all Education Fields, employees left after either 2 or 7 years with current manager.

**3. Salary differences (EDA3)**

In this part we examine how much salary influenced attrition of employees and what other factors together with salary influence attrition. 
![EDA3](https://github.com/vita-levytska/HR-Analytics/blob/main/Visualizations/eda3_education.jpeg)

Employees that have education level below college or Doctorate degrees left the company while having the same  or higher salary than the employees that did not quit their job. Those with college, bachelor or master degrees left their job while having the same or lower salary than those who did not leave their job. 

**4. Job Level differences (EDA4)**   

In this part we look at different job levels more in depths in how they influence attrition along with other factors.    
![EDA4](https://github.com/vita-levytska/HR-Analytics/blob/main/Visualizations/eda4_job_satisfaction.jpeg)

- At Job Levels 1 and 5: the employees who left had lower levels of satisfaction than those who stayed
- At Job Levels 2 and 4: most employees who left had high level of satisfaction, while those who stayed had high/very high levels of satisfaction
- At Job Level 3: employees that left has either low or very high levels of satisfaction, while those who stayed had mostly high/very high levels of job satisfaction

At the end correlation plots are presented to show differences in correlation for employees who stayed in the company vs those who left.    
![Corr](https://github.com/vita-levytska/HR-Analytics/blob/main/Visualizations/corr_plot.jpeg)

Comparing the correlations for employees who left the company and those who stayed we see that:
- Monthly income has higher correlations with all variables but Total Working Years for employees that left, than for those who stayed
- Years at Company has higher correlation with total working years for those who quit their job
- Years at Company and Years with Current manager have almost the same correlation for both those who quit their job and those that did not
- Years since Last Promotion has higher correlation with all the variables for those who quit than for those who did not


# Model Tuning and Testing

Since the response is binary, logistic regression was chosen as binary model. Next, the following models were trained:
- Ridge Regression
- SVM
- Random Forest
- Gradient Boosting

To measure and compare the performance of our models we will use **Recall** because we want to measure how many of employees that quit their job we labeled correctly. If we can identify the employees that are going to leave the company potentially, we can target them with specific programs or trainings to prevent their attrition. The costs of targeting the employees who may potentially leave (even if they are not going to) is lower than looking for a new employee and train them if we fail to identify those at risk of attrition.   

After performing hyperparameter tuning, SVM had the highest recall value, thus it is our best model. 

Below are the precision-recall curves

![EDA4](https://github.com/vita-levytska/HR-Analytics/blob/main/Visualizations/pr_curve.jpeg)


# Limitations and Discussion

After examining the data, we see that 31.6 % and 41.2 % are medical and life sciences education field respectively, which make up the majority (72.8 %) of our employees. Also highest percentage of employees (65.4%) is in research and development. Thus more data is needed to be able to accurately predict employee attrition in different industries and education fields.     

There are internal and external causes of attrition, but the scope of this analysis is limited to internal causes only (based on available data).    

