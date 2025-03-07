# CSRF vs XSS
- XSS: exploit a user's trust in a website by injecting malicious scripts that run within the user's browser on trusted sites.
- CSRF : allowing attackers to perform unauthorized actions on behalf of the authenticated user.

## Part 1. POST Method
- <form> -> XSS

## Part 2.  CSRF Token - <iframe>
```javascript
<form>
<input name ="pass" value="1234">
<input name ="csrf" value="???">
</form>
```

## Part 3. CSRF Countermeasure !!!
- referer check
- referer : read_content.php?id=123
- If having a problem, pass the process
```javascript
<meta name="referrer" content="no-referrer">
```
- Input identification information

## Part 4. SOP / CORS
- Same resource (Domain, Skima, Port)
- Cross Origin Resource Sharing

## Part 5. ACAO
Access-Control-Allow-Origin
```javascript
<ifram src="vuln.com/mypage.php">
```
