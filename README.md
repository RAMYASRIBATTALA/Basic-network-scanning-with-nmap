# Basic-network-scanning-with-nmap
A basic network scanning project using Nmap to identify open ports, running services, and analyze potential security risks on a target system.

**1.First Scan**

Command:
**nmap 192.168.1.19**

Output:

135/tcp → open (msrpc)

139/tcp → open (netbios-ssn)

445/tcp → open (microsoft-ds)

Explanation:
This scan shows the **most common open ports** on the target system.

**Port 135 (MSRPC)**
  → Used for communication between Windows services.
  → Important for system processes.
  
 **Port 139 (NetBIOS Session Service)**
  → Used for file and printer sharing in older Windows systems.
  
 **Port 445 (Microsoft-DS / SMB)**
  → Used for **file sharing and network communication** in Windows.
  → Very important and also a **common attack target**.
  
 **Conclusion:**
The system is likely a **Windows machine** with file sharing enabled.

**2. Detailed Scan**

Command:
**nmap -sV 192.168.1.19**

Output adds:
* Microsoft Windows RPC
* NetBIOS service details
* OS detected: **Windows**

 Explanation:
This scan gives **extra details about services and versions**.
* Confirms services are running on **Microsoft Windows**
* Helps identify **exact service types**
* Useful for **security analysis and vulnerability detection**

 **Conclusion:**
Now you know:
* The OS is **Windows**
* Services are **official Microsoft services**

 **3. Full Port Scan (All Ports)**
 
Command:
**nmap -p- 192.168.1.19**

 New Ports Found:
* **137/tcp → filtered**
* **5040/tcp → open (unknown)**
* **7680/tcp → open (pando-pub)**
* **49664–49682 → open (unknown high ports)**

Explanation of New Findings:

 **1)137/tcp (filtered - netbios-ns)**
* Nmap cannot access it (blocked by firewall)
* Good sign → system has some protection

**2)5040/tcp (unknown)**
* Not a standard port
* Could be:
  * Custom application
  * Background Windows service
 
 **3)7680/tcp (pando-pub)**
* Used by **Windows Update Delivery Optimization**
* Helps share updates across network

 **4)49664–49682 (Dynamic Ports)**
* These are **ephemeral (dynamic) ports**
* Used temporarily by Windows services
* Common in modern Windows systems

 **Security Significance**
 Important Risks:
* **Port 445 (SMB)**
  → Can be used in attacks like ransomware (e.g., WannaCry)

* **Open unknown ports**
  → May expose hidden services

* **Multiple open ports**
  → Increases attack surface

**Final Conclusion**

* Target system is **Windows OS**
* Running **network sharing services (SMB, NetBIOS)**
* Has **multiple open ports including dynamic ports**
* Some ports are **filtered (firewall present)**
* System may be **vulnerable if not secured properly**



