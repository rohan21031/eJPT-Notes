# SMTP

- port 25
    
- nmap -sV -script banner 192.80.153.3
    
- nc 25
    
    - VRFY [admin@openmailbox.xyz](mailto:admin@openmailbox.xyz)
    
    [![SMTP VRFY output 1](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smtp-01.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smtp-01.png) [![SMTP VRFY output 2](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smtp-02.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smtp-02.png) ￼
    
- `telnet <ip> 25`
    
    - `HELO attacker.xyz`
    
    [![SMTP HELO output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smtp-03.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smtp-03.png)
    
    - `EHLO attacker.xyz`
    
    [![SMTP EHLO output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smtp-04.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smtp-04.png) ￼
    
- send fake mail using telnet:
    
    - `HELO attacker.xyz`
    - `mail from: admin@attacker.xyz`
    - `rcpt to:root@openmailbox.xyz`
    
    ```
       data
       Subject: Hi Root
       Hello,
       This is a fake mail sent using telnet command.
       From,
       Admin
       . (dot)
    ```
    
- smtp-user-enum -U -t 192.80.153.3
    
- sendemail -f [admin@attacker.xyz](mailto:admin@attacker.xyz) -t [root@openmailbox.xyz](mailto:root@openmailbox.xyz) -s 192.26.29.3 -u Fakemail -m "Hi root, a fake from admin" -o tls=no
    

# Metasploit Module

- auxiliary/scanner/smtp/smtp_enum
- auxiliary/scanner/smtp/smtp_version

# Wordlists

- /usr/share/commix/src/txt/usernames.txt