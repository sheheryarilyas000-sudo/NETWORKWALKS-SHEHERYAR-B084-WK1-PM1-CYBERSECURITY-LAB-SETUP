# 🛡️ Cybersecurity & Pentesting Lab Environment Setup

## 📖 Project Overview
This project focuses on designing and deploying an isolated, secure virtual laboratory for cybersecurity testing and ethical hacking. The environment is built using VirtualBox and Kali Linux to provide a safe, controlled sandbox for vulnerability assessment, network scanning, and penetration testing without affecting the host machine or exposing real IP addresses.

## 🎯 Core Objectives & Requirements Met
- **Virtualization:** Installed and configured Oracle VirtualBox as the base hypervisor.
- **Attacking Machine:** Deployed Kali Linux (Debian 64-bit) as the primary pentesting OS.
- **Isolated Networking:** Created a custom `NATNetwork` to ensure the VM is completely isolated from the main host but still has internet access.
- **Host Integration:** Enabled Bidirectional Clipboard and Drag & Drop features, along with a permanent Shared Folder (`/downloads`) for seamless file transfer between the Windows 11 host and Kali VM.
- **Static Configuration:** Successfully assigned a static IP (`10.0.0.2`) as per the strict lab architecture guidelines.

## 💻 Network Architecture & Machine Specifications

| Component | Configuration / Specification |
| :--- | :--- |
| **Hypervisor** | Oracle VirtualBox |
| **Operating System** | Kali Linux (Debian 64-bit) |
| **RAM Allocated** | 2048 MB (2 GB) |
| **Storage Allocated** | 25 GB (Virtual Hard Disk) |
| **Network Mode** | NAT Network (`NatNetwork`) |
| **Promiscuous Mode** | Allow All |
| **Subnet (CIDR)** | 10.0.0.0/24 |
| **Kali Static IP** | 10.0.0.2 |
| **Gateway** | 10.0.0.1 |
| **DNS Server** | 8.8.8.8 |

## 🛠️ Detailed Step-by-Step Implementation

1. **Virtual Network Setup:** 
   - Opened VirtualBox Network Manager and created a custom `NATNetwork`.
   - Set the IPv4 Prefix strictly to `10.0.0.0/24` with DHCP enabled.
2. **Virtual Machine Creation:** 
   - Created a new VM and attached the Kali Linux `.iso` image.
   - Allocated 2GB of Base Memory and 25GB of Virtual Hard Disk space on the D: Drive to optimize storage.
3. **Advanced VM Configuration:** 
   - Attached the Network Adapter to the custom `NATNetwork` and set Promiscuous Mode to `Allow All`.
   - Enabled `Bidirectional` Shared Clipboard and Drag'n'Drop.
   - Mounted the host's `Downloads` directory as an Auto-mount Shared Folder.
4. **Operating System Installation:** 
   - Completed the Graphical Install of Kali Linux, opting for the entire disk guided partition and standard Xfce desktop environment.
5. **Network Interface Configuration:** 
   - Navigated to Network Settings in Kali Linux and switched IPv4 from Automatic (DHCP) to Manual.
   - Assigned the IP address `10.0.0.2`, netmask `24`, gateway `10.0.0.1`, and DNS `8.8.8.8`.
6. **Verification & Testing:** 
   - Verified the IP assignment using the `ifconfig` command in the terminal.
   - Executed a `ping 8.8.8.8` test to confirm outbound internet connectivity.

## 🖼️ Proof of Execution (Lab Results)
Below is the terminal output confirming the static IP configuration and active internet connectivity:

<img width="959" height="539" alt="Week1_Sheheryar_LabSetup" src="https://github.com/user-attachments/assets/80d2a557-ef4f-4203-aeb9-edd2d26de0e4" />

## 🔧 Troubleshooting & Problem Solving
- **Issue Encountered:** After manually applying the static IP (`10.0.0.2`), the network connection immediately dropped, and the `eth0` interface failed to show the assigned IPv4 address.
- **Root Cause:** This is a known Duplicate Address Detection (DAD) timeout bug in newer versions of NetworkManager and Kali Linux.
- **Resolution:** I resolved the issue by modifying the connection parameters via the terminal. I executed `sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0`, followed by bringing the connection down (`sudo nmcli connection down "Wired connection 1"`) and back up (`sudo nmcli connection up "Wired connection 1"`). This successfully forced the static IP to apply and restored internet access.
