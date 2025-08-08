# 🐝 **Creating a Honeypot on VirtualBox using a Virtual Machine**

**`virtualbox-honeypot-setup`**

> Simulate and deploy a basic honeypot environment using VirtualBox and an open-source honeypot tool like **Cowrie**, **Dionaea**, or **Kippo** on a Linux virtual machine.

---

## 🗂 Recommended GitHub Repo Structure

```
virtualbox-honeypot-setup/
├── README.md
├── images/
│   ├── virtualbox-network-settings.png
│   ├── honeypot-running.png
│   └── attacker-connection.png
├── Honeypot_Setup_Guide.md
├── Skills_Learned.md
├── Troubleshooting.md
├── test-logs/
│   └── sample-log.txt
└── LICENSE
```

---

## 📄 README.md (Main Repo Page)

```md
# 🐝 Deploying a Honeypot on VirtualBox

This project demonstrates how to create a basic honeypot using **VirtualBox** and a **Linux virtual machine**, simulating attacker behavior in a controlled lab environment.

---

## 🎯 Objectives

- Deploy a honeypot using Cowrie (or Dionaea/Kippo).
- Configure networking to allow external or simulated attack traffic.
- Collect and analyze basic log data.
- Practice threat detection and forensic review.

---

## 🛠 Requirements

- Oracle VirtualBox (latest version)
- At least one Linux-based VM (Ubuntu Server recommended)
- Basic understanding of networking and Linux commands

---

## 🔐 What is a Honeypot?

A **honeypot** is a decoy system or service that mimics a real target to attract cyber attackers. It allows monitoring of attacker behavior without risking production systems.

---

## 🧱 Tools Used

- **Cowrie Honeypot** – Medium interaction SSH and Telnet honeypot
- **Ubuntu Server VM** – Lightweight and easy to configure
- **VirtualBox** – Hypervisor for VM management
- **Python3**, **Git**, **Virtualenv**

---

## 🧰 Setup Steps

See [Honeypot_Setup_Guide.md](Honeypot_Setup_Guide.md) for full step-by-step instructions.

---

## 📁 Logs

Sample test logs from a honeypot session are provided in `/test-logs/sample-log.txt`.

---

## 🧠 Skills Learned

See [Skills_Learned.md](Skills_Learned.md)

---

## 🧯 Troubleshooting

See [Troubleshooting.md](Troubleshooting.md) for firewall, permission, and startup errors.

---

## 🧑‍💻 Author

Matthew Beckles  
CompTIA Security+ | Associate in Cybersecurity | Wilmington University

---

## 🧠 `Skills_Learned.md`

```md
# 💡 Skills Learned from Building the Honeypot Lab

## 🧠 Technical Skills
- **Linux Server Administration**
  - Package management (apt)
  - User/SSH configuration
- **Network Configuration in VirtualBox**
  - Bridged Adapter vs NAT vs Internal Networking
- **Honeypot Deployment**
  - Cowrie installation via GitHub and virtual environments
  - Working with SSH and Telnet emulation
- **Security Monitoring**
  - Analyzing attacker behavior
  - Reviewing logs for forensic evidence
- **Scripting & Automation**
  - Using shell scripts to manage services and setup

## 🔍 Cybersecurity Skills
- Understanding of attacker TTPs
- Logging and log review using log files
- Safe cyber deception tactics in a controlled lab
- Incident response mindset

## 📄 Documentation & Reporting
- Writing setup and troubleshooting guides
- Organizing evidence and output for GitHub sharing
```

---

## 🧰 `Honeypot_Setup_Guide.md`

````md
# 🛠 Honeypot Setup Guide: Cowrie on Ubuntu Server

## Step 1: VM Setup

- Create a new VM in VirtualBox
  - OS: Ubuntu (64-bit)
  - Memory: 2GB
  - Disk: 20GB dynamically allocated
  - Network: **Bridged Adapter** (for attacker access from host or LAN)

## Step 2: Install Ubuntu Server

- Minimal installation
- OpenSSH Server enabled

## Step 3: Update & Install Dependencies

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3 python3-pip python3-venv libssl-dev libffi-dev build-essential -y
````

## Step 4: Clone Cowrie and Set Up Virtualenv

```bash
git clone https://github.com/cowrie/cowrie.git
cd cowrie
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Step 5: Configure Cowrie

```bash
cp etc/cowrie.cfg.dist etc/cowrie.cfg
nano etc/cowrie.cfg
# Modify port and hostname if desired
```

## Step 6: Start the Honeypot

```bash
bin/cowrie start
```

## Step 7: View Logs

```bash
tail -f var/log/cowrie/cowrie.log
```

---

## 🧪 Test Access

From another VM or your host:

```bash
ssh root@<honeypot-ip>
```

Use common credentials like `admin/admin` or `root/toor` and watch Cowrie log the attempt.

---

## 🔒 Note

This setup is for educational purposes **only** and should **not be exposed to public networks**.

````

---

## 🧯 `Troubleshooting.md`

```md
# 🚑 Honeypot Troubleshooting Tips

## Cowrie Won’t Start

- Check logs in `cowrie/var/log/cowrie/cowrie.log`
- Ensure no other services are using the ports (e.g., port 22)
- Disable system SSH if running on the same port

## Network Not Working

- Make sure VM network adapter is set to **Bridged** or **Internal**
- Use `ip a` or `ifconfig` to verify IP
- Check firewall (ufw)

## Logs Not Generating

- Ensure Cowrie is started: `bin/cowrie status`
- Check permissions for `var/log/cowrie/`
- Verify users are attempting login to the honeypot IP

## Can’t SSH into Honeypot

- Confirm it’s running on non-standard port (default is 2222)
- Try: `ssh root@<ip> -p 2222`

## VM Performance Slow

- Increase RAM to 2GB
- Use minimal installation
````
