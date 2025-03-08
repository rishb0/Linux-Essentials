# 🔐 **SSH Command **  

## 🖥️ **1. SSH Command Syntax**  
The basic structure of an SSH command:  
```bash
ssh [options] user@hostname
```  
📌 **Components:**  
- **ssh** → The command itself  
- **user** → Username of the remote system  
- **hostname** → IP address or domain of the remote system  
- **options** → Additional parameters (e.g., port, identity file)  

---

## 🌐 **2. Connecting to a Remote Server**  
### ✅ **Basic Connection**  
```bash
ssh user@remote_host
```  
➡️ Connects to the remote server as **user**  

### 📌 **Specify a Port**  
```bash
ssh -p 2222 user@remote_host
```  
➡️ Connects via port **2222** (instead of default **22**)  

### 🔑 **Using an Identity File (Private Key)**  
```bash
ssh -i /path/to/private_key user@remote_host
```  
➡️ Uses an **SSH private key** for authentication  

### ⚡ **Execute a Command on the Remote Server**  
```bash
ssh user@remote_host "ls -l"
```  
➡️ Runs the `ls -l` command remotely and displays output locally  

---

## 🔑 **3. SSH Key-Based Authentication**  
### 🔹 **Generate an SSH Key Pair**  
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```  
➡️ Creates a **4096-bit RSA** key pair  

### 📤 **Copy SSH Key to Remote Server**  
```bash
ssh-copy-id user@remote_host
```  
➡️ Enables **passwordless authentication**  

### ✍ **Manually Add Public Key**  
```bash
cat ~/.ssh/id_rsa.pub | ssh user@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```  
➡️ Manually appends the public key  

---

## 🔄 **4. SSH Tunneling & Port Forwarding**  
### 🔹 **Local Port Forwarding**  
```bash
ssh -L 8080:localhost:80 user@remote_host
```  
➡️ Forwards local port **8080** to remote port **80**  

### 🔹 **Remote Port Forwarding**  
```bash
ssh -R 9090:localhost:3000 user@remote_host
```  
➡️ Allows access to **localhost:3000** from remote host on **9090**  

### 🌍 **Dynamic Port Forwarding (SOCKS Proxy)**  
```bash
ssh -D 9090 user@remote_host
```  
➡️ Creates a SOCKS proxy on port **9090**  

---

## ⚙️ **5. SSH Config File for Easier Access**  
Save SSH settings for quick access in `~/.ssh/config`:  
```bash
Host myserver
    HostName remote_host
    User username
    Port 2222
    IdentityFile ~/.ssh/id_rsa
```  
➡️ Now you can connect with:  
```bash
ssh myserver
```  

---

## 📂 **6. Secure File Transfers (SCP & SFTP)**  
### 🔄 **Copy Files with SCP**  
```bash
scp file.txt user@remote_host:/path/to/destination
```  
➡️ Uploads `file.txt` to the remote server  

### 📁 **Copy a Directory**  
```bash
scp -r folder/ user@remote_host:/path/to/destination
```  

### ⬇️ **Download a File from Remote Server**  
```bash
scp user@remote_host:/path/to/file.txt .
```  

### 📡 **Using SFTP**  
```bash
sftp user@remote_host
sftp> put local_file.txt  # Upload file
sftp> get remote_file.txt # Download file
sftp> exit
```  

---

## 🚀 **7. Managing SSH Sessions**  
### 🛠️ **Keep Connection Alive**  
```bash
ssh -o ServerAliveInterval=60 user@remote_host
```  
➡️ Prevents SSH from **timing out**  

### ⚡ **Multiplexing SSH Connections (Faster SSH)**  
Add this to `~/.ssh/config` for **faster multiple SSH connections**:  
```bash
Host *
    ControlMaster auto
    ControlPath ~/.ssh/socket-%r@%h:%p
    ControlPersist 10m
```  

### 🎭 **Background SSH Sessions**  
```bash
ssh -f -N user@remote_host
```  
➡️ Runs SSH in **background mode**  

---

## ❌ **8. Closing SSH Connections**  
### 🔚 **Exit SSH Session**  
```bash
exit
```  
or  
```bash
Ctrl + D
```  

### ⚠️ **Kill a Stuck SSH Session**  
```bash
~.
```  
➡️ Instantly terminates the SSH session  

---
