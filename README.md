### Virtualisation Lab – Ubuntu on VirtualBox
CompTIA A+ Core 2 | Independent Project | June 2026
-----------------------------------------------------------------------------------------------------------

A hands on virtualisation project where I deployed Ubuntu Desktop as a guest OS inside Oracle VirtualBox on a Windows 11 host machine. This project covers everything from planning system resources, to installation, to terminal-based verification, including a real troubleshooting scenario I ran into and resolved.

-----------------------------------------------------------------------------------------------------------

## Project Overview

Detail                       |                                Info 
___________________________________________________________________________
Host OS                      |                       Windows 11 Pro (64-bit)
Hypervisor                   |                     Oracle VirtualBox (Type 2)
Guest OS                     |                 Ubuntu Desktop 25.04 (Plucky Puffin)
RAM Allocated                |                                 6 GB
CPU Cores Allocated          |                                  3
Storage Allocated            |                                30 GB



##  What is Virtualisation?

Virtualisation is the technology that enables you to run separate operating systems inside your existing machine (such as a laptop) without needing extra hardware.

In this project I used a Type 2 **Hypervisor** (VirtualBox), which runs on top of my host OS (Windows 11). This creates an isolated environment called a Virtual Machine (VM), where I installed and ran Ubuntu Linux independently.

**Why this matters for cybersecurity:
**Running an isolated VM means I can test commands, configurations, and tools without risking my host system, exactly how security professionals build lab environments.

-----------------------------------------------------------------------------------------------------------

##   Step-by-Step Setup

# Step 1 — Check Host Machine Resources

Before installing anything, I checked my Windows 11 machine had enough resources to share with a VM.

What I checked:
- CPU: 3.30 GHz dual-core ✅
- RAM: 32 GB total ✅
- Free Disk Space: 1.86 TB available ✅
- Virtualisation enabled in BIOS: Yes ✅ (confirmed via Task Manager)

-----------------------------------------------------------------------------------------------------------

# Step 2 - Download Ubuntu ISO

I downloaded the Ubuntu Desktop ISO from the official site:
https://ubuntu.com/download/desktop

# Ubuntu 26.04 minimum system requirements:
- 2 GHz dual-core processor
- 6 GB RAM
- 25 GB storage

My host machine exceeded all of these, so I could safely allocate the minimum to the VM.

-----------------------------------------------------------------------------------------------------------

# Step 3 - Download and Install Oracle VirtualBox

I downloaded Oracle VirtualBox from:
- https://www.virtualbox.org/wiki/Downloads

VirtualBox is a free, open-source Type 2 hypervisor, meaning it installs like a normal application on top of your existing OS.

-----------------------------------------------------------------------------------------------------------

# Step 4 — Create the Virtual Machine

Inside VirtualBox I clicked New and configured:

Setting                      |                     Info 
___________________________________________________________________________
VM Name                      |                 dreUnbuntuVM
OS Type                      |                    Linux
OS Distribution              |                 Ubuntu(64-bit)
Base Memory                  |                 6000 MB (60 GB)
Number o fCPUs               |                      3
Disk Size                    |                    30 GB

I left Unattended Installation unticked to install Ubuntu manually and go through each step myself.

-----------------------------------------------------------------------------------------------------------

# Step 5 - Installing Ubuntu

With the ISO attached, I started the VM and followed the Ubuntu on-screen installer:

- Selected language and keyboard layout
- Chose installation type (standard)
- Set up username and password
- Completed installation and rebooted into Ubuntu Desktop

-----------------------------------------------------------------------------------------------------------

Step 6 - Verify the Setup via Terminal

Once inside Ubuntu, I opened the terminal and ran the following commands to confirm everything was working:

# Gain temporary root access
sudo bash

# Confirm who I'm logged in as
whoami
# Output: root

# Check for available system updates
sudo apt update

# Install available upgrades
sudo apt upgrade

# Print full system summary (OS info + hardware)
uname -a && lsb_release -a && sudo lshw -short

# Check IP address and subnet
ip -a

# Exit root mode
exit

# Confirm back to standard user
whoami
# Output: ubuntu
