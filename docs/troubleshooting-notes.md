## Troubleshooting Notes — Virtualisation Lab
Project: CompTIA A+ Core 2 – Ubuntu Desktop on Oracle VirtualBox
Author: Andre Patterson
Date: June 2026
----------------------------------------------------------------------------------------------------------------------------------

## Issue #1 — Invalid Settings Detected / Mouse Cursor Not Visible
# Summary

After creating the VM and booting Ubuntu for the first time, the VirtualBox settings window displayed a warning and the mouse cursor was invisible inside the VM.

----------------------------------------------------------------------------------------------------------------------------------

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

3- Once Ubuntu booted, the mouse cursor was not visible inside the VM window — making it impossible to confirm whether clicks were registering or navigate the desktop reliably.

----------------------------------------------------------------------------------------------------------------------------------

# Investigation 

**Step 1 - Identified the warning source**
- Clicked the warning triangle icon at the bottom of the VirtualBox settings window. The tooltip pointed directly to the Display: Screen page as the source of the issue.


**Step 2 - Navigate to Display settings**
Went to:

- **Settings**  →  **Display**  →  **Screen**              



**Step 3 - Identified the misconfiguration**

- Found that the **Graphics Controller** was set to **VBoxVGA** - which had been selected by mistake during the initial VM setup.

----------------------------------------------------------------------------------------------------------------------------------

# Root Cause

The wrong graphics controller option was selecected during the initial VM configuration.

|      **Controller**         |               **Recommended For**            |                    **Why**                        |
|-----------------------------|----------------------------------------------|---------------------------------------------------|
|          VMSVGA             |        Linux guests (Ubuntu, Debian etc)     | Best performance and compatibility for Linux
|                             |                                              |
|         VBoxSVGA            |                 Windows guests               | Optimised for Windows display rendering
|                             |                                              |       
|          VBoxVGA            |              Legacy/older setups             | Outdated, causes display issues on modern guest OS
|                             |                                              |


Selecting **VBoxVGA** for a Ubuntu guest caused the display layer to malfunction, resulting in the missing mouse cursor and the invalid settings warning.

----------------------------------------------------------------------------------------------------------------------------------

# Fix Applied

**Settings**  →  **Display**  →  **Screen** → **Graphics Controller**

Changed: **VBoxVGA**  →  **VMSVGA**


Steps taken to apply fix:

1. Opened VM **Settings** from the VirtualBox Manager
2. Clicked **Display** in the left sidebar
3. Selected the **Screen** tab
4. Changed **Graphics Controller** dropdown from VBoxVGA to VMSVGA
5. Clicked **OK** to save
6. Restarted the VM

----------------------------------------------------------------------------------------------------------------------------------

# Result

After restarting the VM:

1- "Invalid settings detected" warning cleared
2-  Mouse cursor appeared correctly inside the Ubuntu VM
3-  Display rendered properly — full resolution and input working
4-  Ubuntu Desktop fully navigable

----------------------------------------------------------------------------------------------------------------------------------

# Lessons Learned

1 - **Ensure the graphics controller match the appropriate guest OS**
VirtualBox does not automatically enforce this - it has to be  manually configured what has a direct impact on how the VM renders display output.

2 - **The warning triangle is your first diagnostic tool**
VirtualBox's "Invalid settings detected" warning is specific - clicking the icon tells you exactly which settings page the problem is on. Ensure that you always read it before troubleshooting blindly.

3 - **Minor configuration errors have real usability consequences**
A single dropdown choice made the entire VM environment unreliable. In a real IT or cybersecurity environment, this kind of misconfiguration could delay work or be mistaken for a more serious hardware/software fault.


4 - **Restart after display setting changes**
Display controller changes don't always take effect until the VM is fully restarted — not just paused or saved.
