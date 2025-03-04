# Basic Web Development

## Study Resource

* [Coding Everybody](https://www.opentutorials.org/course/1688/9331)

## Web Development Environment Setting (MacOS)

### OS Installation
* Web server = deliver file
* Web development APM = Application performance monitoring (APM) is a set of tools and practices that help developers identify and fix performance issues in web applications
* ~~ID / Password = Student / Student1234~~
* ifconfig = IP Address check
* VMware = Setting Network, [Mac Error](https://www.virtualbox.org/wiki/Testbuilds)
* UTM = Setting OS, Convert .ova to .vdmk and another convert .vdmk to .qcow2, [Solution](https://gist.github.com/tadhgboyle/a0c859b7d7c0a258593dc00cdc5006cc)
* Installation = Install .ova file, [Solution](https://www.youtube.com/watch?v=1suVXymrD0Q&ab_channel=SYSADMIN102%E2%84%A2)

### Network Setting
* MAC M1 virtual machine Network Error
  - Understanding [NAT](https://www.comptia.org/content/guides/what-is-network-address-translation)
  - [Solution](https://shape.host/resources/mastering-network-configuration-on-ubuntu-22-04-dhcp-and-static-ip-setup-for-single-and-multiple-nics)
  - Or sudo dhclient
* Termius = Connect IP address for a simple environment

### Connection between server and development environment
* File share - sudo python3 -m HTTP.server 80
* Web file delivery
* [SFTP](https://marketplace.visualstudio.com/items?itemName=Natizyskunk.sftp)
* Request from web browser

* URL Rule
  - Commend = [Protocol]://[Domain or IP address]:[Port]/[File Path]
* Web Root Path

## Web Development Operation (MacOS)

* WAS (Web Application Server)
  - Web (static) + WAS (dynamic) + DB

* Docker Activity Check
  - sudo docker ps -a
  - sudo docker rm -f [container ID] (If some dockers operate, delete those)
  - ./dockerCMD & (Docker open)

* vscode - sftp plug in

* PHP SERVER
  - $_GET['name'] = a parameter through GET Method (*Parameter: elements inserted in your URLs to help you filter and organize content)
  - GET / POST = https://www.akto.io/academy/get-vs-post
  - Front-end vs Back-end
  - Back-end = Server-side code (PHP, ASP, JSP, ...)
  - Front-end = Client-side code, Browser side (HTML, CSS, Javascript, ...)

* PHP
  - form function
  - method = "GET"            (php) $_GET['id']
  - method = "POST"           (php) $_POST['id']      * hidden URL, transfer method = request body
  - & = divide Parameters
  - action="[transfer webpage]">

## Assignment
1. Create a simple log-in page (DB X, the website which is able to log-in [admin/admin1234]
2. Add CSS to the webpage
