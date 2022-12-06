ASSIGNMENT-3
TOPIC: USA SALARY INDICATOR
Conceptual diagram:
 
Objective: 
•	Help individuals achieve the optimal job and location.
•	Users would be able to choose variables such as age, sex, and profession.
•	It accounts for salaries, and savings (net_pay).
•	Additional features include taxes on various occupations in different states.


2) 
•	We scrapped the data from bls website for USA and downloaded it into the csv file. 
•	For persons table, we downloaded the data from Kaggle as it contains person_id, age, gender, account_no, etc so there was no real time data but the persons data was already available on Kaggle so we downloaded the csv file. For savings account table we retrieved the data from Kaggle.
•	For taxes table we downloaded and reformatted the data from BLS website. 
Scrappig screenshots:
![image](https://user-images.githubusercontent.com/67430896/205785975-f4f114f5-e9df-45a8-974a-1acf42e7740c.png)
![image](https://user-images.githubusercontent.com/67430896/205786029-58e5669f-4fb7-48eb-bd3c-00da78162a26.png)
![image](https://user-images.githubusercontent.com/67430896/205786082-67e8e88b-19c2-4ba1-abe3-6f53bb9a9b0a.png)
![image](https://user-images.githubusercontent.com/67430896/205786107-037b9f81-9d91-49f9-bba1-94c3e83b0c73.png)
![image](https://user-images.githubusercontent.com/67430896/205786134-ae88f9cd-7c99-40ef-84e7-826941b3693d.png)

Cleaning screenshots: The scripts to clean the data are in the screenshots.
![image](https://user-images.githubusercontent.com/67430896/205786234-ab30443d-fa4f-4f07-9da6-29a315fcce09.png)
![image](https://user-images.githubusercontent.com/67430896/205786256-5b518708-e491-4f4f-93d7-1e57193cdaa7.png)
![image](https://user-images.githubusercontent.com/67430896/205786266-1e481ff6-f054-4e85-ae53-5b1f47971efe.png)
![image](https://user-images.githubusercontent.com/67430896/205786293-61bec8c8-ae01-4c31-beb4-7aead4de4ea5.png)
![image](https://user-images.githubusercontent.com/67430896/205786335-88677014-3cc5-4ce2-8f83-845638b19526.png)
![image](https://user-images.githubusercontent.com/67430896/205786359-8caa904c-b866-44c5-81de-485452c90dc3.png)
![image](https://user-images.githubusercontent.com/67430896/205786376-d44d616e-c11a-4427-9dc8-2351ddc6bd2d.png)
![image](https://user-images.githubusercontent.com/67430896/205786388-2319b227-9a03-4125-ae08-b023e9f47f59.png)
![image](https://user-images.githubusercontent.com/67430896/205786403-5e801051-afe7-4fc0-97c4-17665b5c4918.png)

Cleaning of person table:
![image](https://user-images.githubusercontent.com/67430896/205786476-292e6e31-33e2-4154-9e31-dce523c423a7.png)
![image](https://user-images.githubusercontent.com/67430896/205786518-e628da8d-58ef-4ae9-a3cc-7fb8d9e1edf4.png)
![image](https://user-images.githubusercontent.com/67430896/205786550-9cd0ec43-fdae-4e1f-9cef-dcd6148404c8.png)
![image](https://user-images.githubusercontent.com/67430896/205786563-866528e9-941e-445e-adb8-a47c4accb3e3.png)
![image](https://user-images.githubusercontent.com/67430896/205786599-44b912bf-2b77-48ba-95f1-e0dcb97cb2b4.png)
![image](https://user-images.githubusercontent.com/67430896/205786613-e19eb454-aa23-44c0-addf-94ccd8a4d59b.png)
![image](https://user-images.githubusercontent.com/67430896/205786643-47003ceb-c787-4e48-8c09-d0d7ae0251c5.png)
![image](https://user-images.githubusercontent.com/67430896/205786657-d35b39a8-433b-4613-a944-2d9b08e0bb49.png)
![image](https://user-images.githubusercontent.com/67430896/205786683-7501b543-2e9f-48fd-8841-ee3833595c27.png)
![image](https://user-images.githubusercontent.com/67430896/205786722-b12005db-01e5-408e-9b11-28bf2a91aa3c.png)

CREATE TABLE person(
person_id bigint ,
name text,
age double,
gender text,
 job_id text,
 account_id text,
 PRIMARY KEY (person_id));

CREATE TABLE job(
job_id int,
job_title text,
emloyement_num text,
employement_per_1000_jobs double,
median_hourly_wage text,
mean_hourly_wage text,
annual_mean_wage text,
job_location VARCHAR(255),
tax_id int,
PRIMARY KEY (job_id)
);



CREATE table taxes(
tax_id int,
location text,
tax_rate text, 

PRIMARY KEY (tax_id)
);




CREATE table savings(
account_no varchar(255), 
savings_amount varchar(255),
PRIMARY KEY (account_no));


Adding foreign key:
ALTER TABLE job
ADD CONSTRAINT fk_job FOREIGN KEY (tax_id)
REFERENCES taxes(tax_id);



ALTER TABLE person
ADD CONSTRAINT fk_person1 FOREIGN KEY (job_id)
REFERENCES job(job_id);

ALTER TABLE person
ADD CONSTRAINT fk4_Person FOREIGN KEY (account_no)
REFERENCES savings_account(account_no);


INSERT INTO :

INSERT INTO person
Values(1000, ‘pramita’, ‘22’, ‘F’, 1000, “A00099”)




USE CASES (NEW 5 PER PERSON)
Use-cases

1.	View the locations that have an average Salary of $50,000 along with name and gender.
SELECT j.job_location, P.name, P.gender, j.avg_salary 
FROM Person P
JOIN Job J
ON P.job_id = j.job_id
WHERE 
j.avg_salary > 50000;

2.	SQL query to find the count of the total occurrences of a particular character – ‘A’ in the Name field and the mean hourly wage.

SELECT j.mean_hourly_wage, P.name
FROM Person P
      JOIN Job J ON P.job_id = j.job_id
WHERE LENGTH(P.name) - LENGTH(REPLACE(P.name, 'A', ''));

3.	SQL query to find the tax rate of each job 
  SELECT J.job_name, T.tax_rate FROM jobs J
      INNER JOIN Taxes T
      ON J.tax_id=T.tax_id
      GROUP BY j.job_name;

4.	SQL Query to find the number of females, name, and savings amount.
SELECT P.name, Count(*), s.savings_amount FROM Person P
JOIN savings_account S
ON P.account_no=S.account_no
WHERE P.gender = ‘Female’;

5.	Display the males where the median hourly wage is NULL.
SELECT J.median_hourly_wage, P.name FROM Jobs J
JOIN Person P
ON P.job_id=J.job_id
WHERE P.gender = ‘male;

6.	SQL Query display all rows from both tables, populating the columns with table value. 
SELECT *
FROM Person
FULL OUTER JOIN Jobs
   ON Jobs.job_id = Person.job_id
ORDER BY Person.name ASC;

7.	SQL Query display all the information whose name start with C and location is either Arizona or Boston. 
   
SELECT Count(*), P.name FROM Person P
JOIN Jobs J
ON P.job_id=J.job_id
WHERE P.name LIKE ‘C%’and J.job_location IN (‘Arizona’ OR Boston’);

8.	SQL Query display all the name and the job name whose tax amount is greater than 1500.
SELECT P.name, J.job_name, T.tax_amount FROM Jobs J
JOIN Person P 
ON P.job_id=J.job_id
JOIN Taxes T
ON J.tax_id=T.tax_id WHERE T.tax_rate > 1500;
9.	Display the Job names and age of the entities who has the least savings amount. 
SELECT P.age, J.job_name, MIN(S.savings_amount) 
FROM Person P 
JOIN Job J 
ON  P.job_id = J.job_id
JOIN Savings_account S 
ON P.account_no = S.account_no;


10.	View the entity who has the highest tax rate.
SELECT COUNT(job_id), MAX(T.tax_rate)
FROM Jobs J 
JOIN Taxes T
ON T.tax_id = J.tax_id;

11.	Which age group has savings more than 1000. 

SELECT P.age, MAX(S.savings_amount)
FROM Person P 
JOIN Savings_account S 
ON P.account_no = S.account_no;

12.	Display names that end with an ‘A’ and have job ids with highest savings amount.
SELECT P.name,j.job_id, MAX(S.savings_amount)
FROM Person P 
JOIN Job J 
ON  P.job_id = J.job_id
      JOIN Savings_account S 
ON P.account_no = S.account_no
WHERE P.name LIKE ‘%A’
ORDER BY S.savings_amount DESC;


13.	Display the job locations that have the highest tax amount and median salary is less than $10,000.
SELECT j.job_location, MAX(T.tax_amount)
FROM Jobs J 
JOIN Taxes T 
ON  T.tax_id = J.tax_id
WHERE J.median_salary_wage > 10000;

14.	Display the number of jobs in each job location (Hint: using job name check which repeats the most and sort in the new table)
Ex: 	New York	5
Boston	8  
Chicago	10
California	25

SELECT job_name, COUNT(*)
FROM Jobs   
GROUP BY job_name;


15.	Display the names of the employees whose Occupation is Police and sort the Names in ascending order.
SELECT P.name, J.job_name
FROM Person P 
JOIN Jobs J
ON  P.job_id = J.job_id
WHERE J.job_name = ‘Police’
ORDER BY J.job_name ASC;



 Relational algebra for the use cases above:




1.	View the locations that have an average Salary of $50,000 along with name and gender.
SELECT j.job_location, P.name, P.gender, j.avg_salary 
FROM Person P
JOIN Job J
ON P.job_id = j.job_id
WHERE 
j.avg_salary > 50000;

2.	SQL query to find the count of the total occurrences of a particular character – ‘A’ in the Name field and the mean hourly wage.

SELECT j.mean_hourly_wage, P.name
FROM Person P
      JOIN Job J ON P.job_id = j.job_id
WHERE LENGTH(P.name) - LENGTH(REPLACE(P.name, 'A', ''));

3.	SQL query to find the tax rate of each job 
  SELECT J.job_name, T.tax_rate FROM jobs J
      INNER JOIN Taxes T
      ON J.tax_id=T.tax_id
      GROUP BY j.job_name;

4.	SQL Query to find the number of females, name, and savings amount.
SELECT P.name, Count(*), s.savings_amount FROM Person P
JOIN savings_account S
ON P.account_no=S.account_no
WHERE P.gender = ‘Female’;

5.	Display the males where the median hourly wage is NULL.
SELECT J.median_hourly_wage, P.name FROM Jobs J
JOIN Person P
ON P.job_id=J.job_id
WHERE P.gender = ‘male;

6.	SQL Query display all rows from both tables, populating the columns with table value. 
SELECT *
FROM Person
FULL OUTER JOIN Jobs
   ON Jobs.job_id = Person.job_id
ORDER BY Person.name ASC;

7.	SQL Query display all the information whose name start with C and location is either Arizona or Boston. 
   
SELECT Count(*), P.name FROM Person P
JOIN Jobs J
ON P.job_id=J.job_id
WHERE P.name LIKE ‘C%’and J.job_location IN (‘Arizona’ OR Boston’);

8.	SQL Query display all the name and the job name whose tax amount is greater than 1500.
SELECT P.name, J.job_name, T.tax_amount FROM Jobs J
JOIN Person P 
ON P.job_id=J.job_id
JOIN Taxes T
ON J.tax_id=T.tax_id WHERE T.tax_rate > 1500;
9.	Display the Job names and age of the entities who has the least savings amount. 
SELECT P.age, J.job_name, MIN(S.savings_amount) 
FROM Person P 
JOIN Job J 
ON  P.job_id = J.job_id
JOIN Savings_account S 
ON P.account_no = S.account_no;


10.	View the entity who has the highest tax rate.
SELECT COUNT(job_id), MAX(T.tax_rate)
FROM Jobs J 
JOIN Taxes T
ON T.tax_id = J.tax_id;

11.	Which age group has savings more than 1000. 

SELECT P.age, MAX(S.savings_amount)
FROM Person P 
JOIN Savings_account S 
ON P.account_no = S.account_no;

12.	Display names that end with an ‘A’ and have job ids with highest savings amount.
SELECT P.name,j.job_id, MAX(S.savings_amount)
FROM Person P 
JOIN Job J 
ON  P.job_id = J.job_id
      JOIN Savings_account S 
ON P.account_no = S.account_no
WHERE P.name LIKE ‘%A’
ORDER BY S.savings_amount DESC;


13.	Display the job locations that have the highest tax amount and median salary is less than $10,000.
SELECT j.job_location, MAX(T.tax_amount)
FROM Jobs J 
JOIN Taxes T 
ON  T.tax_id = J.tax_id
WHERE J.median_salary_wage > 10000;

14.	Display the number of jobs in each job location (Hint: using job name check which repeats the most and sort in the new table)
Ex: 	New York	5
Boston	8  
Chicago	10
California	25

SELECT job_name, COUNT(*)
FROM Jobs   
GROUP BY job_name;


15.	Display the names of the employees whose Occupation is Police and sort the Names in ascending order.
SELECT P.name, J.job_name
FROM Person P 
JOIN Jobs J
ON  P.job_id = J.job_id
WHERE J.job_name = ‘Police’
ORDER BY J.job_name ASC;





