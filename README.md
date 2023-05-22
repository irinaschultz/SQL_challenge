# SQL_challenge
---sql-challenge_EmployeeSQL
-- PART 1 - Data Engineering
-- Creating table schema
-- Create department table 

DROP TABLE departments;  

CREATE TABLE departments (dept_no VARCHAR, dept_name VARCHAR NOT NULL,
   PRIMARY KEY (dept_no));

select * from departments;

-- Create dept_emp table
DROP TABLE dept_emp;
CREATE TABLE dept_emp (emp_no INT   NOT NULL,
    dept_no VARCHAR   NOT NULL,
    FOREIGN KEY (emp_no) REFERENCES employees (emp_no),
    FOREIGN KEY (dept_no) REFERENCES departments (dept_no),
    PRIMARY KEY (emp_no, dept_no) );
select* from dept_emp;
--- Create dept_manager table
DROP TABLE dept_manager;
CREATE TABLE dept_manager (
    dept_no VARCHAR   NOT NULL,
    emp_no INT   NOT NULL,
    FOREIGN KEY (emp_no) REFERENCES employees (emp_no),
    FOREIGN KEY (dept_no) REFERENCES departments (dept_no),
    PRIMARY KEY (dept_no, emp_no)
);
select * from dept_manager;
--- Create table employees
DROP TABLE employees;
CREATE TABLE employees (
    emp_no INT   NOT NULL,
    emp_title_id VARCHAR NOT NULL,
    birth_date  VARCHAR   NOT NULL,
    first_name VARCHAR   NOT NULL,
    last_name VARCHAR   NOT NULL,
    sex VARCHAR   NOT NULL,
    hire_date  VARCHAR   NOT NULL,
    FOREIGN KEY (emp_title_id) REFERENCES titles (title_id),
    PRIMARY KEY (emp_no)
);
select * from employees; 
--- create table salaries
drop table salaries

create table salaries (
      emp_no int not null,
      salary int not null,
    Primary Key (emp_no),
	Foreign key (emp_no) references employees(emp_no));

select * from salaries;

--- create table titles
drop table titles

create table titles (
     title_id VARCHAR  NOT NULL,
	 title VARCHAR NOT NULL,
   Primary Key (title_id)
);

select * from titles;

--Data analysis____
-----------------------------------------------

--1.List the employee number, last name, first name, 
--sex, and salary of each employee____
SELECT employees.emp_no, 
employees.last_name,
employees.first_name,
employees.sex,
salaries.salary
FROM employees
LEFT JOIN salaries
ON employees.emp_no = salaries.emp_no
ORDER BY emp_no

--2.List the first name, last name, 
--and hire date for the employees who were hired in 1986.
SELECT first_name, last_name, hire_date 
FROM employees
WHERE hire_date BETWEEN '1/1/1986' AND '12/31/1986'
ORDER BY hire_date;

--3.List the manager of each department along with their department number, 
--department name, employee number, last name, and first name.
SELECT departments.dept_no, departments.dept_name, dept_manager.emp_no, 
employees.last_name, employees.first_name
FROM departments
JOIN dept_manager
ON departments.dept_no = dept_manager.dept_no
JOIN employees
ON dept_manager.emp_no = employees.emp_no;

--4.List the department number for each employee along with that employee’s employee number, 
--last name, first name, and department name.
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no;

--5.List the first name, last name, 
--and sex of each employee whose first name is Hercules and whose last name begins with the letter B.
SELECT employees.first_name, employees.last_name, employees.sex
FROM employees
WHERE first_name = 'Hercules'
AND last_name Like 'B%'

--6.List each employee in the Sales department, 
--including their employee number, last name, and first name.
SELECT departments.dept_name, employees.last_name, employees.first_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales';

--7.List each employee in the Sales and Development departments, 
--including their employee number, last name, first name, and department name.
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales' 
OR departments.dept_name = 'Development';

--8.List the frequency counts, in descending order, 
--of all the employee last names (that is, how many employees share each last name).
SELECT last_name,
COUNT(last_name) AS "frequency"
FROM employees
GROUP BY last_name
ORDER BY
COUNT(last_name) DESC;


