# Cybersecurity Home Lab Setup Guide

## Prerequisites

- VirtualBox
- Kali Linux
- Docker
- Wireshark

## Lab Setup

### Install VirtualBox

Download and install VirtualBox.

### Install Kali Linux

Create a virtual machine and install Kali Linux.

### Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

### Run DVWA

```bash
docker run --rm -it -p 4280:80 vulnerables/web-dvwa
```

Open:

http://localhost:4280

### Start Wireshark

Capture traffic on the active network interface.

## Learning Goals

- Understand common web vulnerabilities
- Observe network traffic
- Practice attack simulation in a safe lab environment
