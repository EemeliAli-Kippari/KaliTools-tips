# KaliTools-tips
MY collection of commands to different tools in Kali Linux on my journey to learn it and try to hack tryhackme.com

## LINUX
update everything
```
sudo apt update --> sudo apt upgrade
```
move in terminal
```
cd +
/ = root
.. = one dir back
- = previous dir
```
make files
```
touch filename
cat >> filename
echo "yourtexthere" > filename
nano filename || will open the nano text editor
```
make a dir
```
mkdir dirname
```
remove
```
rm || removes files
rmdir || removes a dir
rmdir -r || empties a dir and deletes it
```

## SSH
Make a connection
```
ssh user@ipofuser || will ask for a password
```

## NMAP
Basic scan to file
```
sudo nmap -sV --script vuln <ip> -o nmap.txt
```

## Metasploit
Intialize database 
```
msfdb init
```
Update
```
msfupdate
```
Check connection to db
```
db_status
```

Start msf 
```
msfconsole
```

Set RHOSTS globally
```
setg RHOSTS <ip>
```
Set LHOSTS
```
set LHOSTS <yourownip>
```
Search module, payload for it & set
```
search <module>
show payloads
set PAYLOAD payload/path
```  

## Hashcat
Crack MD5 hash with username (username: hash)
```
hashcat --username -a 0 -m 0 <hash-file> <path-to-wordlist>
```

Show earlier cracked
```
hashcat --username --show -a 0 -m 0 <hash-file> <path-to-wordlist>
```  

## John the ripper
Crack hash
```
sudo john <hash-file>
```  

Show earlier cracked
```
sudo john --show <hash-file>
```  

## Hydra
Crack FTP login
``` 
hydra -l <username> -P /usr/share/wordlists/rockyou.txt <ip> <ftp/ssh>
``` 

## Gobuster
Basic directory scan
```
gobuster dir -o gobuster.txt -u <url> -w <path-to-wordlist>
```

## Priviledge escalation
Find suid programs
```
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```
