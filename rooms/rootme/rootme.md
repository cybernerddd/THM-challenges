# TryHackMe - Rootme

##Enumeration
Nmap Found:
- Port 22(SSH), 80(HTTP) opened

## Web
Used Gobuster to find directories on the webserver
Gobuster Found:
-/panel/ as hidden directory
- Found out I could upload files to the /panel/ directory so decided to drop a php reverse shell.
- Got one from pentestmonkey(renamed it to .php5) github.link>>>>
(https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

## Exploitation
Visited /uploads to open the bomb(reverseshell file) and boom;
File upload was successful and I got a reverse shell to my listener on netcat

Upgraded the shell with python. Found user.txt

## Privilege esc
- searched for files with SUID permission set.. and found python in the results
- Used `GTFOBINS` for the needed python script to escalate my priv using that vulnera..

## Boom I got root access

## Takeaways
- Never skip info gathering phase, and always check for priv esc opportunities
