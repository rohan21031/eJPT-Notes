# Enumeration
### Enumerating servers and services
##### ***Note: the 10.10.10.10 IP address is used as an example here and you can change it to your desired IP address.*** 
#### SSH
- Secure Shell
- port 22
- how to connect :- $ ssh root@10.10.10.10
- $ nc 10.10.10.10 22
- $ nmap 10.10.10.10 -p 22 --script ssh2-enum-algos  --> to check which algorithms is being used
- nmap 10.10.10.10 -p 22 --script ssh-hostkey --script-arg ssh_hostkey=full --> pull rsa host key
- check for weak passwords - $ nmap 10.10.10.10 -p 22 --script ssh-auth-methods --script-args="ssh.user=student" --> student can be admin or any user
- SSH Dictionary attack -- for poor passwords and poor misconfiguration
- $ hydra -l student -P /usr/share/passwordlists/rockyou.txt 
- $ nmap 10.10.10.10 -p 22 --script ssh-brute --script-args user=administrator ***or can be a list of users and can be specified by -- userdb=/root/users***
- we can also use Metasploit to perform a brute force 
- metasploit command --> use auxiliary/scanner/ssh/ssh_login -- configure the options and run

#### MySQL -- Windows version
- Nmap script fo MSSQL --> nmap 10.10.10.10 -p 1433 --script ms-sql-info 
- $ nmap 10.10.10.10 -p 1433 --script ms-sql-ntlm-info --script-args mssql.instance-port=1433
- $ nmap 10.10.10.10 -p 1433 --script ms-sql-brute --script-args userdb=< **users list path**>,password=< **pass list path**>
- check for empty passwords --> $ nmap 10.10.10.10 -p 1433 --script ms-sql-empty-password
-  $ nmap 10.10.10.10 -p 1433 --script ms-sql-query --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-query.query="SELECT * FROM master..syslogins" -oN output.txt
- $ $ nmap 10.10.10.10 -p 1433 --script ms-sql-dump-hashes --script-args mssql.username=admin,mssql.password=anamaria
- $ nmap 10.10.10.10 -p 1433 --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="ipconfig" --> running a command 
- Metasploit 
- $ use auxiliary/scanner/mssql/mssql_login  --> configure all options
- $ use auxiliary/admin/mssql/mssql_enum 
- $ use auxiliary/admin/mssql/mssql_enum_sql_logins
- $ use auxiliary/admin/mssql/mssql_exec -- set cmd whoami
- $ use auxiliary/admin/mssql/mssql_enum_domain_accounts
- For all the above Metasploit commands, do complete all the options that are required with a yes

#### SQL:
- $ nmap 10.10.10.10 -p 3306 --script=mysql-empty-password --> check the Nmap documentation for more scripts for MySQL
- $ mysql -h 10.10.10.10 -u root 
- once inside -- show databases 
- and then -- use books; 
- using Metasploit 
- use auxiliary/scanner/mysql/mysql_writeable_dirs
- use auxiliary/scanner/mysql/mysql_hashdump  --> another Metasploit auxiliary that can be used
- $ nmap 10.10.10.10 -p 3306 --script=mysql-empty-password
- dictionary attack using Metasploit --> use auxiliary/scanner/mysql/mysql_login
- or by hydra --> $ hydra -l root -P < **password list path**> 10.10.10.10 mysql

#### HTTP
- for hosting websites
- $ whatweb 10.10.10.10
- $ http 10.10.10.10
- $ dirb http://10.10.10.10
- $ browsh --startup-url http://10.10.10.10/Default.aspx  --> a good tool if you have access to just the terminal, it will help you see somehow the actual webpage
- Nmap scripts --> nmap 10.10.10.10 -sV -p 80 --script http-enum 
- $ nmap 10.10.10.10 -sV -p 80 --script http-headers
- $ nmap 10.10.10.10 -sV -p 80 --script http-methods --script-args http-methods.url-path=/webdav/
- the above commands are an example of how to enumerate an HTTP with Nmap Scripts 
- for Linux/Unix OS
- nmap 10.10.10.10 -p 80 -sV -script banner
- using Metasploit --> use auxuilary/scanner/http/http_version --> configure all options
- wget "http://10.10.10.10/index"  --> will download the webpage
- also browsh 
- Metasploit again --> use auxiliary/scabber/http/brute_dirbs 
- dirb http://10.10.10.10 <passwordlist path>
- robots.txt --> use auxiliary/scanner/http/robots_txt


