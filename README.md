NETWORKWALKS-WK1-CYBERSECURITY-LAB-SETUP

An Isolated Virtual Cybersecurity Lab Using VirtualBox and Kali Linux

👤 Author Details

- Author: Relebogile Majatladi
- Task Batch: B084
- Date Completed: October 2026
- LinkedIn: https://www.linkedin.com/in/relebogile-modise-60a2ab43b

---

📌 Project Overview

This project documents the setup and configuration of a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux.

The purpose of this lab is to establish a controlled environment for practising cybersecurity fundamentals, network reconnaissance, network scanning, vulnerability assessment, and penetration-testing techniques.

The lab uses a VirtualBox NAT Network to support communication between virtual machines while providing outbound internet connectivity. This configuration creates a foundation for future cybersecurity exercises involving attacker and target virtual machines.

«⚠️ Disclaimer: This laboratory is intended strictly for educational purposes and authorised security testing. Only test systems that you own or have explicit permission to assess.»

🎯 Project Objectives

- Install and configure VirtualBox.
- Install 7-Zip to extract virtual machine archives.
- Create and configure a dedicated NAT Network.
- Import and configure a Kali Linux virtual machine.
- Configure and verify IPv4 networking.
- Test network connectivity and DNS resolution.
- Verify that Nmap is installed and functional.
- Create a clean virtual machine snapshot for recovery.
- Troubleshoot hardware virtualisation issues.

🛠️ Lab Configuration

Component| Configuration
Host Operating System| Windows 11
Host RAM| 8 GB
Processor| Intel Core i5
Hypervisor| Oracle VirtualBox 7.2
Security Operating System| Kali Linux 2026.3
Kali Linux RAM| 2048 MB (2 GB)
Virtual Network| NAT Network
Network Name| "NatNetwork"
IPv4 Network| "10.0.0.0/24"
Kali Linux IP Address| "10.0.0.2/24"
Default Gateway| "10.0.0.1"
DNS Server| "8.8.8.8"
DHCP| Enabled
IPv6| Disabled
Network Adapter| Intel PRO/1000 MT Desktop

Note: The Kali Linux IP address is intended to be a consistent lab address. Ensure it is reserved or excluded from the DHCP pool to avoid IP address conflicts.

🏗️ Lab Architecture

The laboratory consists of a Windows 11 host running VirtualBox, with Kali Linux connected to a dedicated NAT Network.

                Internet
                    |
             VirtualBox NAT
                    |
          NatNetwork: 10.0.0.0/24
                    |
             +--------------+
             | Kali Linux   |
             | 10.0.0.2/24  |
             +--------------+
                    |
          Future Target VMs
          (Isolated Lab Tests)

This architecture provides a starting point for a multi-machine cybersecurity environment.

Why NAT Network?

Unlike standard NAT, which typically isolates individual VMs from one another, a NAT Network allows connected virtual machines to communicate with one another while sharing outbound network connectivity through network address translation.

⚙️ Lab Setup Procedure

Step 1: Install 7-Zip

Installed 7-Zip to extract the Kali Linux virtual machine package if distributed as a ".7z" archive.

