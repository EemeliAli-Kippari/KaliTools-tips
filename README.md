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
files/dirs
```
mv file /destination || move around
mv oldname newname || rename
rm || removes files
rmdir || removes a dir
rmdir -r || empties a dir and deletes it
touch filename || make file
cat >> filename || make file
echo "yourtexthere" > filename || make file
nano filename || will open the nano text editor
mkdir dirname
```
Download from internet
```
wget url || when downloading code from github use the "raw" page
```
Download/Send files from/to through SSH
```
scp user@userip:/from_dir/file /to_dir || download from another user
scp file.txt remote_username@10.10.0.2:/remote/directory || send file file.txt
```
## SSH
Make a connection
```
ssh user@ipofuser || will ask for a password
```
## FTP
make a connection
```
ftp <ip> || asks for user and password
get <filename>/* || downloads files
bye 
```
## NMAP
Basic scan to file
```
sudo nmap -sV --script vuln <ip> -o nmap.txt
```
## BINWALK
```
binwalk <filename> <filename> || opens files if they contain something
-e || extract known filetypes
-M || recursive scan
```
## STEGHIDE
```
steghide --info -p || display info and p for password
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
Crack FTP/SSH/login form and various other protocols
``` 
hydra -l <username> -P /usr/share/wordlists/rockyou.txt <ip> ssh -o<filename> || uppercase letter for the option you want to crack. SSH at the end for SSH cracking
hydra -l user -P p<path to wordlist> ftp://<ip> || for FTP cracking
hydra -l <username> -P <path to wordlist> <ip> http-post-form "/login:username=^USER^&password=^PASS^:F=<wrong psswd msg>" -V -o <filename> || verbose brute force a POST login form

More info: https://tryhackme.com/room/hydra
``` 

## Gobuster
Basic directory scan
```
gobuster dir -o gobuster.txt -u <url> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
```

## Priviledge escalation
Find suid programs
```
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```
