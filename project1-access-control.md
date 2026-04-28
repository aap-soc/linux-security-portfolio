<img width="647" height="150" alt="image" src="https://github.com/user-attachments/assets/ee45ab4f-3487-4111-af23-2416f000667b" />#  Project 1: Linux Access Control & File Permission Security

##  Overview

This project demonstrates how Linux file permissions are used to secure sensitive data and enforce controlled access in a multi-user environment. The implementation focuses on reducing unauthorized access and aligning with security best practices relevant to SOC operations.

--------------------------------------------------------------------------------------------------------------------------

##  Objectives

* Enforce least privilege access control
* Prevent unauthorized access to sensitive files
* Manage user and group ownership securely
* Apply secure default permission settings

--------------------------------------------------------------------------------------------------------------------------

##  Implementation & Evidence

--------------------------------------------------------------------------------------------------------------------------

### 1. Creating a File with Restricted Access

```bash
touch secure.txt
chmod 600 secure.txt
ls -l
```

**Explanation:**

* Created a file with **owner-only access**
* Removed all permissions for group and others
* Verified permissions using `ls -l` → `-rw-------`

📸 <img width="647" height="150" alt="image" src="https://github.com/user-attachments/assets/ff4ec9f0-e677-4284-8648-a89b0b7eae62" />
 (secure file permissions)*

-----------------------------------------------------------------------------------------------------------------------------

### 2. Managing File Ownership

```bash
sudo useradd testuser
sudo chown testuser secure.txt
```

**Explanation:**

* Created a new user (`testuser`)
* Transferred file ownership using `chown`
* Demonstrates controlled delegation of file access

📸 *Add screenshot here (ownership change)*

--------------------------------------------------------------------------------------------------------------------------

### 3. Creating and Executing a Script

```bash
echo 'echo Hello, Linux!' > hello.sh
chmod +x hello.sh
./hello.sh
```

**Explanation:**

* Created a script and made it executable
* Demonstrates controlled execution permissions

📸 *Add screenshot here (script execution)*

--------------------------------------------------------------------------------------------------------------------------

### 4. Securing a Group-Shared Directory

```bash
mkdir shared_folder
chmod 770 shared_folder
ls -l
```

**Explanation:**

* Owner and group have full access
* No access for others
* Suitable for controlled team collaboration

📸 *Add screenshot here (directory permissions)*

--------------------------------------------------------------------------------------------------------------------------

### 5. Changing Group Ownership

```bash
sudo groupadd developers
sudo chown :developers secure.txt
```

**Explanation:**

* Assigned file to a group
* Enables controlled group-based access

📸 *Add screenshot here (group ownership)*

--------------------------------------------------------------------------------------------------------------------------
### 6. Removing Execute Permission

```bash
chmod -x hello.sh
ls -l
```

**Explanation:**

* Removed execution rights
* Prevents unauthorized script execution

📸 *Add screenshot here (permission removal)*

--------------------------------------------------------------------------------------------------------------------------

### 7. Setting Read-Only Permissions

```bash
chmod 444 secure.txt
```

**Explanation:**

* File becomes read-only for all users
* Prevents modification or deletion

📸 *Add screenshot here (read-only file)*

--------------------------------------------------------------------------------------------------------------------------

### 8. Applying Secure Defaults with umask

```bash
umask
umask 027
touch testfile.txt
ls -l testfile.txt
```

**Explanation:**

* Configured secure default permissions
* Ensures new files are not accessible to unauthorized users

📸 *Add screenshot here (umask result)*

--------------------------------------------------------------------------------------------------------------------------
### 9. Using Symbolic Permission Notation

```bash
touch file1.txt
chmod u=rw,g=r,o= file1.txt
ls -l file1.txt
```

**Explanation:**

* Applied granular permission control
* Equivalent to `chmod 640`

📸 *Add screenshot here (symbolic permissions)*

--------------------------------------------------------------------------------------------------------------------------
## 🔐 Security Analysis

### Principle of Least Privilege (PoLP)

Permissions are restricted so users only have the access necessary for their role.

### Data Exposure Prevention

* Sensitive files restricted using `600` and `640`
* Default permissions hardened using `umask 027`

### Attack Surface Reduction

Restricting file access limits what an attacker can view if a system is compromised.

--------------------------------------------------------------------------------------------------------------------------

## 🚨 SOC Scenario: Unauthorized File Access

### Scenario

An attacker gains access to a low-privileged account on a Linux system.

### Risk

If permissions are too open:

* Sensitive files (logs, configs) can be read
* Data exposure may occur

### Mitigation Implemented

* Restricted permissions (`chmod 600`, `640`)
* Secure defaults using `umask 027`
* Controlled group access

### SOC Relevance

* Reduces lateral movement opportunities
* Protects sensitive data from insider threats
* Supports secure system hardening

--------------------------------------------------------------------------------------------------------------------------

##  Pra Applications

* Securing authentication and system logs
* Protecting sensitive business data (e.g., payroll)
* Restricting access to configuration files

--------------------------------------------------------------------------------------------------------------------------

##  Key Takeaways

* File permissions are critical for system security
* Misconfigurations can lead to data breaches
* Secure defaults reduce risk automatically
* Access control is a foundational SOC security skill

--------------------------------------------------------------------------------------------------------------------------
