### Troubleshooting Notes — Virtualisation Lab
Project: CompTIA A+ Core 2 – Ubuntu Desktop on Oracle VirtualBox
Author: Andre Patterson
Date: June 2026
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Issue #1 — Invalid Settings Detected / Mouse Cursor Not Visible
# Summary

After creating the VM and booting Ubuntu for the first time, the VirtualBox settings window displayed a warning and the mouse cursor was invisible inside the VM.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Environment

|     **Detail**              |                 **Info**                     |
|-----------------------------|----------------------------------------------|
|Host OS                      |            Windows 11 Pro (64-bit)           |
|Hypervisor                   |          Oracle VirtualBox (Type 2)          |
|Guest OS                     |      Ubuntu Desktop 25.04 (Plucky Puffin)    | 
|Stage of setup               |         First boot after VM creation         |       


# Symptom

Two problems appeared at the same time:

1- A warning at the bottom of the VirtualBox settings window:
    "Invalid settings detected"

2- When clicking the warning icon, the tooltip read:
   "Display: Screen page — The virtual machine is configured to use a graphics controller other than the recommended one (VMSVGA). Please consider switching unless you have a reason to keep the currently selected graphics controller."

Once Ubuntu booted, the mouse cursor was not visible inside the VM window — making it impossible to confirm whether clicks were registering or navigate the desktop reliably.
