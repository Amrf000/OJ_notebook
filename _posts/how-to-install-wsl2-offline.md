---
layout: default
---

[How to install wsl2 offline](https://ripon-banik.medium.com/how-to-install-wsl2-offline-b470ab6eaf0e)
===========================

[![Ripon Banik](https://miro.medium.com/fit/c/56/56/0*eVdo4350dV6X3gOz.)](/?source=post_page-----b470ab6eaf0e--------------------------------)

[

Ripon Banik

](/?source=post_page-----b470ab6eaf0e--------------------------------)

[

Apr 10·2 min read

](/how-to-install-wsl2-offline-b470ab6eaf0e?source=post_page-----b470ab6eaf0e--------------------------------)

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Fb470ab6eaf0e&operation=register&redirect=https%3A%2F%2Fripon-banik.medium.com%2Fhow-to-install-wsl2-offline-b470ab6eaf0e&source=post_actions_header--------------------------bookmark_preview-----------)

Manually install wsl2 when locked in Microsoft Store

Introduction
============

Microsoft offers running Linux in Windows using technology was WSL (Windows Subsystem for Linux). The new version of wsl which is called wsl2 allow to run a Microsoft customized Linux Kernel with distro of your choice. In this article, I will use Ubuntu distro.

To update to WSL 2, you must be running Windows 10.

*   For x64 systems: Version 1903 or higher, with Build 18362 or higher.
*   For ARM64 systems: Version 2004 or higher, with Build 19041 or higher.
*   Builds lower than 18362 do not support WSL 2.

To check your version and build number, select Windows logo key + R, type winver, select OK. (Or enter the `ver` command in Windows Command Prompt)

Pre-requisites
==============

The follow are required to be installed before you can run the installation of distro. It will install wsl.exe as well.

**a.** **Enable the Windows Subsystem for Linux**

Open PowerShell as Administrator and run:

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

**b. Enable Virtual Machine feature**

Open PowerShell as Administrator and run:

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

**c. Download and install the Linux kernel update package**

Open Command Prompt or PowerShell and enter: `systeminfo | find "System Type"`.

Download package for the system type as above

x64 — [https://wslstorestorage.blob.core.windows.net/wslblob/wsl\_update\_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

arm64 — [https://wslstorestorage.blob.core.windows.net/wslblob/wsl\_update\_arm64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)

Run the update package downloaded in the previous step. (Double-click to run — you will be prompted for elevated permissions, select ‘yes’ to approve this installation.)

**Download and install distro**
===============================

Here I am going to download Ubuntu 20.04 distro for x64 and install it via Powershell

1.  Download the distro

Invoke-WebRequest -Uri [https://aka.ms/wslubuntu2004](https://aka.ms/wslubuntu2004) -OutFile Ubuntu.appx -UseBasicParsing

2\. Install the distro

Add-AppxPackage .\\app\_name.appx

Configure the distro
====================

If the above installation is complete, left click on Windows Icon and select Ubuntu 20.04 LTS and continue with the configuration. Provide the username and password when prompted.

The installation is now complete. By default it set the version as 1, to change it to Version 2, type the command

wsl --set-version Ubuntu-20.04 2

When the conversion is complete, you can verify it by using command —

wsl -l -v

To set wsl2 as your default version, you can run the following command -

wsl --set-default-version 2

Icing on the cake
=================

To manage multiple version of wsl distro, Microsoft has made it way by introducing Windows Terminal. Again to run it offline, download the bundle from the link below and install it. In my case, I downloaded version [v1.5.10411.0](http://Microsoft.WindowsTerminal_1.5.10411.0_8wekyb3d8bbwe.msixbundle)

[

Releases · microsoft/terminal
-----------------------------

### This is a quick servicing release to address a few issues in the 1.5 stable release. A preinstallation kit is available…

github.com



](https://github.com/microsoft/terminal/releases)