# Burp Suite Basic

## Part 1 - Reviews
1. Identification / Authentication
  1) Identification and Authentication together
```javascript
//pseudocode
$sql = "select * from member where id='$user=_id' and pass='$user_pass'"
$ret = $sql.execute()
if($ret) { //login success }
else     { //login fail    }
```

  2) Identification / Authentication separately
```javascript
//pseudocode
$sql = "select * from member where id='$user=_id'" and pass='$user_pass'"
$db_pass = $sql.execute()
if($db_pass == $user_pass) { // login success }
else { // login fail }
```

  3) With Hash (Password)

2. Cookie / Session / SessionID
* Cookie: A small piece of data stored on the user's computer by the web browser while browsing a website. Cookies are used to remember information about the user, such as login status or site preferences, across different sessions.
* Session: A server-side storage of information that is used to maintain user state between HTTP requests. Unlike cookies, session data is stored on the server and can keep sensitive information secure from client-side access.
* Session ID: A unique identifier that is typically stored in a cookie on the user's browser or passed in the URL. This ID maps to the session data stored on the server, allowing the server to retrieve the user's session information on subsequent requests.

3. Burp Suite Basic Concept
* Web Proxy Tool
* Proxy - A proxy server acts as an intermediary between a client and the internet. It accepts requests from clients, forwards them to the appropriate server, and returns the server's response back to the client.
* Intall - (https://portswigger.net/burp)
  1) Own computer -> Burp Suite (Analysing own traffic) = Setting Loopback only
  2) Other Computers -> Burp Suite (Mobile Web Hacking) = Setting All interfaces under proxy listener of burp suite
* Setting - Firefox (or any browsers)
  1) Network Setting -> Manual Proxy Configuration -> HTTP Proxy (127.0.0.1 / Port 8888)
* Normal Transmission = Browser -> Google Server
* Burp Suite Transmission = Browser -> Proxy -> Google Server
* Why Web Proxy tool? Through the tool, security professionals can see the traffic

## Part 2 - Burp Suite
1. Burp Suite Instruction
* Proxy -> Intercept -> Open Browser = Automatically setting of burp suite basic concept
* Request Interception rules
* Response Interception rules
* Match and Replace rules

2. Burp Suite Intercept
* Intercept on - It makes the browser stop and read the processing.
* History - Traffic history
* Repeater
* Decoder
* Comparer
* Intruder

3. state code
* 200 = OK
* 300 = Redirect
* 400 = Client Error
* 500 = Server Error

## Part 3 - Assignment
1. BBS (bulletin board system)
- Post Something : Insert
- List BBS : Select
- Read Something : Select
- Revise something : update
- Delete something : delete
2. BBS Page
- select * from board limit 0,10    = limit [index],[count]
3. BBS Search
- select * from board where title like 'normaltic'
- %normaltic : the last word normaltic
- normaltic% : the first word normaltic
4. BBS sort
- order by [column name] [asc/desc]
5. Review
- Burp = CTF
6. Javascript
- Create keylog or Cookie
