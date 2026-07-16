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


### Step 9: Start DVWA Container

1. In the terminal, type:
```bash
sudo docker run -d -p 80:80 vulnerables/web-dvwa
```
2. Press Enter
3. Wait for the image to download (2-3 minutes)
4. You will see a long container ID (like `abc123def456...`)

---

### Step 10: Verify DVWA is Running

1. In the terminal, type:
```bash
sudo docker ps
```
2. Press Enter
3. You should see a container with "vulnerables/web-dvwa" in the list

---

### Step 11: Access DVWA in Firefox

1. Open Firefox (orange fox icon at the bottom of Kali desktop)
2. In the address bar, type:
```
http://localhost
```
3. Press Enter
4. Click "Create/Reset Database" button
5. Login with:
   - Username: `admin`
   - Password: `password`

---

### Step 12: Set Security Level to Low

1. In DVWA left menu, click "DVWA Security"
2. Change the dropdown to "low"
3. Click "Submit"

---

### Step 13: Perform Command Injection Attack

1. In DVWA left menu, click "Command Injection"
2. In the "Enter an IP address" box, type:
```
127.0.0.1; ls
```
3. Click "Submit"
4. You will see directory listing

---

### Step 14: Perform SQL Injection Attack

1. In DVWA left menu, click "SQL Injection"
2. In the "User ID" box, type:
```
1' OR '1' = '1
```
3. Click "Submit"
4. You will see multiple users displayed

---

### Step 15: Perform XSS Attack

1. In DVWA left menu, click "XSS (Reflected)"
2. In the text box, type:
```
<script>alert('XSS')</script>
```
3. Click "Submit"
4. A popup will appear

---

### Step 16: Install Wireshark

1. Open a new terminal
2. Type:
```bash
sudo apt install wireshark -y
```
3. When asked, select "Yes"

---

### Step 17: Start Wireshark

```bash
sudo wireshark
```

---

### Step 18: Capture Attack Traffic

1. In Wireshark, select "lo" (loopback interface)
2. Click the blue shark fin to start capture
3. Go to Firefox and perform Command Injection again (`127.0.0.1; ls`)
4. Click red square to stop capture

---

### Step 19: Filter and Find the Attack

In Wireshark filter bar, type:
```
http contains ";"
```
Press Enter

---

### Step 20: Take Screenshots

Capture these and save them:

| Filename | What to capture |
|----------|-----------------|
| cmd-injection-input.png | `127.0.0.1; ls` typed |
| cmd-injection-output.png | Directory listing result |
| sql-injection-input.png | `1' OR '1' = '1` typed |
| sql-injection-output.png | Multiple users displayed |
| xss-input.png | `<script>alert('XSS')</script>` typed |
| xss-output.png | Popup alert |
| wireshark-capture.png | Wireshark showing attack packet |

---

### Step 21: Watch Docker Logs

1. Get container ID:
```bash
sudo docker ps
```
2. Watch logs:
```bash
sudo docker logs -f <container_id>
```
3. Perform SQL Injection in Firefox
4. You will see the attack in the logs

---

## Commands Reference Sheet

| Task | Command |
|------|---------|
| Start DVWA | `sudo docker run -d -p 80:80 vulnerables/web-dvwa` |
| Check running containers | `sudo docker ps` |
| Start Wireshark | `sudo wireshark` |
| View Docker logs | `sudo docker logs -f $(sudo docker ps -q)` |

---

## Attack Payloads

| Attack | Payload |
|--------|---------|
| Command Injection | `127.0.0.1; ls` |
| SQL Injection | `1' OR '1' = '1` |
| XSS | `<script>alert('XSS')</script>` |

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| DVWA not loading | `sudo docker run -d -p 80:80 vulnerables/web-dvwa` |
| SQL Injection error | Try `1' OR '1' = '1` instead |
| Wireshark not capturing | Select "lo" interface |

---

**Your project is complete!** 🎉
