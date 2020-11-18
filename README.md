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
ssh user@ipofuser -p <port>|| will ask for a password
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
sudo nmap -sV -sC -O --script vuln <ip> -o nmap.txt || -sV probes ports, vuln finds vulnerabilities,-O for OS, -p to specify port ranges, sC default scripts
```
## MASSCAN
Installation to masscan/bin
```
sudo apt-get install git gcc make libpcap-dev
git clone https://github.com/robertdavidgraham/masscan
cd masscan
make
```
## BINWALK
```
binwalk <filename> <filename> || opens files if they contain something
-e || extract known filetypes
-M || recursive scan
```
## STEGHIDE
```
steghide --info -p <filename> || display info and p for password
steghide extract -sf tryhackme.jpeg || extracts data inside
```

## Metasploit
Intialize database 
```
msfdb init
```
Start msf 
```
msfconsole
```
Check connection to db
```
db_status
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
sudo john --wordlist=/usr/share/wordlists/rockyou.txt <hashedfile> || first make a hashed file using zip2john
```  

Show earlier cracked
```
sudo john --show <hash-file>
``` 


## Hydra
Crack FTP/SSH/login form and various other protocols

SSH
``` 
hydra -l <username> -P /usr/share/wordlists/rockyou.txt <ip> ssh -o<filename>
```
FTP
```
hydra -l user -P p<path to wordlist> ftp://<ip>
```
Web login
```
hydra -l <username> -P <path to wordlist> <ip> http-post-form "/login:username=^USER^&password=^PASS^:F=<wrong psswd msg>" -V -o <filename>
```

More info: https://tryhackme.com/room/hydra

## Gobuster
Basic directory scan
```
gobuster dir -o gobuster.txt -t 30 -u <url> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
```

## Priviledge escalation
Find suid programs
```
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null || "2>/dev/null" = errors do not show
```
## Python
Turn a crappy reverse shell or similar into a better one
```
python -c 'import pty;pty.spawn("/bin/bash")'
```
Really simple http server on port 8K
```
python -m SimpleHTTPServer
```
