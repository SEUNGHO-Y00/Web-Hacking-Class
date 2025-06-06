# Intermedium Web Development

NAT ? Network Address Translation is a technique that allows multiple devices to share a single IP address.
NAT network ? A system that uses a router to map private IP addresses to public IP addresses.
* How NAT works
  - NAT modifies the IP header of packets while they are in transit.
  - NAT translates private IP addresses to public IP addresses before packets are sent to an external network. 
  - NAT can be configured to advertise only one address for the entire network to the outside world. 
Log-in page connecting to DB ?
Docker ? A platform for building, shipping, and running applications using containers.
Docker (WebApp, mysql / specific port: CAT) vs Python (Web Application)

## Part 1. Reminding week 1
* Web server architecture
* WEP, WAS, DB

* URL = [protocol]://[IP]:[port]/[path]
* ?[parameter name]=[parameter value]   (GET Method)

* Assignment Review
  - Index page
    - main page (Log-in page) = When people get the webpage access, the webpage shows directly the index page (Log-in page).
    - header("location:login.php"); exit;
      = When operating page movement, the header needs a direction inside a response.
      = exit; function is essential!!! because it is available to redirect it.
  - Login page - <form action = "">
    = When the value in action is empty, the login function sends the value itself.
    - PHP function = When using any function frequently, we can make separated classes for the function.
    - <?php require_once('login_func.php'); ?>

* Example of the separated function class
```php
<?php
function login1($userid, $userpass) {
  $cred_id = "admin";
  $cred_pw = "admin1234";
  if($userid == $cred_id and $userpass == $cred_pw) {
    return $userid;
  }else{
    return 0;
  }
}
?>
```

* Example of Login page to bring the separated function
```php
<?php
  if(isset($_POST[ 'Submit'])){
    $login_res=login1($_POST[ 'UserId'], $_POST['Password']) ;
    echo "This > ". $login_res;
    if($login_res) {
      header ("location: index.php?login_id=". $login_res );
      exit;
    }else{
?>
```

* Error!
1. Print PHP Error
2. Echo "This >".$login_res;

## Part 2. Database = saving data, ex) Excel file
* Table
* Columns = Data category
* Rows
* DB
  - http://10.60.126.181:1018/phpmyadmin/
  - account and password (admin / student1234)
  - click new and create a test db => create table
* SQL = DB language
  - select = bring data
    = select [column name] from [table name]
    = ex) select name,pass from test_table
    = select * from test_table (every column)
  - insert = input data, save data
    = insert into [table name] (column name) value (values)
    = ex) insert into test_table (name,score,pass) value ('doldol','80','2222')
    = insert into test_table value (NULL,'dangdol','70','3333')
  - where = specific select data
    = select [column name] from [table name] where [condition]
    = ex) select name,pass from test_table where name='doldol'
    = condition - and // or

## Part 3. WAS - DB Connection
* PHP and MySQL Connection
1. WAS must know ID and Password
2. select
3. Bring data and print

* db_test.php
```php
<?PHP
  define('DB_SERVER', 'localhost');
  define('DB_USERNAME', 'admin');
  define('DB_PASSWORD', 'student1234');
  define('DB_NAME', 'test');

  $db_conn = mysqi_connect(DB_SERVER,DB_USERNAME,DB_PASSWORD,DB_NAME);

  //$sql = "select * from test_table";
  $sql = "select * from test_table where name='doldol'";
  $result = mysql_query($db_conn, $sql);

  $row = mysql_fetch_array($result);

  echo "Name : " . $row['name'];
  var_dump($row);

  echo "Pass : " . $row['pass'];
  $db_pass = $row['pass'];
  if($_POST['userpass'] == $db_pass) {
      //login ok
  }
?>
```

* mysql_fetch_array = It can make individual values bring out

## Part 4. Summary

* Database?
* SQL? SQL(select, insert, where)?
* How to use select in SQL of DB by using PHP

## Assignment
1. Review (Database, SQL)
2. Mini Mission = Result (Student "DolDol"'s score is "80") Using the GET method 
3. Create Account Page
4. Log-in page connect to DB
Extra. Joining Account information page
