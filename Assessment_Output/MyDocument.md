Please read below points for Data Processig/KPI/Deployment/Triggering/Visualization

Data Processing:

1.The dataset is in csv file is having mostly string datatypes, Have cleaned and casted columns that are mostly date,int and double datatype for further processing.

2. Renamed # of Positions to No of Positions for better coulmn names.

3. Removed Job Category having Null values.

4.There isn't single "Salary" coulumn so introduced new column "Average Salary" by taking average from existing "Salary Range From" 
and "Salary Range To" columns. this newly derived Salary column would be used in KPI as well

5.Applied below 3 feature engineering techniques :

a.Extract year from "Posting date" column (Looking at the dataset it resembles that this column plays a vital role) 
b.binning "job category" in to Top 10 ( Binning is kind of transforming certain set of high-cardinality of data into categorical "bins") 
c.There is a column named "Minimum Qual Requirements" that has list of degrees,We are splitting the most valued degree with other using flag (1-bachelor,master | 0-other)

6.Removed unwanted columns - To Apply,Additional Information,Job Description,Residency Requirement,Recruitment Contact

7.Each cell in notebook display the sample output for easy reference of each dataframes

KPI:

1. Average salary per agency for last 2 years - this KPI return blank result because the latest year in the dataset is 2019.

2. Highest paid skills: For this KPI I've considered key words from the column "Preferred skills" and used UDF to extract the same for calculating highest paid skills.


Assessment Solutions:
1. I have written functions to call all data processing.
2. All KPI results are shown and visualization also displayed(we can save visulization as image if we want).

Test Cases:
Test Description	      			Expectation
Null handling in numeric fields	    No nulls remain in Salary columns
Header correction					_c0, _c1 style headers are replaced correctly
Correct salary average	            Average Salary = (Salary Range From + Salary Range To) / 2
Date conversion						All date fields are correctly parsed
Skills extraction					Only known skills are returned
KPI: Job category counts			Top 10 categories are correct by count
KPI: Salary distribution			Salary aggregation logic is valid

Deployment:
Method 1(On-Prem): 
1. Create a .py file with program code (driver.py). All main classes and program should be present.
2. Create a config file with all required configs like input path,output path,file name and spark configs.
3. Create a shell script run.sh with spark-submit command by passing the configs as parameter which will refer config file.
4. Create a folder structure like src,scripts,configs,logs.
5. Push the code and commit in GIT into Dev branch and get pull-request approval.
6. Using Jira and RLM build the code package into UAT environment.
7. Execute the code and verify in UAT and get all approvals
8. Create Prod CR and push these changes into Prod.

Method 2 (AWS or Azure Cloud): 
Batch Job Deployment (on Databricks, EMR, or similar)
1. Package your code in a .py file.
2. Set up a scheduled job via Airflow / Databricks Job Scheduler.
3. Input: Raw CSV from data lake (e.g., ADLS, S3).
Output: Cleaned data + analytics to storage or dashboard (Power BI, Tableau).

Triggering:

Method 1(On-Prem):
Autosys can be used by creating JIL files.

Method 2(AWS or Azure Cloud): 
Airflow DAG: with SparkSubmitOperator
Databricks Jobs: configured for CSV ingestion and notebook execution
Azure Data Factory pipeline: using a Databricks or EMR notebook


Visualization:
We can use Tableau or Power BI for building dashboards on busiess insights

