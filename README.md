postgres-# \dt employee;
          List of relations
 Schema |   Name   | Type  |  Owner
--------+----------+-------+----------
 public | employee | table | postgres
(1 row)
postgres-# \dt DEPARTMENTS;
            List of relations
 Schema |    Name     | Type  |  Owner
--------+-------------+-------+----------
 public | departments | table | postgres
(1 row)
postgres-# \dt PROJECTS;
          List of relations
 Schema |   Name   | Type  |  Owner
--------+----------+-------+----------
 public | projects | table | postgres
(1 row)
postgres-# \dt EMPLOYEE_PROJECTS;
               List of relations
 Schema |       Name        | Type  |  Owner
--------+-------------------+-------+----------
 public | employee_projects | table | postgres
(1 row)
postgres=# SELECT * FROM departments;
 department_id |     department_name
---------------+--------------------------
             1 | Human Resources
             2 | Finance
             3 | Information Technology
             4 | Marketing
             5 | Legal
             6 | Operations
             7 | Customer Service
             8 | Sales
             9 | Research and Development
            10 | Procurement
(10 rows)
postgres=# SELECT * FROM employee;
 employee_id | first_name | last_name |           email           | hire_date  | salary  | department_id | phone_number -------------+------------+-----------+---------------------------+------------+---------+---------------+--------------         101 | Alice      | Johnson   | alice.johnson@company.com | 2015-03-15 | 4500.00 |             1 |
         102 | Bob        | Smith     | bob.smith@company.com     | 2018-06-23 | 5200.00 |             3 |
         103 | Carol      | Adams     | carol.adams@company.com   | 2012-09-10 | 6700.00 |             2 |
         104 | David      | Lee       | david.lee@company.com     | 2020-01-05 | 3800.00 |             4 |
         105 | Eve        | Martins   | eve.martins@company.com   | 2019-12-11 | 4000.00 |             3 |
         106 | Frank      | Green     | frank.green@company.com   | 2017-07-08 | 6000.00 |             8 |
         107 | Grace      | Brown     | grace.brown@company.com   | 2014-11-02 | 4900.00 |             5 |
         108 | Hank       | Wilson    | hank.wilson@company.com   | 2013-02-17 | 3100.00 |             6 |
         109 | Ivy        | Clark     | ivy.clark@company.com     | 2021-08-30 | 2700.00 |             9 |
         110 | Jake       | White     | jake.white@company.com    | 2022-05-19 | 3600.00 |             7 |
(10 rows)
postgres=# SELECT * FROM employee_projects;
 employee_id | project_id | assigned_date
-------------+------------+---------------
         101 |        201 | 2023-01-10
         102 |        203 | 2024-01-05
         103 |        202 | 2022-05-20
         104 |        204 | 2025-02-10
         105 |        203 | 2024-01-07
         106 |        207 | 2022-04-15
         107 |        205 | 2023-07-15
         108 |        210 | 2022-09-10
         109 |        208 | 2025-01-10
         110 |        206 | 2021-11-05
(10 rows)
postgres=# SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employee;
   full_name
---------------
 Alice Johnson
 Bob Smith
 Carol Adams
 David Lee
 Eve Martins
 Frank Green
 Grace Brown
 Hank Wilson
 Ivy Clark
 Jake White
(10 rows)
                                                             ^
postgres=# SELECT LOWER(first_name) AS first_name_lower, LOWER(last_name) AS last_name_lower FROM employee;
 first_name_lower | last_name_lower
------------------+-----------------
 alice            | johnson
 bob              | smith
 carol            | adams
 david            | lee
 eve              | martins
 frank            | green
 grace            | brown
 hank             | wilson
 ivy              | clark
 jake             | white
(10 rows)
postgres=# SELECT SUBSTRING(first_name FROM 1 FOR 3) AS first_three_letters FROM employee;
 first_three_letters
---------------------
 Ali
 Bob
 Car
 Dav
 Eve
 Fra
 Gra
 Han
 Ivy
 Jak
(10 rows)


postgres=# SELECT REPLACE(email, '@company.com', '@org.com') AS updated_email FROM employee;
     updated_email
-----------------------
 alice.johnson@org.com
 bob.smith@org.com
 carol.adams@org.com
 david.lee@org.com
 eve.martins@org.com
 frank.green@org.com
 grace.brown@org.com
 hank.wilson@org.com
 ivy.clark@org.com
 jake.white@org.com
(10 rows)
postgres=# SELECT TRIM('padded_string_column') AS trimmed_string FROM employee;
    trimmed_string
----------------------
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
 padded_string_column
(10 rows)

postgres=# SELECT LENGTH(CONCAT(first_name, ' ', last_name)) AS name_length FROM employee;
 name_length
-------------
          13
           9
          11
           9
          11
          11
          11
          11
           9
          10
(10 rows)
                   ^
