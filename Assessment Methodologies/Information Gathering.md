# Information Gathering

## Passive Information Gathering

- Website recon & footprinting
    - robots.txt
    - sitemap.xml
    - use add-ons like BuiltWith & Wappalyzer
    - whois enumeration - Whois target.com
    - whatweb target.com
    - Netcraft - netcraft.com
- dnsrecon
    - dnsrecon -d target.com
    - dnsdumpster.com
    - dig tryhackme.com MX
    - nslookup -type=A tryhackme.com 1.1.1.1
- WAF detection
    - wafw00f tool - it is preinstalled in Kali
    - usage - wafw00f target.com
- subdomain enumeration
    - sublist3r -d target.com -e google,yahoo
    - Amass
    - subfinder
    - crt.sh
    - You can check the usage of this tools ONLINE
- Google dorking
    - site:target.com
    - site:target.com inurl:admin
    - site:*.target.com
    - site:*.target.com intitle:admin
- Email Harvesting
    - tool → theHarvester
    - usage → theHarvester -d [target.com](http://target.com) -b google, linkedin
- Leaked Password Database
    - haveibeenpwned.com

## Active Information Gathering

- DNS Zone Transfer
    - tools → dnsenum & dig
    - usage → dnsenum zonetransfer.me
    - file - /etc/hosts
    - fierce -dns target.com
- Host Discovery with Nmap
    - usage → sudo nmap -sn <target IP>/24
- Port Scanning with Nmap
    - nmap -p <port numbers you want to scan> <target IP>
