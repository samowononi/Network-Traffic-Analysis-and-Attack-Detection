![Network Traffic Analysis and Attack Detection](https://github.com/user-attachments/assets/c8d69752-8cee-470a-a427-bc3091a5ae90)


# **Network Traffic Analysis and Attack Detection**

## **Overview**  

This project demonstrates the identification and documentation of malicious network activity using packet capture (PCAP) files and Wireshark. This analysis investigates two separate captures highlighting distinct attack scenarios, providing insights into the methods employed by attackers and the necessary defenses to counteract such threats.  

- **Capture 1** focuses on **unauthorized access and data exfiltration**, where an attacker employs brute-force techniques to compromise credentials and retrieve a sensitive document from the target server.  
- **Capture 2** delves into a **potential Denial-of-Service (DoS) attack** and a **brute-force password cracking attempt**, showcasing how attackers attempt to disrupt services and gain unauthorized access to critical systems.   

This project shows the importance of network monitoring and traffic analysis in detecting and responding to cyber threats and also serves as a practical demonstration of applying cybersecurity principles to real-world scenarios.

---

## **Capture 1: Unauthorized Access and Data Exfiltration**

### **Timeline of Events**

#### **Step 1: Legitimate User Activity**
- **Packet Range**: [10 - 71]  
- **Details**: A legitimate user (`192.168.56.102`) successfully logs into the server (`192.168.56.101`) via FTP using the credentials:  
  - **Username**: `ftpuser`  
  - **Password**: `cmpsem055`  
- The user uploads a file named `Confidential Information.doc`.

<img width="787" alt="Screenshot 2025-01-17 182112" src="https://github.com/user-attachments/assets/11075e3d-ee10-465e-8bc6-a4dac3bd5400" />

Successful login and file upload captured in Wireshark.

---

#### **Step 2: Suspicious Activity Initiation**
- **Packet Range**: [86 - 100]  
- **Details**: Approximately 15.5 seconds later, a TCP connection attempt originates from a different IP address (`192.168.56.1`).  
- The connection succeeds, but immediately, the server logs a **500 Internal Server Error** and prompts for login credentials.

<img width="791" alt="Screenshot 2025-01-17 182847" src="https://github.com/user-attachments/assets/44604ead-f61d-469f-a9b7-640386cf6206" />

TCP connection attempt from `192.168.56.1` and server error log.

---

#### **Step 3: Brute-Force Attack**
- **Packet Range**: [105 - 14143]  
- **Details**: The user (`192.168.56.1`) initiates a **password brute-force attack** over a period of 42.11 minutes, attempting numerous passwords using a dictionary list.  
  - **First 3 Passwords**: `aaa`, `abc`, `academia`  
  - **Last 3 Passwords**: `root`, `backup`, `cmpsem055`  
- The attack was successfull with the correct password, `cmpsem055`.

<img width="789" alt="Screenshot 2025-01-17 183752" src="https://github.com/user-attachments/assets/13a1baf3-1d8c-41f1-b4e1-c85984031fdf" />

Start of Brute-force attack.
<br>

<img width="788" alt="Screenshot 2025-01-17 184531" src="https://github.com/user-attachments/assets/cee9116c-9414-4efc-85dd-6ea80721f6f1" />

Successful login.

---

#### **Step 4: Unauthorized File Retrieval**
- **Packet**: [14222]  
- **Details**: After gaining access, the attacker navigates to the directory containing the confidential document.  
  - **Request**: `RETR Confidential Information.doc`  
  - **Response**: `226 File send OK.`  
- The attacker successfully retrieves the file.

<img width="791" alt="Screenshot 2025-01-17 185509" src="https://github.com/user-attachments/assets/fb617981-91dd-4d44-9b5f-4b652f044319" />

File retrieval request and response.

---

### **Findings**
1. The capture reveals an **unauthorized access** and **data exfiltration attempt**.  
2. The attacker employs a **brute-force attack** to bypass authentication mechanisms. 
3. The sensitive document `Confidential Information.doc` is successfully retrieved, as it was not encrypted.
4. The FTP protocol sends credentials (USER and PASS) in plaintext, which makes it vulnerable to interception.


---

### **Recommendations**

1. **Stronger Password Policies:** Enforce complex password requirements (e.g., minimum length of 8, special characters).  
2. **Monitoring and Logging:** Regularly review logs for unusual patterns like repeated failed login attempts.  
3. **Two-Factor Authentication (2FA):** Add an additional layer of security to prevent unauthorized access.  
4. **Data Encryption:** Encrypt sensitive documents to protect their content even if unauthorized access occurs.

---

### **Additional Notes**
Using the Export FTP-DATA Object List, there are two more files on the analyzed network traffic.
<img width="557" alt="Screenshot 2025-01-17 193844" src="https://github.com/user-attachments/assets/76690a22-a368-43ab-b363-c1b761b0bb74" />


- **Other Files on the Server**:  
  
  1. `1.png`: A png image of a skull and crossbones in white color.

  ![1](https://github.com/user-attachments/assets/ec2484cb-3e56-44b0-9bea-2aacc1fa98c9)
  ![Screenshot 2025-01-17 191811](https://github.com/user-attachments/assets/57f3f8bb-eaf8-4926-b3a4-32a13c8ca0e9)


    
  2. `memo`: Contains the text, "this is a memo to remind all users not to share their passwords."
 
  <img width="433" alt="Screenshot 2025-01-17 195320" src="https://github.com/user-attachments/assets/cf79ee8e-c5d3-40c8-88a9-c7f6119f3ac7" />

  <img width="789" alt="Screenshot 2025-01-17 191942" src="https://github.com/user-attachments/assets/6b668b90-1d24-4da8-a9e1-682eedd20da6" />
  

 
  
- **Content of `Confidential Information.doc`**:  
  - "This file contains confidential information and should not be distributed."
 
  <img width="461" alt="Screenshot 2025-01-17 195547" src="https://github.com/user-attachments/assets/5658a226-b0ef-44d6-865e-12c198799ddc" />

---

## **Conclusion**  
This analysis highlights the critical importance of proactive security measures, such as password management, activity monitoring, and data encryption, in safeguarding sensitive information against unauthorized access and potential breaches.


---
---

# **Capture 2: Potential Denial-of-Service (DoS) and Brute-Force Attack**

## **Overview**  
This analysis focuses on identifying and documenting a potential DoS attack and brute-force password cracking attempt captured in a network packet analysis.

---


### **Timeline of Events**

#### **Step 1: Potential DoS Attack**  
- **Packet Range**: [32 - 88]  
- **Details**:  
  - The attacker (`192.168.56.1`) initiates a potential **SYN flood attack** (half-open attack) against the target (`192.168.56.102`).  
  - SYN packets are sent in rapid succession, overwhelming the target system with incomplete connection requests, a common tactic in DoS attacks.

**Screenshot Placeholder**: SYN flood packets as displayed in Wireshark.  

---

#### **Step 2: Brute-Force Password Cracking**  
- **Packet Range**: [138 - 81188]  
- **Details**:  
  - The attacker continues their malicious activity with a **brute-force attack** against the target server.  
  - Numerous password attempts are made systematically to gain unauthorized access.  
  - Example passwords captured in the data include:  
    - **First 3**: `eeeeeeee`, `eeeeeeei`, `eeeeeeeo`  
    - **Last 3**: `eeeeeESU`, `eeeeeESm`, `eeeeeESM`

**Screenshot Placeholder**: Brute-force password attempts shown in Wireshark.

---

### **Findings**  

1. **Denial-of-Service (DoS) Activity**  
   - The SYN flood attack observed in this capture is an attempt to overwhelm the target server's resources with incomplete TCP connections.  

2. **Brute-Force Password Attack**  
   - The attacker systematically attempts various passwords in an attempt to gain unauthorized access to the target server.  

**Screenshot Placeholder**: Summary of findings in Wireshark (e.g., filtered views of DoS and brute-force attack patterns).

---

### **Recommendations**  

1. **Mitigation of DoS Attacks**  
   - Implement mechanisms to detect and mitigate DoS attacks, such as:  
     - Rate limiting for incoming connection requests.  
     - SYN cookies to handle half-open connections more effectively.  
     - Traffic filtering to block malicious IPs.  

2. **Enhanced Password Policies**  
   - Enforce strong password requirements, including:  
     - Minimum length (e.g., 12+ characters).  
     - Complexity (e.g., mix of uppercase, lowercase, numbers, and special characters).  
     - Account lockout after a limited number of failed login attempts.  

3. **Two-Factor Authentication (2FA)**  
   - Add 2FA for all login mechanisms to enhance security against brute-force attacks.  

---

## **Conclusion**  
This analysis highlights the significance of robust defenses against DoS and brute-force attacks, including preventive measures such as rate limiting, password policy enforcement, and multi-factor authentication.  

**Screenshot Placeholder**: Include relevant screenshots from Wireshark showing the SYN flood and brute-force patterns.  

