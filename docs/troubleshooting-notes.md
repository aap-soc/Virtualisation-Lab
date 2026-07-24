## Troubleshooting Notes - Virtualisation Lab
Project: CompTIA A+ Core 2 -  Ubuntu Desktop on Oracle VirtualBox
Author: Andre Patterson
Date: June 2026
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Issue #1 - Invalid Settings Detected / Mouse Cursor Not Visible
# Summary

After creating the VM and booting Ubuntu for the first time, the VirtualBox settings window displayed a warning and the mouse cursor was invisible inside the VM.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Environment

|     **Detail**              |                 **Info**                     |
|-----------------------------|----------------------------------------------|
|Host OS                      |            Windows 11 Pro (64-bit)           |
|Hypervisor                   |          Oracle VirtualBox (Type 2)          |
|Guest OS                     |      Ubuntu Desktop 25.04 (Plucky Puffin)    | 
|Stage of setup               |         First boot after VM creation         |       


# Symptoms  

Two problems appeared at the same time:

1- A warning at the bottom of the VirtualBox settings window:
    "Invalid settings detected"

2- When clicking the warning icon, the tool tip read:
   "Display: Screen page -  The virtual machine is configured to use a graphics controller other than the recommended one (VMSVGA). Please consider switching unless you have a reason to keep the currently selected graphics controller."

3- Once Ubuntu booted, the mouse cursor was not visible inside the VM window- making it impossible to confirm whether clicks were registering or navigate the desktop reliably.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Investigation 

**Step 1 - Identified the warning source**
- Clicked the warning triangle icon at the bottom of the VirtualBox settings window. The tool tip pointed directly to the Display: Screen page as the source of the issue.

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/cf278f87784b176b3416c05e61d0dffdf59fb2bd/20-troubleshooting-3%20(1).png)


**Step 2 - Navigate to Display settings**
Went to:

- **Settings**
  
![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/cf278f87784b176b3416c05e61d0dffdf59fb2bd/18-troubleshooting-1.png)


  
-   **Display** and select the  **Screen** tab 

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/cf278f87784b176b3416c05e61d0dffdf59fb2bd/20-troubleshooting-3.png)


-            



**Step 3 - Identified the misconfiguration**

- Found that the **Graphics Controller** was set to **VBoxVGA** - which had been selected by mistake during the initial VM setup.

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/20-troubleshooting-3.png)






--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


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

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Fix Applied

1. Selected **Settings**

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/18-troubleshooting-1.png)

   
1a. Then selected the **Display** option and then the **Screen** tab - with the **invalid settings detected**  message displayed 

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/20-troubleshooting-3.png)



2. Clicked on the dropdown arrow on **Graphics Controller** option and changed from **VBoxVGA**  to **VMSVGA**

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/21-troubleshooting-4.png)



# Steps taken to apply fix:

1. Opened VM **Settings** from the VirtualBox Manager
2. Clicked **Display** in the left sidebar
3. Selected the **Screen** tab
4. Changed **Graphics Controller** dropdown from VBoxVGA to VMSVGA
5. Clicked **OK** to save
6. Restarted the VM

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Result

After restarting the VM:

1. "Invalid settings detected" warning no longer displayed
   
   ![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/21-troubleshooting-4.png)
   
   
2. Mouse cursor appeared correctly inside the Ubuntu VM

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/VMSVGA%20config%20FIX-%20mouse%20cursor%20displaying.png)



3. Display rendered properly leading to full resolution and input working and Ubuntu Desktop fully navigable

![image alt](https://github.com/aap-soc/Virtualisation-Lab/blob/e5d369aa3e368ec7409b21e4e7acb8fedbad84b6/12-terminal-verify-1.png)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Lessons Learned

1 - **Ensure the graphics controller match the appropriate guest OS**
VirtualBox does not automatically enforce this - it has to be  manually configured what has a direct impact on how the VM renders display output.

2 - **The warning triangle is your first diagnostic tool**
VirtualBox's "Invalid settings detected" warning is specific - clicking the icon tells you exactly which settings page the problem is on. Ensure that you always read it before troubleshooting blindly.

3 - **Minor configuration errors have real usability consequences**
A single dropdown choice made the entire VM environment unreliable. In a real IT or cybersecurity environment, this kind of misconfiguration could delay work or be mistaken for a more serious hardware/software fault.


4 - **Restart after display setting changes**
Display controller changes don't always take effect until the VM is fully restarted — not just paused or saved.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Issue Log

|               Issue                       |               **Root Cause**                    |                  **Why**                         |           **Status**            |
|-------------------------------------------|-------------------------------------------------|--------------------------------------------------|----------------------------------
|Invalid settings warning +no mouse cursor  |   Wrong graphics controller (VBoxVGA) selected  |   Changed to VMSVGA in Display → Screen settings |             Resolved            |
|                                           |                                                 |                                                  |                                 |

