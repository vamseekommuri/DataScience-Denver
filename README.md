				 
Problem Statement:  

	Web scrapping recent Data Scientist jobs for major cities in USA from Indeed.com using python request library and find the top skills/tools used for Data Scientist Job. Predict the salary of the job based on the keywords in the Description, summary, JobTitle, Location using NLP techniques & logistic regression


Source of Data: 

	We have web scrapped recent Data Scientist jobs for major cities in USA from Indeed.com using python request library. The following cities are captured are show in screenshot 
 
Sample Reference,Austin Job link: https://www.indeed.com/jobs?q=data+scientist&l=Austin&start=10

	We collected following fields from the Job links up-to 200 pages of various cities,
	
	JobTitle: Role of the job as per requirement, Example: senior Data Scientist
	
	Location: Location of the job to work from, Example: Colorado,CO
		Splits the data to two columns: City, state
	
	CompanyName: Name of the company posted job, Example: Apple
	
	Summary: Highlights of the job description
	
	Description: Job detailed description of each job posted

	Once the data had been collected, we saved it as pickle file and also as CSV file as part of the project process, so it is easier to read the data for processing than to scrap it every time that was time consuming. This helped us to quickly fetch the data for further analysis as scrapping several pages of data took us couple of hours.
	 we were able to approximately scrap more than 2200 records based on criteria and it helped us to provide insight on the jobs.
 

Converting dtypes:

	   Using salary column we created two attributes salary_mean ,salary_median and that process we converted the type to float using astype which is useful for categorizing the data based on salary_median value
   
Missing Data and Data Cleanup: 

	Before analysis on the data, we wanted to the data to be clean and no outliers.

	EmptyStrings:
		We had placed field values with ‘empty string’ that was outliers about the data that there are no null values in all the columns. We had replaced empty value to np.nan
 
	Location:  Drop the location places with null values as no other fields have that value and it’s a small subset we can ignore 
 
	State: After the split of location to city and state we had received the state column with null values. We derived the state value from city with map dictionary 
	 

	CompanyName: We had only row of CompanyName was null so we read from the description and fixed the value 
	 
	Description:
		   Description had lot of special characters and null values, we had removed the special character(‘\n’) and replaced the np.nan values with ‘not Available’ since the subset of missing was low compared to the whole dataframe size

 


New attributes created:

	Salary_mean, salary_type:  Not all Jobs had salary value mentioned (2030 null values). Values exist also have different types like per year, hour, week, month, day
	We had a major chunk of data level fixing to achieve the following and to get it to right format:
	•	Splitting the range of salary values,
	•	finding the average salary, 
	•	converting the salary yearly/hourly/weekly/monthly/daily 

 

	salary_above_median:	 Creating categorical value based on the median of salary value of entire salaryJobData set 
 


Model Building:
	  Using NLP techniques, we had read the key columns from the job dataframe and identified the keywords determining whether a salary is above or below the 		median value 
	Please find the snippet of the keywords based on JobTitle 
 
	we had identified similarly five such binary variables to determine the salary is above or below median and those are "JobTitle", "City", 'state', "Summary", "Description" and create categorical variables based on the above binary variables
	 
    
	Based on the above we had calculated the accuracy of 63% and cross-validated scores of the model comparing the data with salary_above_median column (where the median value was given 1 and 0 based on the mean of the 179 rows of the data ,i.e 115k)
	 
	Using the above model we had conducted the similar process of 5 binary variables on the salary data with null values 

 

Predict the data salary_median_predict based on the above data and logisticRegerssion.predict and plot the data 
 
	Future Analysis enhancement options:
	   We could have contacted the indeed data with linkedin.com & glasddoor.com and create superset of it without duplicates and create an UI page with inputs of job role interested and not just predict only for ‘Data Scientist’ and many other roles.
	   Prediction of salary would have been improved with better binary variables if we had more salary data available unlike just 179 rows out of 2200 rows. 

Conclusion: 

	Based on the prediction graph we see the no of job posting with above median salary range are in Texas state compared to all other state. This dataset had only 179 rows of salary field filled data after scrapping 2500 pages. 



![image](https://user-images.githubusercontent.com/72536274/121137852-f82ef100-c7eb-11eb-9b05-a3ee34bde96b.png)
