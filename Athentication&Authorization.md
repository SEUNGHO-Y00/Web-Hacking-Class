# Athentication & Authorization
1. Authentication
   - During authenticating vulnerability
   - Ignoring the attack of authentication
2. Authorization
   - Not working, but make it work

## Part 1. Authentication representative cases
1. Authentication through Cookie (Client Side information)
2. Process jump - Direct connect, identify verification (ex. create ID process)
3. Parameter response values modification
   - mobile app vulnerability
4. No limitation on the number of Authentication (Log-in page, mypage password change)

## Part 2. Authorization representative cases
- The key strategy is parameter modification
- Direct contact
- Checking file extension in JavaScript
- Static Analysis(without executing code), Dynamic Analysis(executing code)

## Part 3. CTF
1. CTF - Authorization 1
   - access limitation by using footnote (Client side, authorization check)
     * Using CSS, display: none;
   - Using Burp Suite, it intercepts the process
   - During the GET method, "Accept-Encoding: gzip, deflate, br" => Do intercept => Response this request
   - Delete the footnote comment
   - OR, check the link page (href=)

2. CTF - Authorization 2
   - Checking authorization on the client side

3. CTF - Authorization 3
   - When using intercept in the Burp suite, the button function does not connect with the server.
   - It means it connects with the client side, JavaScript.
   - The JavaScript with Obfuscation method => dynamic analysis
   - F12 = Console => type the function "goMenu('9999','admin')

4. CTF - Authorization 4
   - Guessing attack
   - When entering the notice and checking the URL, it said read.php
   - Put the possible URLs like post, create, and write.

5. CTF - Authorization 5

6. CTF - Authorization 6
   - Parameter modification
