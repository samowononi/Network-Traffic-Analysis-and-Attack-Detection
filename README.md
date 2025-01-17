# **Network Traffic Analysis and Attack Detection**

## **Overview**  
This analysis investigates an unauthorized access attempt and subsequent data exfiltration captured in a network packet analysis using Wireshark. The incident involves a brute-force attack to gain unauthorized server access and the retrieval of sensitive data.

---

## **Capture 1: Unauthorized Access and Data Exfiltration**

### **Timeline of Events**

#### **Step 1: Legitimate User Activity**
- **Packet Range**: [10, 71]  
- **Details**: A legitimate user (`192.168.56.102`) successfully logs into the server (`192.168.56.101`) via FTP using the credentials:  
  - **Username**: `ftpuser`  
  - **Password**: `cmpsem055`  
- The user uploads a file named `Confidential Information.doc`.

**Screenshot Placeholder**: Successful login and file upload captured in Wireshark.

---

#### **Step 2: Suspicious Activity Initiation**
- **Packet**: [86]  
- **Details**: Approximately 15.5 seconds later, a TCP connection attempt originates from a different IP address (`192.168.56.1`).  
- The connection succeeds, but the server logs a **500 Internal Server Error** and prompts for login credentials.

**Screenshot Placeholder**: TCP connection attempt from `192.168.56.1` and server error log.

---

#### **Step 3: Brute-Force Attack**
- **Packet Range**: [105 - 14143]  
- **Details**: The user (`192.168.56.1`) initiates a **password brute-force attack** over a period of 42.11 minutes, attempting numerous passwords using a dictionary list.  
  - **First 3 Passwords**: `aaa`, `abc`, `academia`  
  - **Last 3 Passwords**: `root`, `backup`, `cmpsem055`  
- The attack successfully retrieves the correct password, `cmpsem055`.

**Screenshot Placeholder**: Brute-force attempts and successful login.

---

#### **Step 4: Unauthorized File Retrieval**
- **Packet**: [14222]  
- **Details**: After gaining access, the attacker navigates to the directory containing the confidential document.  
  - **Request**: `RETR Confidential Information.doc`  
  - **Response**: `226 File send OK.`  
- The attacker successfully downloads the file.

**Screenshot Placeholder**: File retrieval request and response.

---

### **Findings**
1. The capture reveals a **potential unauthorized access** and **data exfiltration attempt**.  
2. The attacker employs a **brute-force attack** to bypass authentication mechanisms.  
3. The sensitive document `Confidential Information.doc` is successfully retrieved, as it was not encrypted.

**Screenshot Placeholder**: Summary of findings in Wireshark (e.g., filtered view of key events).

---

### **Recommendations**

1. **Stronger Password Policies**  
   - Enforce complex password requirements (e.g., minimum length, special characters).  
2. **Monitoring and Logging**  
   - Regularly review logs for unusual patterns like repeated failed login attempts.  
3. **Two-Factor Authentication (2FA)**  
   - Add an additional layer of security to prevent unauthorized access.  
4. **Data Encryption**  
   - Encrypt sensitive documents to protect their content even if unauthorized access occurs.

---

### **Additional Notes**

- **Other Files on the Server**:  
  - `memo`: Contains the text, "this is a memo to remind all users not to share their passwords."  
  - `1.png`: An image of a skull and crossbones in white color.  
- **Content of `Confidential Information.doc`**:  
  - "This file contains confidential information and should not be distributed."

**Screenshot Placeholder**: Details of other files and their content as displayed in Wireshark.

---

## **Conclusion**  
This analysis highlights the critical importance of proactive security measures, such as password management, activity monitoring, and data encryption, in safeguarding sensitive information against unauthorized access and potential breaches.
