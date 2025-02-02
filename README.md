# Cybrary_IT
## Network module :
### Scan with `NMAP` :
1. `nmap -sn -n -oG - host/24 | awk '/Up$/{print $2}' > ip-list.txt`
    - sn → Ping scan only (no port scanning).
    - n → No DNS resolution (faster).
    - oG - → Output in grepable format .
    - Filtering for live (up) hosts using awk:
    Your awk command has a syntax issue, but it aims to extract only live hosts (Up status).
    Saving results to ip-list.txt.

### Scan with `MassScan` : **use it when you want to scan all serveice and ports*
1. No default ports to scan like Nmap, you should specify the -p <ports>
2. T arget hosts are ip adressess or simple range not DNS names .
3. `--banners`
   - Why Check Banners in a Mass Scan? <BR>
Service Fingerprinting – Identify what software and versions are running (e.g., Apache, OpenSSH, MySQL).
Vulnerability Discovery – Some banners reveal outdated or vulnerable services.
Misconfiguration Detection – Exposed banners may leak sensitive information.
Red Teaming & Pentesting – Helps in reconnaissance during security assessments.

4. In Masscan, the `--source-ports` option allows you to specify the source ports from which scan packets originate. This can help evade firewall rules, avoid detection, or comply with network policies.
5. `--source-ip`  : specify specific ip
6. **example command : masscan -p 80,443 192.168.1.0/24 --rate 10000 --source-ports 40000-50000**
### Scan with `NetCat` : 
1. `nc -nv -w 1 -z` :<br>
    - n → No DNS resolution (faster scanning).
    - v → Verbose output (shows connection results).
    - w 1 → Sets a 1-second timeout for connections.
    - z → "Zero-I/O mode" (just check if the port is open, no data is sent) / specifies a port scan.
    - u → UDP mode can be unreliable.
    - can be slow to scan but find things nmap doesn't.
2. `while read l ; do nc -nv -w 1 -z $l 80 ; done < ip-list.txt` : 
    - while read l → Reads each IP from ip-list.txt, storing it in variable $l.
    - nc nv -w 1 -z $l 80 → Uses Netcat to check if port 80 (HTTP) is open on the IP.
    - n → No DNS resolution (faster).
    - v → Verbose (shows connection status).
    - w 1 → 1-second timeout
    - z → Zero-I/O mode (just check if port is open, no data sent).
    done < ip-list.txt → Loops through the IPs from ip-list.txt.

### SMB Enumeration :
1. What is SMB?
   - Server Message Block (SMB) is a network protocol used for file sharing, printer sharing, and interprocess communication between devices on a network. It                 allows users and applications to read and write files and request services over a network.
2. How SMB Works :
   - SMB operates over TCP port 445 (modern versions) and allows a client to:
       - Access shared files and directories on a remote server.
       - Use networked printers.
       - Authenticate users via Active Directory in Windows environments.
       - Enable inter-process communication between applications.
3. SMB Versions :
 
           - SMBv1 (Legacy & Insecure):
               - Introduced in Windows 95.
               - Vulnerable to exploits like EternalBlue (MS17-010).
               - Disabled by default in modern Windows.
   
           - SMBv2 (Improved Performance & Security):
               - Introduced in Windows Vista & Server 2008.
               - Reduces the number of commands for efficiency.
               - More secure than SMBv1 but still lacks strong encryption.
   
           - SMBv3 (Enhanced Security & Performance):
               - Introduced in Windows 8 & Server 2012.
               - Supports encryption to prevent MITM attacks.
               - Faster data transfer and improved security features.
   
           - SMBv3.1.1 (Latest & Most Secure):
               - Introduced in Windows 10 & Server 2016.
               - Adds pre-authentication integrity for better security.
               - Strengthens encryption to prevent tampering.
4. SMB Enumeration Using Nmap :
   - Enumerate SMB Shares
     - `nmap -p 445 --script=smb-enum-shares <target>`
   - Enumerate SMB Users :
     - `nmap -p 445 --script=smb-enum-users <target>`
   - Enumerate SMB OS Version bash :
     - `nmap -p 445 --script=smb-os-discovery <target>`
   - Run All SMB Scripts bash :
     - `nmap -p 445 --script=smb* <target>`
       
### NFS Enumeration :
    1. NFS Enumeration (Network File System) :
        - NFS (Network File System) allows remote file sharing between systems, primarily in UNIX/Linux environments. 
        - Misconfigured NFS servers can expose sensitive files and allow unauthorized access.
    2. 
        




   