postgres=# SELECT UPPER('project_name') AS project_upper FROM employee;
 project_upper
---------------
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
 PROJECT_NAME
(10 rows)
postgres=# SELECT REPLACE('project_name', '-', '') AS project_no_dashes FROM employee;
 project_no_dashes
-------------------
 project_name
 project_name
 project_name
 project_name
 project_name
 project_name
 project_name
 project_name
 project_name
 project_name
(10 rows)
postgres=# SELECT CONCAT('Emp: ', first_name, ' ', last_name, ' (', department_id, ')') AS label FROM employee;
         label
------------------------
 Emp: Alice Johnson (1)
 Emp: Bob Smith (3)
 Emp: Carol Adams (2)
 Emp: David Lee (4)
 Emp: Eve Martins (3)
 Emp: Frank Green (8)
 Emp: Grace Brown (5)
 Emp: Hank Wilson (6)
 Emp: Ivy Clark (9)
 Emp: Jake White (7)
(10 rows)
postgres=# SELECT LENGTH(email) AS email_length FROM employee;
 email_length
--------------
           25
           21
           23
           21
           23
           23
           23
           23
           21
           22
(10 rows)
postgres=# SELECT SPLIT_PART(email, '@', 1) AS username FROM employee;
   username
---------------
 alice.johnson
 bob.smith
 carol.adams
 david.lee
 eve.martins
 frank.green
 grace.brown
 hank.wilson
 ivy.clark
 jake.white
(10 rows)
postgres=# SELECT CONCAT(UPPER(last_name), ', ', INITCAP(first_name)) AS formatted_name FROM employee;
 formatted_name
----------------
 JOHNSON, Alice
 SMITH, Bob
 ADAMS, Carol
 LEE, David
 MARTINS, Eve
 GREEN, Frank
 BROWN, Grace
 WILSON, Hank
 CLARK, Ivy
 WHITE, Jake
(10 rows)
postgres=#
postgres=# SELECT ROUND(salary) AS rounded_salary FROM employee;
 rounded_salary
----------------
           4500
           5200
           6700
           3800
           4000
           6000
           4900
           3100
           2700
           3600
(10 rows)


postgres=# SELECT salary FROM employee WHERE MOD(salary, 2) = 0;
 salary
---------
 4500.00
 5200.00
 6700.00
 3800.00
 4000.00
 6000.00
 4900.00
 3100.00
 2700.00
 3600.00
(10 rows)
postgres=# SELECT end_date - start_date AS project_duration FROM PROJECTS;
 project_duration
------------------
              364
              350

              149
              184
              364
              364

              245
              365
(10 rows)
postgres=# SELECT ABS(e1.salary - e2.salary) AS salary_difference
postgres-# FROM employee e1, employee e2
postgres-# WHERE e1.employee_id = 1 AND e2.employee_id = 2;
 salary_difference
-------------------
(0 rows)

postgres=# SELECT salary, salary * POWER(1.10, 1) AS increased_salary FROM employee;
 salary  |    increased_salary
---------+-------------------------
 4500.00 | 4950.000000000000000000
 5200.00 | 5720.000000000000000000
 6700.00 | 7370.000000000000000000
 3800.00 | 4180.000000000000000000
 4000.00 | 4400.000000000000000000
 6000.00 | 6600.000000000000000000
 4900.00 | 5390.000000000000000000
 3100.00 | 3410.000000000000000000
 2700.00 | 2970.000000000000000000
 3600.00 | 3960.000000000000000000
(10 rows)


postgres=# SELECT FLOOR(RANDOM() * 10000 + 1) AS test_id;
 test_id
---------
    5901
(1 row)
postgres=# SELECT salary,
postgres-#        CEIL(salary) AS salary_ceil,
postgres-#        FLOOR(salary) AS salary_floor
postgres-# FROM employee;
 salary  | salary_ceil | salary_floor
---------+-------------+--------------
 4500.00 |        4500 |         4500
 5200.00 |        5200 |         5200
 6700.00 |        6700 |         6700
 3800.00 |        3800 |         3800
 4000.00 |        4000 |         4000
 6000.00 |        6000 |         6000
 4900.00 |        4900 |         4900
 3100.00 |        3100 |         3100
 2700.00 |        2700 |         2700
 3600.00 |        3600 |         3600
(10 rows)


postgres=# SELECT phone_number, LENGTH(phone_number) AS phone_length FROM employee;
 phone_number | phone_length
--------------+--------------
              |
              |
              |
              |
              |
              |
              |
              |
              |
              |
(10 rows)
salary  | salary_category
---------+-----------------
 4500.00 | Low
 5200.00 | Low
 6700.00 | Low
 3800.00 | Low
 4000.00 | Low
 6000.00 | Low
 4900.00 | Low
 3100.00 | Low
 2700.00 | Low
 3600.00 | Low
