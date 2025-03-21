# Linux Study for Web Hacking

## 01. Intro Linux
 Part 1. OS
 
 Part 2. History
 
 Part 3. OpenSource

## 02. Setting
 Part 1. Virtual Machine 
 
 Part 2. Kali Linux
 
     - Kali Linux download (https://www.kali.org/get-kali/#kali-platforms)
     - Install on UTM (https://www.youtube.com/watch?v=9zdjQ9w_v_4&ab_channel=KskRoyal)
        = Error Kali needs at least 30GB
        
 Part 3. Command
     - CLI
     - Shell
     - Command Structure (1. Command 2. Argument 3. Option)
         which id (the command belongs to some programs)

## 03. Directory
 Part 1. Current directory - pwd
 
 Part 2. Directory movement 
     - Directory files check - ls
     - Change Directory - cd
     
 Part 3. Home Directory (~) - cd ~
     - Switch User - su
     
 Part 4. File information - ls [file name or directory path] -l
     - (.) hidden files => ls -a
     
 Part 5. Kali Linux File System
     - /bin = Binary, execute files
     - /dev = device, connecting hardware device
     - /etc = setting files
     - /home = each account home directory
     - /lib = library, sharing folders
     - /sbin = system administrator files
     - /tmp = temporary, anyone can use this directory, delete after shutdown
     - /var = save files in programs
     
 Part 6. Absolute Path vs Relative Path
    - https://www.redhat.com/sysadmin/linux-path-absolute-relative
    - ./ = current location
    - ../ = higher location
    
## 04. File
 Part 1. Vi Text Editor - Note
    - Vi mode (Edit mode [Excute: i] / Command mode [esc button back to the mode])
    - Command mode (:w = Save, :q = exit)
    - Search (on command mode) = /[search word]
    - Specific line = :[line number] , line delete (dd)
    
 Part 2. Check files
    - cat [txt file name]
    - It can read txt file only
    - file [file name] = text file type
    - more = it shows on the top
    
 Part 3. COPY
    - cp cp_test ./Desktop/        = copy [src] [dst]
    - cp cp_test ./Desktop/copy_test    = change the file name
    - mkdir normal_dir          = create a folder
    - cp -r normal_dir ./copy_dir      = directory copy
    
 Part 4. Remove
    - rm -r ./copy_dir       = remove directory // -f force remove
    
 Part 5. Move
    - mv mv_test ./Desktop/
    - mv [current directory] [future directory]
    - mv mv_test ./mv_changeName          = change file name
    
## 6. Authentication
  - People need account for individual usages

 Part 1. UID/GID
    - UID: User ID
    - GID: Group ID
    - root: highest account
    - useradd normaltic       = create new account
    - su normaltic
    
 Part 2. passwd
    - /etc/passwd    = user information in Linux
    - more /etc/passwd
    - vi /etc/passwd
    - 1. ID 2. password (/etc/shadow) 3. UID 4. GID 5. nickname of user 6. home directory 7. login shell (/usr/bin/nologin)
      
 Part 3. rwx
    - r: read
    - w: write
    - x: execute
    - cd /tmp      = everyone can use this directory
    - (1) owner authentication / (2) Group authentication / (3) Extra user authentication
    - 
 Part 4. Specialty Authority 
    (1) setuid - when the file is executed, it executes on owner of the file
               - -rws = setuid with execute authority
               - -rwS = setuid without execute authority
    (2) setgid - when the file is executed, it executes for group of the file
    (3) sticky bit - setting of directory
                   - anyone can create a file, but the creator only delete the created file.
      
 Part 5. Change Authority
    - chmod
    - u         r
    - g    +,-  w
    - o         x

## 7. Redirection
 Part 1. Data Stream
            input ---------------------->
       People <--> operation system <---> Computer
            <---------------------- output
   Standard input stream, 0
   Standard output stream, 1
   Standard error stream, 2
   File descriptor (fd):
   
 Part 2. Redirection
   pwd > pwd_result    (>: redirection)
   pwd >> pwd_result    (>>: redirection without deleting information)
   For Hacking, when saving the file instead of the result of the command on the screen
   
 Part 3. PIPE
   Process --> pipe --> process
   The output of one process makes the input of the other process
   A form of redirecting output to another destination for further processing.
   grep [finding pattern] [searching file / directory]
   ex) cat /etc/passwd | grep root
   ex) ifconfig | grep inet
   ex) ls /bin | grep "find"
