# Cybersecurity Home Lab - Complete Project Guide

## 📖 About This Guide

This is a complete step-by-step guide showing how I built my cybersecurity home lab from scratch as a complete beginner.

**Time to complete:** 3-4 hours

**Difficulty:** Beginner

---

## 📋 Prerequisites

| Requirement | Details |
|-------------|---------|
| Computer | Windows/Mac/Linux with 8GB+ RAM |
| Storage | 60GB free space |
| Internet | To download files |
| Time | 3-4 hours |

---

## Phase 1: Setting Up Kali Linux

### Step 1: Install VirtualBox

1. Go to: https://www.virtualbox.org/wiki/Downloads
2. Download the version for your operating system
3. Install VirtualBox (click Next, Next, Install)

### Step 2: Download Kali Linux

1. Go to: https://www.kali.org/get-kali/#kali-virtual-machines
2. Download "Kali Linux VirtualBox" image (about 4-5 GB)
3. Wait for download to complete

### Step 3: Extract the Kali File

1. Right-click the downloaded file
2. Select "Extract Here" (using 7-Zip or WinRAR)
3. Wait for extraction (creates a folder with `.vbox` file)

### Step 4: Import Kali into VirtualBox

1. Open VirtualBox
2. Click "Add" (orange button)
3. Browse to the extracted folder
4. Select the `.vbox` file
5. Click "Open"

### Step 5: Enable Virtualization in BIOS (If Needed)

**If you get "AMD-V disabled" or "VT-x disabled" error:**

1. Restart your computer
2. Press F2, Del, or F10 during startup (depends on your computer)
3. Find "SVM Mode" (AMD) or "Intel Virtualization Technology" (Intel)
4. Change from Disabled → Enabled
5. Press F10 to Save and Exit

### Step 6: Start Kali Linux

1. In VirtualBox, click on Kali
2. Click the green "Start" button
3. Wait for boot (2-3 minutes)
4. Login with:
   - Username: `kali`
   - Password: `kali`

---

## Phase 2: Setting Up DVWA (Vulnerable Target)

### Step 7: Open Terminal in Kali

- Click the black terminal icon at the bottom of Kali desktop

### Step 8: Install Docker

```bash
sudo apt update
sudo apt install docker.io -y

When asked "Remove all Docker data?" → Select "No"

Step 9: Start DVWA Container
bash
sudo docker run -d -p 80:80 vulnerables/web-dvwa
Step 10: Verify DVWA is Running
bash
sudo docker ps
You should see a container with "vulnerables/web-dvwa"

Step 11: Access DVWA
Open Firefox (orange fox icon)

Go to: http://localhost

Click "Create/Reset Database"

Login with:

Username: admin

Password: password

Phase 3: Performing Attacks
Step 12: Set Security Level to Low
In DVWA left menu, click "DVWA Security"

Change to "low"

Click "Submit"

Step 13: Command Injection Attack
Click "Command Injection" on left menu

In the IP address box, type:

text
127.0.0.1; ls
Click "Submit"

Result: You will see directory listing (the server executed the ls command)

Step 14: SQL Injection Attack
Click "SQL Injection" on left menu

In User ID box, type:

sql
1' OR '1' = '1
Click "Submit"

Result: Multiple users appear in the result

Step 15: XSS Attack (Reflected)
Click "XSS (Reflected)" on left menu

In the text box, type:

html
<script>alert('XSS')</script>
Click "Submit"

Result: A popup appears saying "XSS"

Phase 4: Monitoring with Wireshark
Step 16: Install Wireshark
bash
sudo apt install wireshark -y
Step 17: Start Wireshark
bash
sudo wireshark
Step 18: Capture Attack Traffic
Select interface "lo" (loopback)

Click the blue shark fin to start capture

Go back to Firefox and perform Command Injection again (127.0.0.1; ls)

Return to Wireshark and click red square to stop

Step 19: Filter the Capture
In Wireshark filter bar, type:

text
http contains ";"
Press Enter

What you see: The HTTP request containing ; ls in the URL

Step 20: Take Screenshots
Capture these for documentation:

Command Injection input (127.0.0.1; ls before submit)

Command Injection output (directory listing)

Wireshark showing the attack packet

Phase 5: Monitoring with Docker Logs
Step 21: Get Container ID
bash
sudo docker ps
Step 22: Watch Real-Time Logs
bash
sudo docker logs -f <container_id>
Step 23: Perform Attack While Watching
In Firefox, perform SQL Injection

Look at the terminal - you will see the attack logged:

text
GET /vulnerabilities/sqli/?id=1%27+OR+%271%27%3D%271
Commands Reference Sheet
Task	Command
Start DVWA	sudo docker run -d -p 80:80 vulnerables/web-dvwa
Check DVWA status	sudo docker ps
Stop DVWA	sudo docker stop $(sudo docker ps -q)
Start Wireshark	sudo wireshark
Watch Docker logs	sudo docker logs -f $(sudo docker ps -q)
Command Injection	127.0.0.1; ls
SQL Injection	1' OR '1' = '1
XSS	<script>alert('XSS')</script>
Common Problems and Solutions
Problem	Solution
7-Zip extraction not working	Install 7-Zip, right-click → Extract Here
"AMD-V disabled" error	Enter BIOS (F2), enable SVM Mode, save with F10
DVWA stuck on setup page	Click "Create/Reset Database"
SQL Injection syntax error	Try 1' OR '1' = '1 instead
Snort/Suricata installation failed	Use Wireshark and Docker logs instead
What I Learned
Technical Skills
Virtual machine setup (VirtualBox)

BIOS configuration (enabling virtualization)

Basic Linux commands (sudo, docker, ls, cd)

Docker container deployment

Web application attacks (Command Injection, SQL Injection, XSS)

Network traffic analysis with Wireshark

Log monitoring with Docker logs

Soft Skills
Troubleshooting errors systematically

Knowing when to abandon tools that don't work

Documenting the entire process

Quick Start (One-Line Commands)
bash
# Start everything
sudo docker run -d -p 80:80 vulnerables/web-dvwa

# Then in Firefox:
http://localhost
# Login: admin / password

# Attack: 127.0.0.1; ls
# Attack: 1' OR '1' = '1
# Attack: <script>alert('XSS')</script>
Resources
Kali Linux

VirtualBox

DVWA on Docker Hub

Wireshark

Built with ☕ and persistence | June 2026

text

---

## How to Post This

1. Go to your GitHub repository: `https://github.com/swapnilingle2406/Cybersecurity-home-lab`

2. Click **"Add file"** → **"Create new file"**

3. Name it: `PROJECT-GUIDE.md`

4. Copy everything inside the code block above and paste it

5. Scroll down → Write commit message: `Added complete project guide`

6. Click **"Commit changes"**

---

## Update Your README.md

At the bottom of your README.md, add:

```markdown
## 📚 More Information

For a complete step-by-step guide, see [PROJECT-GUIDE.md](PROJECT-GUIDE.md)
