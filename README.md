# Analytics Vidhya -JOB-A-THON-NOV-2021

**RANK:** 86

**SCORE:** 0.6922596859

**PROBLEM STATEMENT:**
In recent years, attention has increasingly been paid to human resources (HR), since worker quality and skills represent a growth factor and a real competitive advantage for companies. After proving its mettle in sales and marketing, artificial intelligence is also becoming central to employee-related decisions within HR management. Organizational growth largely depends on staff retention. Losing employees frequently impacts the morale of the organization and hiring new employees is more expensive than retaining existing ones.

You are working as a data scientist with HR Department of a large insurance company focused on sales team attrition. Insurance sales teams help insurance companies generate new business by contacting potential customers and selling one or more types of insurance. The department generally sees high attrition and thus staffing becomes a crucial aspect.

To aid staffing, you are provided with the monthly information for a segment of employees for 2016 and 2017 and tasked to predict whether a current employee will be leaving the organization in the upcoming two quarters (01 Jan 2018 - 01 July 2018) or not, given:

Demographics of the employee (city, age, gender etc.)
Tenure information (joining date, Last Date)
Historical data regarding the performance of the employee (Quarterly rating, Monthly business acquired, designation, salary)
Acknowledgements:
https://datahack.analyticsvidhya.com/contest/job-a-thon-november-2021/

**Data Dictionary:**
**Train Data**
MMMM-YY - Reporting Date (Monthly)
Emp_ID - Unique id for employees
Age - Age of the employee
Gender - Gender of the employee
City - City Code of the employee
Education_Level - Education level : Bachelor, Master or College
Salary - Salary of the employee
Dateofjoining - Joining date for the employee
LastWorkingDate - Last date of working for the employee
Joining Designation - Designation of the employee at the time of joining
Designation - Designation of the employee at the time of reporting
TotalBusinessValue - The total business value acquired by the employee in a month (negative business indicates cancellation/refund of sold insurance policies)
Quarterly Rating - Quarterly rating of the employee: 1,2,3,4 (higher is better)

**Test Data**
Emp_ID - Unique Id for the employees

**Evaluation Metric:**
The evaluation metric for this competition is macro f1_score.

**APPROACH:**
I have approached this problem as a classification problem. We had to predict whether
an employee will leave the organization in the next 2 quarters. In the dataset, there were
multiple records for each employee for each reporting month. I first focused on creating
unique records for each employee and calculating the target variable (attrition in 2
quarters) by using the joining date and last working day columns.
Once the feature engineering part was done, I built a classification model to reach the
final output.

As I mentioned, it was important to create a unique record for each employee.
I took the latest record for each column for each employee except the total business
value. The total business value was aggregated for each employee by calculating the
mean business values for all months.
The joining designation column was used in conjunction with the designation column. I
calculated the difference between the 2 columns to show the number of promotions for
that employee and used that column for building the model.
For calculating the target variable, I took the difference between the last working date
and joining date in days. For the employees who left the organization before 220
days(took a buffer of 40 days), were labelled as 1 and the rest were labelled 0.
Finally encoding was done for categorical variables using the get_dummies function in
pandas.

I applied the Random Forest Classifier algorithm as Random Forest can be used to
handle large datasets as well and provides good accuracy on cross validation.
I divided the train dataset into train and test in 70:30 ratio and applied the model. The
accuracy score and F1 score obtained were 78% and 73% respectively.
To further enhance the model, I did Hyperparameter Tuning by using the Random
Search CV provided by scikit learn and estimated optimal ranges of parameters for the
Random Forest Model. After applying the model this time, the score and F1 score were
improved to 80% and 76% respectively.

