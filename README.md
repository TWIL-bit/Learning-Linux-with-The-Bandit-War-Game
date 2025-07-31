<h1>Learning Linux: The Bandit War Game</h1>


<h2>Description</h2>
Today I decided to take a crack at The Bandit wargame hosted by Over the Wire. This is a progressive based Linux game where you can complete challenges to make it to the next level and the goal is to see if you can complete all 34 levels.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Virtual Box</b>
- <b>Linux</b>

<h2>Environments Used </h2>

- <b>Kali-Linux</b>




<h2>Project walk-through:</h2>

<p>

I start with Level 0, which is logging into the game using SSH. The host as well as the username, password, and port number are provided for me.
Host: bandit.labs.overthewire.org
<br>
Username: bandit0
<br>
Password: bandit0
<br>
Port: 2220
<br>
I attempt to connect to the host via secure shell using the following command: 
ssh bandit0@bandit.labs.overthewire.org -p 2220 
After entering the command to establish the connection via port 2220, I am now asked for the password which was provided to me. I entered the password bandit0 and I am welcomed into the game.


 <br>
 <img width="975" height="542" alt="image" src="https://github.com/user-attachments/assets/72cd4898-c7ae-4628-8ab1-1c0ff375e626" />

 <br> </br>
 <img width="973" height="533" alt="image" src="https://github.com/user-attachments/assets/9fe3597e-db63-4bbd-9d7b-c31a8129496e" />



