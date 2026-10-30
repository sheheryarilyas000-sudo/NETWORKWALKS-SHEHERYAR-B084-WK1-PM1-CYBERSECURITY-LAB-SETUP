# Cybersecurity Lab Environment Setup

## 📖 Project Overview
This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux. 

## 🎯 Objectives
- Install and configure VirtualBox.
- Create a custom NAT Network (10.0.0.0/24) for an isolated environment.
- Install Kali Linux as the primary attacking machine.
- Configure a static IP (10.0.0.2) and ensure internet connectivity.

## 💻 Machine Details
- **Hypervisor:** VirtualBox
- **OS:** Kali Linux (Debian 64-bit)
- **IP Address:** 10.0.0.2
- **Subnet Mask:** 255.255.255.0
- **Gateway:** 10.0.0.1
- **DNS:** 8.8.8.8

## 🛠️ Step-by-Step Setup
1. Created a NAT Network in VirtualBox with the CIDR `10.0.0.0/24`.
2. Imported the Kali Linux ISO and configured the VM with 2GB RAM and 25GB Storage.
3. Attached the VM to the custom NAT Network.
4. Configured the network adapter manually to set the IP address to `10.0.0.2`.
5. Verified the setup by checking the IP using `ifconfig` and pinging `8.8.8.8` for internet access.

<img width="959" height="539" alt="Week1_Sheheryar_LabSetup" src="https://github.com/user-attachments/assets/80d2a557-ef4f-4203-aeb9-edd2d26de0e4" />


## 🔧 Troubleshooting Experience
- **Issue:** Network disconnected automatically after setting the static IP.
- **Solution:** It was a DAD (Duplicate Address Detection) timeout issue in Kali Linux. I solved it by running `sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0` and restarting the network connection.
