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
dpkg -i [file] || dpkg is a tool to install, build, remove and manage Debian package. -i = install
lsb_release -a || show the Ubuntu version
```
Download from internet
```
wget url || when downloading code from github use the "raw" page
```
Different DNS and IP lookup tools
```
whois
dig
nslookup
host
tracert/traceroute
shodan
```
Download/Send files from/to through SSH
```
scp user@userip:/from_dir/file /to_dir || download from another user
scp file.txt remote_username@10.10.0.2:/remote/directory || send file file.txt
```
Grep
```
grep "[word]" [file] || search a line in a file with the [word] in it
-v || invert the results = show everything but the matches
-r || search recursively
```
## NetCat
Listen on port 1234 at tun0 ip
```
nc -lkvnp 1234

nc -vl 4444 > name_the_file_to_anything

nc -n [targetIP] 4444 < /path/to/file/you/want/to/send
```
Send files through nc
```
nc -vl 4444 > name_the_file_to_anything

nc -n [targetIP] 4444 < /path/to/file/you/want/to/send
```
##Nessus
```
sudo /bin/systemctl start nessusd.service || start nessus
localhost:8834 || user interface
```
## SSH
Make a connection
```
ssh user@ipofuser -p <port>|| will ask for a password
```
Good to know
```
-i [file] option gives the identity file, used for example to sign in using SSH keys
```
```
id_rsa and id_rsa.pub are default names of SSH private- and public keys
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
sudo nmap -sV -O --script vuln <ip> -oN nmap.txt || -sV probes ports, vuln finds vulnerabilities,-O for OS, -p to specify port ranges, sC default scripts, -A for OS detection, version detection, script scanning, and traceroute, -p- for all ports
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
## STEGCRACK
```
stegcrack <filename> || automatically runs rockyou.txt against a file
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

Options
```
-t number of paraller connections
-l user
-P password path
```

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
File search
```
gobuster dir -u <url> -x php -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -o gobuster.txt  
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
Check your sudo rights
```
sudo -l
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
## SQL
Cheatsheet at: https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3
MySQL versions 5.X and earlier are suspectible to user account and table enumeration. Metasploit has mysql_sql module with "show databases" sql option.

MYSQL
```
mysql -h [IPaddress] -u [username] -p || asks fro password
```
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

## NFS
Mount a NFS share to tmp
```
sudo mount -t nfs [IP]:[share name] /tmp/mount/ -nolock || mounting needs to be done to access a nfs share
```
Find out a name of a nfs share
```
/usr/sbin/showmount -e [IP]  || find out a name of a nfs share
```
## YARA
Yara is tool to analyze malware for example. It is based on a rule system, which are its arguments and they have boolean conditions inside them. It analyzes strings and binaries.

```
yara [rule_file] [file/dir] || basic syntax to run a yara rule
```

## SPLUNK
```
splunk.exe remove app [appname] -auth splunk-[username]:splunk-[password]|| remove an app on Windows
```
```
net stop splunkd || stop splunk on Windows
```
```
net start splunkd || start splunk on Windows
```

## GHOSTSCRIPT
repairs broken files
```
gs \ -o repaired.pdf \ -sDEVICE=pdfwrite \ -dPDFSETTINGS=/prepress \ corrupted.pdf || Repairs a broken pdf file
 ```
## USEFUL LINKS
https://dnsdumpster.com/
https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06
https://www.shodan.io/
https://excalidraw.com/
https://opintel.net/
https://dnstwister.report/
https://dnstwist.it/
