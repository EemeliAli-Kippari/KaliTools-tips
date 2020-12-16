# KaliTools-tips
MY collection of commands to different tools in Kali Linux on my journey to learn it and try to hack tryhackme.com

## LINUX
update everything
```
sudo apt update --> sudo apt upgrade
sudo apt-get dist-upgrade || if backages are kept back
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
## NetCat
Listen on port 1234 at tun0 ip
```
nc -lkvnp 1234
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
put <filename> || upload files
bye 
```
## NMAP
Basic scan to file
```
sudo nmap -sV -O --script vuln <ip> -o nmap.txt || -sV probes ports, vuln finds vulnerabilities,-O for OS, -p to specify port ranges, sC default scripts
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
Upgrade meterpreter shell
```  
shell
script -qc /bin/bash /dev/null
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
hydra -l <username> -P /usr/share/wordlists/rockyou.txt <ip> http-post-form "/login:username=^USER^&password=^PASS^:F=<wrong psswd msg>" -V -o <filename>
```
SQL
```
hydra -L usernames.txt -P /usr/share/wordlists/rockyou.txt <ip>  mysql -s <port> -f
```
More info: https://tryhackme.com/room/hydra

## Gobuster
Basic directory scan
```
gobuster dir -o gobuster.txt -t 30 -u <url> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt
```
## WFUZZ
Fuzz directories, variables, file types...
```
wfuzz -c -z file,<wordlist> http://example.com/FUZZ || variable=FUZZ works as well
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
## MySQL
Cheatsheet at: https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3
SQLmap
```
sqlmap -u <url> --batch --dbms <db_type> || basic scan
```
--dump =     Dump the data within the database that the application uses
--dump-all = Dump the ENTIRE database

## PHP
Reverse shell at
```
/usr/share/webshells/php/php-reverse-shell.php
```
