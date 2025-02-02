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


