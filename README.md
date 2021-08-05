# Pewlett-Hackard-Analysis
HR analytics for retiring employees

## Overview and Purpose of Analysis
Pewlett-Hackard will soon have a multitude of employees retiring from the company, leaving a large amount of vacancies to be filled. In preparation for this "silver tsunami," Pewlett-Hackard has asked me to provide some analysis that will help them get ahead of the curve. The company wants to know what employees are eligible for retirement, and what titles will become vacant soon. Furthermore, a mentorship program has been initiated with the hopes of providing mentoring to incoming employees from retiring employees. With this program, the mentoring employees can stay on part time to ensure that the new hires are comfortable and successful in their role.

I started this project with six excel spreadsheets containing various information about the company's employees and departments. The first step I took towards analysis was to create an entity relationship diagram (ERD) showing how the six spreadsheets were connected (fig.1). I used this ERD throughout my analysis as guide. 

###### (Fig. 1) Employee ERD

![EmployeeDB](https://user-images.githubusercontent.com/84139177/128421192-ea46dc49-df5e-4b91-a22c-a981e5b3368a.png)

## Resources
- Data Source: departments.csv, dept_emp.csv, dept_manager.csv, employees.csv, salaries.csv, titles.csv
- Software: PostgreSQL 12.7, pgAdmin 4 5.2, Visual Studio Code 1.58

## Results

### 1. The Number of Retiring Employees by Title
I needed to find what employees were retiring and and tally the number of unique job titles that were about to become vacant. The first table I created, called "retirement_titles" (fig. 2) showed duplicates created by employees that changed positions.

###### (Fig. 2) Head of the first table for retiring employees
<img width="780" alt="retirement_titles" src="https://user-images.githubusercontent.com/84139177/128423084-5a6aad25-dc01-4fd3-91a4-d7696f5e904b.png">

The duplicates were going to cause trouble in the analysis, so I needed to remove them before I moved on. So, I created a table, named "unique_titles" (fig. 3) that showed only the most recent title of the eligible employees.

###### (Fig. 3) Head of retiring employees with their most recent title
<img width="583" alt="unique_titles" src="https://user-images.githubusercontent.com/84139177/128423442-7fec9883-8457-42d9-a423-2bac752df72d.png">

Using the unique_titles table, I could finally move onto my final product: a table showing the number count of each job title belonging to a soon-to-be retiree. My query to create "retiring_titles" (fig. 4) was:

![Count](https://user-images.githubusercontent.com/84139177/128424417-c8bf8595-5d23-4edf-b107-663655c1df57.png)

###### (Fig. 4) Count of retiring titles
<img width="250" alt="retiring_titles" src="https://user-images.githubusercontent.com/84139177/128424245-6ee38be0-4b31-4f2a-b3e9-f1cceddff563.png">

#### Major points
- There are almost 30,000 employees retiring in both the senior engineer role and the senior staff role each. This upcoming retirement season will result in large changes and it is important the company be prepared for challenges like vacancies and employee-induced data loss.
- Without removing the duplicates from the first table created, the final tally results would have been much larger. The use of "DISTINCT ON" in the query is necessary to avoid incorrect data.

### 2. The Employees Eligible for the Mentorship Program
In hopes of helping company newcomers, I created a table (fig. 5) titled "mentorship_eligibility" showing the employees that are eligible to participate in the mentorship program. My query includes employees born in 1965 only:

![Screenshot (54)](https://user-images.githubusercontent.com/84139177/128425885-a7f717b0-41a0-4f3e-abec-3535b1b188a0.png)

###### (Fig. 5) Head of employees eligible for the mentorship program
<img width="951" alt="eligible" src="https://user-images.githubusercontent.com/84139177/128426011-58d09f30-6a3b-44f9-8d9c-12656dd44872.png">

#### Major points
- There are 1550 employees listed in this table, which is only 1.7% of the total amount of employees retiring.
- The query used to create the eligibility table could be edited to include more than those born in 1965, which will increase the amount of mentors.

## Summary

#### How many roles will need to be filled as the "silver tsunami" begins to make an impact?
In total, there are 90,398 positions that need to be filled. Promoting from within could lessen those numbers at first and help with the vacancy whiplash. Using fig. 4 as an example, if the company where to promote the engineers, that would cover about half the staff of senior engineers. Still, the assistant engineers, if promoted to engineers, would only make up for about 12% of employees lost in that role, and over 1700 assistant engineers would still need to be hired. Overall, promoting from within could stop the "silver tsunami" from making a catastrophic impact on office culture but it would not resolve the issue of the large amount of vacancies.

#### Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
Currently, no, there are not enough employees for mentoring. I created a table (fig. 6) showing a count of the titles included in the table "mentorship_eligibility." 

###### (Fig. 6) Count of mentorship titles available
![Screenshot (55)](https://user-images.githubusercontent.com/84139177/128429436-b5b93fa4-fa74-448c-9420-3bb3d953930a.png)

We can see here that there are only 458 senior staffers available for mentorship out of the 28,254 total vacancies about to be created (according to fig. 4). This means that the mentorship for senior staffers alone only covers 1.6% of the incoming employees. However, by creating a new eligibility query that included more birth years (fig. 7), the company could add more employees to the mentorship program. 

###### (Fig. 7) Example of new eligibility query
![Screenshot (56)](https://user-images.githubusercontent.com/84139177/128430369-b0a2e402-58ac-4abb-b7bf-4bd215b548e0.png)