Tool: "7-Zip Official Website" (https://www.7-zip.org/)

Step 2: Install VirtualBox

Installed Oracle VirtualBox to create, manage, and configure virtual machines and virtual network interfaces.

Tool: "VirtualBox Official Website" (https://www.virtualbox.org/)

Step 3: Create a NAT Network

Created a dedicated NAT Network in VirtualBox with the following configuration:

Setting| Value
Network Name| "NatNetwork"
IPv4 Prefix| "10.0.0.0/24"
DHCP| Enabled
IPv6| Disabled

This network allows multiple VMs attached to the same NAT Network to communicate with one another while supporting outbound internet connectivity.

Step 4: Import Kali Linux

Downloaded the Kali Linux VirtualBox image from the official Kali Linux website and imported it into VirtualBox.

Virtual Machine Package: "kali-linux-2026.3-virtualbox-amd64"

Download: "Official Kali Linux Website" (https://www.kali.org/get-kali/)

Configured the virtual machine with the following settings:

- Network Adapter: Adapter 1
- Attached To: NAT Network
- Network Name: "NatNetwork"
- Adapter Type: Intel PRO/1000 MT Desktop
- Allocated RAM: 2048 MB

A shared folder was also configured to facilitate file transfers between the Windows host and the Kali Linux virtual machine.

Step 5: Configure Kali Linux Networking

Configured and checked the Kali Linux IPv4 network settings.

Intended network configuration:

IP Address:    10.0.0.2
Subnet Mask:   255.255.255.0
Default Route: 10.0.0.1
DNS Server:    8.8.8.8

A consistent IP address makes it easier to document the environment and reference the Kali Linux machine during future exercises.

Important: Confirm the actual gateway address assigned by VirtualBox. Also ensure that the selected IP address does not conflict with the NAT Network's DHCP allocation.

Step 6: Create a Clean VM Snapshot

Created a clean baseline snapshot after completing the initial setup and network checks.

The snapshot provides a recovery point that can be restored if later experiments modify the operating system or network configuration.

Benefit: Snapshots make it easier to return to a known working state between cybersecurity exercises.

🔍 Lab Verification

The following commands were used or identified to verify the lab configuration.

Test| Command| Expected Result
Check IP configuration| "ip a"| Kali Linux displays the expected IPv4 address
Test gateway connectivity| "ping -c 4 10.0.0.1"| Replies from the configured gateway
Test outbound connectivity| "ping -c 4 8.8.8.8"| Replies if ICMP traffic is permitted
Test DNS resolution| "nslookup networkwalks.com"| Domain resolves to an IP address
Verify Nmap installation| "nmap --version"| Installed Nmap version is displayed
Verify snapshot recovery| Restore snapshot, then run "ip a"| Baseline network configuration is restored

Connectivity result: Outbound routing and connectivity were reported as successfully verified using "ping 8.8.8.8".

Note: Expected results describe the verification criteria. DNS, ICMP, and network results may vary depending on the configuration and availability of external services.

Example Network Configuration Commands

The following commands illustrate how to configure a temporary IPv4 address and default route on a Linux network interface.

First, identify the correct interface:

ip -br address
ip route

Then, if the interface is "eth0" and the intended network settings have been confirmed:

sudo ip addr flush dev eth0
sudo ip addr add 10.0.0.2/24 dev eth0
sudo ip route replace default via 10.0.0.1

Important: Replace "eth0" with the actual interface name on your system. These commands can remove existing interface addresses and alter connectivity. Use them only when appropriate for your lab configuration.

For persistent network configuration, use the relevant NetworkManager connection settings instead of relying on temporary commands.

🐛 Troubleshooting

Problem 1: Network Connectivity and Routing

Issue: The Kali Linux VM required network configuration and connectivity verification.

Resolution steps:

1. Checked the assigned IP address using "ip a".
2. Inspected the routing table using "ip route".
3. Confirmed the intended gateway and subnet.
4. Tested gateway connectivity.
5. Tested outbound connectivity to "8.8.8.8".
6. Verified DNS resolution using "nslookup".

Lesson learned: Correct IP addressing, routing, DNS configuration, and virtual network attachment are essential for reliable connectivity.

Problem 2: VirtualBox VT-x / Hardware Virtualisation Error

Issue: The virtual machine initially failed to start because hardware virtualisation was disabled in the host system's firmware settings.

Resolution steps:

1. Restarted the computer.
2. Entered the BIOS/UEFI settings.
3. Enabled Intel VT-x or the corresponding hardware virtualisation setting.
4. Saved the configuration and restarted the host operating system.
5. Attempted to start the virtual machine again.

Lesson learned: Hardware virtualisation must be enabled and available to the hypervisor for the intended virtual machine configuration.

📚 What I Learned

Through this project, I gained practical experience in virtualisation, Linux networking, and cybersecurity lab preparation.

1. NAT vs. NAT Network

I learned the difference between standard NAT and NAT Network configurations in VirtualBox.

A NAT Network allows multiple attached VMs to communicate with one another while providing outbound network address translation. This makes it useful for building a multi-machine cybersecurity lab.

2. Virtual Machine Networking

I learned how virtual network adapters connect guest operating systems to virtual networks and how IP addresses, subnet masks, gateways, and DNS settings affect connectivity.

3. Kali Linux Fundamentals

I gained experience with basic Linux networking commands and learned how to inspect network interfaces, routing information, and connectivity.

4. Cybersecurity Lab Preparation

I learned how to prepare a controlled environment for future reconnaissance, network scanning, vulnerability assessment, and authorised penetration-testing exercises.

5. Virtual Machine Snapshots

I learned the importance of maintaining a clean baseline snapshot so that the lab can be restored after testing or configuration changes.

6. Troubleshooting Virtualisation

I gained practical experience identifying and resolving a hardware virtualisation issue involving Intel VT-x in the BIOS/UEFI settings.

🔮 Future Improvements

Planned improvements for the laboratory include:

- Adding a deliberately vulnerable target VM for authorised testing.
- Configuring multiple virtual machines on the same NAT Network.
- Practising Nmap host discovery and port scanning against lab-owned targets.
- Performing vulnerability assessments in the controlled environment.
- Documenting results with terminal outputs and screenshots.
- Exploring packet analysis with Wireshark.
- Improving network segmentation and lab isolation where appropriate.

🔐 Ethical and Safety Considerations

This environment is intended for learning and authorised security testing.

- Only scan systems you own or have explicit permission to test.
- Keep vulnerable target machines within the intended lab network.
- Avoid exposing vulnerable services directly to public networks.
- Take snapshots before making significant configuration changes.
- Follow applicable cybersecurity laws and responsible disclosure practices.

📖 References

- "Kali Linux Official Website" (https://www.kali.org/)
- "VirtualBox Official Website" (https://www.virtualbox.org/)
- "7-Zip Official Website" (https://www.7-zip.org/)
- "Nmap Official Website" (https://nmap.org/)

---

✅ Project Status

Status: Initial lab setup documented.

The project establishes a foundation for future hands-on cybersecurity learning using Kali Linux and VirtualBox.

Repository: "NETWORKWALKS-WK1-CYBERSECURITY-LAB-SETUP"

Author: Relebogile Majatladi
Task Batch: B084
Date Completed: October 2026
LinkedIn link:https://www.linkedin.com/in/relebogile-modise-60a2ab43b