(10 rows)


postgres=# SELECT salary, LENGTH(CAST(salary AS TEXT)) AS digit_count FROM employee;
 salary  | digit_count
---------+-------------
 4500.00 |           7
 5200.00 |           7
 6700.00 |           7
 3800.00 |           7
 4000.00 |           7
 6000.00 |           7
 4900.00 |           7
 3100.00 |           7
 2700.00 |           7
 3600.00 |           7
(10 rows)
postgres=# SELECT salary,
postgres-#   CASE
postgres-#     WHEN salary >= 100000 THEN 'High'
postgres-#     WHEN salary >= 50000 THEN 'Medium'
postgres-#     ELSE 'Low'
postgres-#   END AS salary_label
postgres-# FROM employee;
 salary  | salary_label
---------+--------------
 4500.00 | Low
 5200.00 | Low
 6700.00 | Low
 3800.00 | Low
 4000.00 | Low
 6000.00 | Low
 4900.00 | Low
 3100.00 | Low
 2700.00 | Low
 3600.00 | Low
(10 rows)


postgres=# SELECT COALESCE(email, 'No Email') AS email_display FROM employee;
       email_display
---------------------------
 alice.johnson@company.com
 bob.smith@company.com
 carol.adams@company.com
 david.lee@company.com
 eve.martins@company.com
 frank.green@company.com
 grace.brown@company.com
 hank.wilson@company.com
 ivy.clark@company.com
 jake.white@company.com
(10 rows)
ostgres=# SELECT hire_date,
postgres-#   CASE
postgres-#     WHEN hire_date < DATE '2015-01-01' THEN 'Veteran'
postgres-#     ELSE 'New'
postgres-#   END AS status
postgres-# FROM employee;
 hire_date  | status
------------+---------
 2015-03-15 | New
 2018-06-23 | New
 2012-09-10 | Veteran
 2020-01-05 | New
 2019-12-11 | New
 2017-07-08 | New
 2014-11-02 | Veteran
 2013-02-17 | Veteran
 2021-08-30 | New
 2022-05-19 | New
(10 rows)


postgres=# SELECT COALESCE(salary, 3000) AS salary_with_default FROM employee;
 salary_with_default
---------------------
             4500.00
             5200.00
             6700.00
             3800.00
             4000.00
             6000.00
             4900.00
             3100.00
             2700.00
             3600.00
(10 rows)

postgres=# SELECT department_name,
postgres-#   CASE
postgres-#     WHEN department_name = 'Information Technology' THEN 'IT'
postgres-#     WHEN department_name = 'Human Resources' THEN 'HR'
postgres-#     ELSE 'Other'
postgres-#   END AS department_category
postgres-# FROM departments;
     department_name      | department_category
--------------------------+---------------------
 Human Resources          | HR
 Finance                  | Other
 Information Technology   | IT
 Marketing                | Other
 Legal                    | Other
 Operations               | Other
 Customer Service         | Other
 Sales                    | Other
 Research and Development | Other
 Procurement              | Other
(10 rows)

postgres=# SELECT salary,
postgres-#   CASE
postgres-#     WHEN salary >= 100000 THEN 'High Tax'
postgres-#     WHEN salary >= 50000 THEN 'Medium Tax'
postgres-#     ELSE 'Low Tax'
postgres-#   END AS tax_band
postgres-# FROM employee;
 salary  | tax_band
---------+----------
 4500.00 | Low Tax
 5200.00 | Low Tax
 6700.00 | Low Tax
 3800.00 | Low Tax
 4000.00 | Low Tax
 6000.00 | Low Tax
 4900.00 | Low Tax
 3100.00 | Low Tax
 2700.00 | Low Tax
 3600.00 | Low Tax
(10 rows)

postgres=# SELECT end_date - start_date AS duration,
postgres-#   CASE
postgres-#     WHEN end_date - start_date < 30 THEN 'Short'
postgres-#     WHEN end_date - start_date BETWEEN 30 AND 90 THEN 'Medium'
postgres-#     ELSE 'Long'
postgres-#   END AS duration_label
postgres-# FROM projects;
 duration | duration_label
----------+----------------
      364 | Long
      350 | Long
          | Long
      149 | Long
      184 | Long
      364 | Long
      364 | Long
          | Long
      245 | Long
      365 | Long
(10 rows)

postgres=# SELECT employee_id,
postgres-#   CASE
postgres-#     WHEN MOD(employee_id, 2) = 0 THEN 'Even'
postgres-#     ELSE 'Odd'
postgres-#   END AS id_type
postgres-# FROM employee;
 employee_id | id_type
-------------+---------
         101 | Odd
         102 | Even
         103 | Odd
         104 | Even
         105 | Odd
         106 | Even
         107 | Odd
         108 | Even
         109 | Odd
         110 | Even
(10 rows)
