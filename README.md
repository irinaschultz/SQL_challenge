# SQL_challenge
For SQL analysis, there are given six data csv tables
1.departments:
•	dept_no (primary key): VARCHAR
•	dept_name: VARCHAR
2.dept_emp:
•	emp_no (foreign key referencing employees.emp_no): INTEGER
•	dept_no (foreign key referencing departments.dept_no): VARCHAR
3.	dept_manager:
•	dept_no (foreign key referencing departments.dept_no): VARCHAR
•	emp_no (foreign key referencing employees.emp_no): INTEGER
4.	employees:
•	emp_no (primary key): INTEGER
•	emp_title_id VARCHAR
•	birth_date: DATE
•	first_name: VARCHAR
•	last_name: VARCHAR
•	sex: VARCHAR
•	hire_date: DATE
5.	salaries:
•	emp_no (foreign key referencing employees.emp_no): INTEGER
•	salary: INTEGER
6.	titles:
•	title_id VARCHAR
•	title: VARCHAR
As I mentioned, the *date columns should ideally be defined as DATE type. However, I encountered issues while importing the data from CSV files, using VARCHAR temporarily and then converting the text to DATE in Jupyter Notebook is a viable solution for further data investigation.
Variable character columns are commonly set to VARCHAR as the default option. However, I know the maximum length of the text in a specific column.