Level 0-1:
Now that I’ve established a connection to the host, I must locate a file in the home directory to retrieve the next password to log into the bandit1 account. The name of the file is “readme”. I used the find command to locate the file. (find -name “readme”) After locating the file, I was able to use the cat command to see the contents of this file. (cat readme)
<br> </br>
<img width="973" height="263" alt="image" src="https://github.com/user-attachments/assets/28f46b8d-d054-4696-8834-c42bfe795f58" />
<br> </br>
Level 1-2:
For this level, I have to login to the bandit1 account and locate the file that has the password for the bandit2 account. The file name is a dash “- “. Using the cat command will not allow you to see the contents of a file that has a dash as the file name. This is because the cat command sees a dash a stdin. Instead, we must prefix the path of the file. The file is in the home directory so we should use the command (cat ./-) to find the file named dash in the home directory. I tried this command and was able to get the password.
<br> </br>
<img width="975" height="58" alt="image" src="https://github.com/user-attachments/assets/8e7a04bc-82ba-46d2-ab89-e531764b17dc" />
<br> </br> 
Level 2-3:
Now I must look for the password that is stored in a file called “spaces in this filename”. I logged into the bandit2 account with the password I received in the last level and used the cat command to see what’s in the file. I originally got an error since the file name has spaces. Linux doesn’t recognize the spaces in file names, so it treats each word as its own file instead of looking for the entire name of a single file. To mitigate this, I must put the file name in quotations, and you will achieve the desired result.
<br> </br>
<img width="908" height="411" alt="image" src="https://github.com/user-attachments/assets/4094d171-ebfb-4eb6-9659-e6c7c262c6b0" />
<br> </br> 
Level 3-4:
The password for this file was stored in a different directory than the home directory. The file is in the inhere directory. The file is also hidden. To find the password, we must first change the directory to inhere by using the change directory command. (cd inhere) Now I can use the (ls) command to list the files in this directory. Since this file is hidden, it will not show when the list command is run. I must modify the command to show the hidden files as well. So, we can use (ls -a). The -a will show me files that are hidden in the directory. After running this command, I was able to locate the file and then the password.
<br> </br>
<img width="975" height="316" alt="image" src="https://github.com/user-attachments/assets/8b218f07-e12a-475d-97f2-11dc681c444d" />
<br> </br> 
Level 4-5:
To find the password for this file, I must look at the only human readable file in the inhere directory. There are multiple files in this directory, but we can run a command to help us find the human readable file that we need. By running the file command for all the files in the directory (file ./*), I can see the file type of each file.I can see that there is only one file that has ASCII text which is human readable & this is file 7. Now that I know which file is human readable, all I must do now is run the cat command (cat ./-file07) to open the file and get the password.
<br> </br>
<img width="975" height="292" alt="image" src="https://github.com/user-attachments/assets/e11d9290-ef70-4456-943a-22735e2a414e" />
<br> </br> 
Level 5-6:
I am given some criteria for the file that’s needed for this level:
<br> </br>
Human-readable; 1033 bytes in size; non-executable
<br> </br>
I start searching for this file by first looking at the file size for all the files in the inhere directory using the du command. (du -bytes –all) This shows me the file size of every file here. I see that there is only one file that is 1033 bytes in size which is (./maybehere07/.file2). It looks like the file is in the maybehere07 directory with the file name (.file2). Seeing this, I can now change to the maybehere07 directory using the cd command (cd maybehere07). Now all I must do is look at the contents of the file using the cat command. (cat ./.file2) I run this command and am given a password.
<br> </br>
<img width="975" height="544" alt="image" src="https://github.com/user-attachments/assets/2de3eaa5-e089-4d92-a425-7a9af78cb36a" />
<br> </br>
<br> </br>
<img width="973" height="391" alt="image" src="https://github.com/user-attachments/assets/0596c144-86f2-48c8-a66b-d2d7ecefbefb" />
<br> </br>
Level 6-7:
Level Criteria: Owned by user bandit7; Owned by group bandit6; 33 bytes in size.
<br> </br>
With the given criteria, I need to search the server for a file containing the password since the directory isn’t given to me. I start by seeing if I can find the file using the find command while also including the criteria given. The command I run is (find / -type f -user bandit7 -group bandit6 -size 33c). Running that command gave me many files, most of them saying permission denied. I did see one file that was accessible to me after looking through every file, but if I wanted to remove all the files that I don’t have permission to access I can do that by adding a null command. (2>/dev/null) I run my command again adding the null command (find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null) and receive the following file. After getting this file, I can cat the entire file path to see its contents and retrieve the password.
<br> </br>
<img width="973" height="489" alt="image" src="https://github.com/user-attachments/assets/ec7a9c50-1cb6-4ee5-853b-d9d995efa83c" />
<br> </br>
<br> </br>
<img width="975" height="98" alt="image" src="https://github.com/user-attachments/assets/f67bed9d-d735-4b37-9ab5-d0846c0f4407" />
<br> </br>
Level 7-8:
For this level, the password is stored in a text file next to the word millionth. I can run the ls command to see that there is only one file. After opening the file with cat command, I see that there are thousands of words and passwords, and I need to be more specific. I can use the grep command to search for a specific word in this file. After searching for the word millionth with the grep command, I can retrieve the password.
<br> </br>
<img width="973" height="498" alt="image" src="https://github.com/user-attachments/assets/45507efe-f727-42c6-afcb-4ad72d89a2dc" />
<br> </br> 
Level 8-9:
I will be using the file data.txt again for this level. I am looking for a string of text that only occurs once & that will be my password to the next level. I start by using cat command to open the file and I am giving many lines of characters. I must sort through this list to find the unique line of text. I can do this by sorting and searching for only unique characters with the following command: (cat data.txt | sort | uniq -u) After running this command, I am left with one line, and this must be the password.
<br> </br>
<img width="975" height="533" alt="image" src="https://github.com/user-attachments/assets/51b84031-66b5-4979-ba4f-4bccd4012002" />
<br> </br>
<br> </br>
<img width="955" height="252" alt="image" src="https://github.com/user-attachments/assets/3d4b7f71-b73a-4c2d-a755-98097d5577f0" />
<br> </br>
Level 9-10:
The data.txt file for this level has a lot of non-human readable data as well as some human readable data. The password I’m looking for is stored in one of the few human-readable data strings preceded by several “=” signs. When opening the file normally, there is a lot of data that is hard to read and understand. I can search for the human-readable strings by using the strings command. (strings data.txt) I am then provided with hints that lead me to the password.
<br> </br>
<img width="975" height="525" alt="image" src="https://github.com/user-attachments/assets/33bdf8f6-d4a6-4d85-8068-52d913be7dbf" />
<br> </br>
<br> </br>
<img width="975" height="542" alt="image" src="https://github.com/user-attachments/assets/7f0775e0-ae2b-47a2-a150-74c700e48fd3" />
<br> </br>
<br> </br>
<img width="975" height="539" alt="image" src="https://github.com/user-attachments/assets/09b18247-1a31-4688-90ff-4db6e8dc5fef" />
<br> </br>
<br> </br>
<img width="972" height="530" alt="image" src="https://github.com/user-attachments/assets/ddae0965-7806-4342-9b3e-f6ae908843bb" />
<br> </br>
Level 10-11:
I am provided with the information that the password is stored in the data.txt file which contains base64 encoded data. Knowing this, I must run a command that decodes the data to give me the original password. To decode the data, I can run the base64 decode command. (base64 –decode ./data.txt) Running this command gave me the password to the next level.
<br> </br>
<img width="964" height="291" alt="image" src="https://github.com/user-attachments/assets/be439a09-5065-4e0f-8c8e-c534143b70d4" />
<br> </br> 
Level 11-12:
The password for this level is in the data.txt file and each character has been rotated by 13 positions. I must use ROT13 which is a substitution cipher that rotates each letter of a string by 13 positions. Since the letters have already been rotated, I must run the command to rotate them back. I achieved this using the command (tr ‘A-Za-z’ ‘N-ZA-Mn-za-m’ <<< “text”). Running this command gave me the password I needed for the next level.
<br> </br>
<img width="975" height="178" alt="image" src="https://github.com/user-attachments/assets/f770400a-fb86-4a1e-ab48-fd8400788c43" />
<br> </br> 
Level 12-13:
This level involved a hex dump of a file that was repeatedly compressed. I found it extremely difficult to get through this level. After following a guide on hex dumps and how to decompress multiple times with different decompression formats, I was finally able to get through the level. I also learned a lot that I didn’t know before this level. I have been introduced to the tar command as well as the gzip and bzip file types and plan to get more familiar with this area.
<br> </br>
<img width="973" height="561" alt="image" src="https://github.com/user-attachments/assets/aa5fe667-ede8-4d1c-8695-81a0f2a9fc01" />
<br> </br> 
Level 13-14:
For level 13-14, I’m not given a password. The goal is to obtain the private key to allow me to connect to the bandit14 account. I was able to login to the bandit13 account to see that a file named sshkey.private was in the home directory of that account. After seeing this, I now need to securely transfer that file to my own local account. I can do this using the secure copy command. (SCP) After I obtained the file containing the private key, I can now attempt to connect to bandit14 using the ssh key rather than a password. I can do this by including (-i) in my command to allow access via private key. I was granted access.
<br> </br>
<img width="966" height="558" alt="image" src="https://github.com/user-attachments/assets/2b42cbe4-485b-471d-a97d-a98e0b907be8" />
<br> </br> 
Level 14-15:
After logging into bandit14, I was already told the location of the password in the previous level which is (/etc/bandit_pass/bandit14). I open the file and get the password. The goal for this level is to take that password and submit it to port 30000 on the local host. I can do this by using the nc/netcat command. (nc/netcat) This allows me to read and write data over a network connection. I used the command (nc localhost 30000) and provided the password here. This gave me the next password that I need to progress to the next level.
<br> </br>
<img width="975" height="417" alt="image" src="https://github.com/user-attachments/assets/68ac3e27-04a8-4280-b52a-ab277a584e48" />
<br> </br> 
Level 15-16:
To get to the next level, I must submit the current password from the previous level to port 30001 on the localhost using ssl/tls encryption. OpenSSL is a command that can be used to establish a secure connection to the local host. I connect to the local host using the command (openssl s_client -connect localhost:30001) After establishing connection, I simply paste the password from the previous level, and I am given the password that I need.
<br> </br>
<img width="975" height="555" alt="image" src="https://github.com/user-attachments/assets/ba4c13ba-05da-461c-8209-01b6faa42f3a" />
<br> </br> 
Level 16-17:
I was able to solve this level by doing a port scan on the network. I first had to scan a range of ports to see which ports were open. I then had to figure out which ports had an ssl/tls connection. After running a port scan over the range of 31000-32000 using the command 
(nmap -sV localhost -p 31000-32000), I saw that there are five ports open and two of them have an ssl connection. I tried my current password for both and port 31790 turned out to be the correct port. Once I entered my password for this port, I was given the private key to the next level. I created a folder on my localhost containing the private key to log into the next level.
<br> </br>
<img width="975" height="569" alt="image" src="https://github.com/user-attachments/assets/13574e68-26fa-4d78-a1e2-1811bd0055a0" />
<br> </br> 
Level 17-18:
This level involved obtaining the password by looking at the difference between two files which are passwords.old and passwords.new. The line that is different between the two is the password. I can use the difference command (diff) to see which line is different between the two files. (diff passwords.old passwords.new) The output gave me the password I was looking for to get to the next level.
<br> </br>
<img width="969" height="570" alt="image" src="https://github.com/user-attachments/assets/56aebe1b-9a35-445e-80b8-673fb6996705" />
<br> </br> 
Level 18-19:
I was provided with the information that the password is in a file named readme in the home directory of the bandit18 user account. When trying to login to the bandit18 account, I receive a message that says “Byebye!” It looks like something is preventing me from logging in through ssh. The .bashrc file is run every time a terminal is loaded, and it has been modified to deny my access through ssh. I am still able to see if there are any files on the account. I can establish a connection along with the (ls) command to see what files are on the account without logging in. (ssh bandit18@bandit.labs.overthewire.org -p 2220 ls) Running this command, I can see that there is one file named readme and it looks to be the file that I need. I can now establish another connection along with the cat command to open the file without logging into the account. (ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme) Running this command gave me the password that I need for the next level.
<br> </br>
<img width="967" height="566" alt="image" src="https://github.com/user-attachments/assets/3bb6c860-a1dc-4312-8fd0-ed3aabc56ed1" />
<br> </br> 
Level 19-20:
To retrieve the password for this level, I must use the setuid binary in the home directory. After looking at the file permissions for bandit20-do with (ls -la), I can see that the file is owned by user bandit20 and group bandit19. I also see that I have permission to execute the binary as bandit20 since it is owned by the bandit19 group. I execute the binary with command (./bandit20-do). This now allows me to run a command as user bandit20, so I open the file path that has the password. (./bandit20-do ls /etc/bandit_pass) From here, I just need to open the bandit20 file to get the password. (./bandit20-do cat /etc/bandit_pass/bandit20)
<br> </br>
<img width="973" height="481" alt="image" src="https://github.com/user-attachments/assets/108c8373-aef7-4e9f-a19d-772afa289e0b" />
<br> </br> 
Level 20-21:
To get the password for level 20-21, I must establish a connection to my localhost through a port number. The setuid binary (./suconnect) will read a line of text through the connection & if the text input is the same as the password from the previous level, I will get the password to the next level. I establish a connection using the netcat command while including the echo command to input my message. I also include the “&” symbol to allow the process to run in the background. (echo -n ‘0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO’ | nc -l -p 1234 &) After executing this command, I am given the password.
<br> </br>
<img width="973" height="478" alt="image" src="https://github.com/user-attachments/assets/b862be7d-4c28-4944-b2e4-4a0c9842c31a" />
<br> </br> 
Level 21-22:
This level involved looking at a cronjob to see what command is being executed. To locate the file, I was provided with the cronjobs directory to see what files were there. I accessed this directory with command (cd /etc/cron.d/). I see multiple cronjob files but looked specifically at cronjob_bandit22 for this level. A file is being created in the temporary folder and executed every minute by user bandit22. The name of the file is /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv. Seeing this, I can open this temporary file and see if it will provide me with the password, which it did.
<br> </br>
<img width="973" height="472" alt="image" src="https://github.com/user-attachments/assets/18371957-3961-4305-aba9-afa184375b02" />
<br> </br> 
Level 22-23:
Passing this level is very similar to level 21-22. I navigate to cronjobs the same way as in the previous level, but this time I am looking at cronjob_bandit23. I open this cronjob to see what file is being executed which is (/usr/bin/cronjob_bandit23.sh). I open this file with the cat command to see the details of the file. I am provided with a line of code that will give me the password. I just need to replace the myname variable with the name of the user who owns the file which is bandit23. (echo I am user bandit23 | md5sum | cut -d ' ' -f 1) After running this command, I am given the password.
<br> </br>
<img width="973" height="484" alt="image" src="https://github.com/user-attachments/assets/ed24678e-4786-4ad2-803a-8900864b5d8e" />
<br> </br> 

</p>
