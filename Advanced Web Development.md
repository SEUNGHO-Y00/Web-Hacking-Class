# Advanced Web Development

## Part 1. Review
* SQL = DB Language (select, insert, update)
* Check Mini assignment

```php
‹?php
  define('DB_SERVER', 'localhost');
  define('DB_USERNAME', 'admin');
  define('DB_PASSORD', 'student1234');
  define('DB_NAME', 'test');

  $db_conn = mysqli_connect (DB_SERVER, DB_USERNAME, DB_PASSWORD, DB_NAME);

  if ($_GET [' name '] == "") {
    $sql = "select * from test_table";
  }else{
    $sql = "select * from test_table where name='".$_GET ['name'] ."'";
  ｝
// call result package
  $result = mysqli_query($db_conn, $sql);
  $row = mysqli_fetch_array ($result);
?>
<h1>
student : <?=$row['name']?>, score : <?=$row['score']?>
</h1>
```

* Sign-in webpage
```php
if ($username != NULL && $password != NULL) {
  $sql = "INSERT INTO member (ber (user_id, user_pass, name, user_level, info) VALUES ('$username', '$password', '$username, 'student', '$userinfo');";

  if(Sresult = mysqli_query ($conn, $sql））{
    echo "<script>alert('회원가입 성공!')</script>";
    echo "<script>window.location.href='index.php';</script>";
  } else{
    echo "<script>alert('이미 존재하는 ID입니다.')</script>";
    echo "<script>window.location.href='signup.html';</script>";
  }
  mysqli_close($conn) ;
} else{
  echo"<script>alert('아이디와 비밀번호를 입력해주세요.')</script>";
  echo"«script>window.location.href='signup.html';</script>";
}
```

* log-in webpage
```php
if(isset($_POST['id']) && isset($_POST['pw'])){
  $conn = mysqli_connect ('localhost', 'admin', 'student1234', 'segfaultDB');
  $username = mysqli_real_escape_string ($conn, $_ POST['id']);
  $password = mysqli_real_escape_string(Sconn, $_POST ['pw']);

  $sql = "SELECT * FROM member where user_id = '$username' and user_pass = '$password';";
  if($result = mysqli_fetch_array(mysqli_query($conn, $sql))){
    $_SESSION['id'] = $username;
    header ('Location: index.php');
  } else{
    echo "<script>alert('등록되지 않은 사용자입니다.')</script>";
    header ('Location: index.php');
  }
  mysqli_close ($conn) ;
}
```

* Log-in: Authentication
  - OTP number authentication vulnerability?
  - Checking the identification
  - Identification / Authentication
  - Identification: a personal identification identifier that is used along with a password to access an electronic service among the various databases.
                    It should be unique identification information and should not be the same.
  - Authentication: the way of confirming the identity of a user while they access their profile on a particular platform.
                    Password, It is dangerous to open authentication information

## Part 2 - Login logic case

1) Identification and Authentication together - Create the login website to operate DB at one time
```php
$sql = "select * from member where"
$sql .= "id='$userid' and pass='$user_pass'"
ret = $sql.execute();
if($ret) { //login success}
else { //login fail}
```

2) Identification / Authentication separately
```php
sql =
select * from member where id = ''
$db_pass = sql.ret['pass']
if ($db_pass == $user_pass){ // login success}
else { // login fail}
```

(+) HASH - one way, it cannot return, One string of characters in a password is transformed into a completely different string using a mathematical hashing function.

3) 4 ways logics to Login
1. Identification / Authentication together
2. Identification / Authentication Seperately
3. Identification / Authentication together (with Hash)
4. Identification / Authentication Sepeartely (with Hash)

## Part 3 - Session ID
* typically located in either the URL query parameters or in a Cookie that is assigned to the user.

## Part 4 - Assignment
1. Review - Understanding Login Logic (Identification / Authentication)
2. Last Assignment
3. Log-in page (based on 4 Logics)
Additional - jwt
