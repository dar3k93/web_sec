# Gobuster

#### dir mode
dir mode allows to enumerate website directories. 
```
gobuster dir -u http://<ip_address> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
Other useful flag:
-x: File extension(s) to search for
-k: Skip TLS certificate verification
-H: Specify HTTP headers, -H 'Header1: val1' -H 'Header2: val2'

#### dns Mode
dns mode allows to brute-force subdomains
```
gobuster dns -d mydomain.test -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
Other useful flag:
-c Show CNAME Records (cannot be used with '-i' option)
-i Show IP Addresses
-r Use custom DNS server

#### vhost mode
vhost mode allows to brute-force virtual hosts
```
gobuster vhost -u http://mydomain.test -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
