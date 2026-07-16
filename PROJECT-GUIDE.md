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

