<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro, version 22H2 - Gen2
- Linux (Ubuntu 20.04)

<h2>High-Level Steps</h2>

**Part 1 (Create our Resources)**
1. Create a Resource Group
2. Create a Windows 10 Virtual Machine (VM)
  - While creating the VM, select the previously created Resource Group
  - While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
3. Create a Linux (Ubuntu) VM
  - While create the VM, select the previously created Resource Group and Vnet
4. Observe Your Virtual Network within Network Watcher



**Part 2 (Observe ICMP Traffic)**
5. Use Remote Desktop to connect to your Windows 10 Virtual Machine
6. Within your Windows 10 Virtual Machine, Install Wireshark
7. Open Wireshark and filter for ICMP traffic only
8. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
  - Observe ping requests and replies within WireShark
9. From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
10. Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
  - Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
  - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
  - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
  - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
  - Stop the ping activity



**Part 3 (Observe SSH Traffic)**
11. Back in Wireshark, filter for SSH traffic only
12. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
  - Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
  - Exit the SSH connection by typing ‘exit’ and pressing [Enter]

**Part 4 (Observe DHCP Traffic)**
13. Back in Wireshark, filter for DHCP traffic only
14. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
  - Observe the DHCP traffic appearing in WireShark

**Part 5 (Observe DNS Traffic)**
15. Back in Wireshark, filter for DNS traffic only
16. From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
  - Observe the DNS traffic being show in WireShark

**Part 6 (Observe RDP Traffic)**
17. Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
18. Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
  - Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

