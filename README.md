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

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

1. VM Setup

2. ICMP Traffic

3. Firewall & Protocols (SSH, DHCP, DNS, RDP)


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1 – Create Virtual Machines (Part 1)

Go to Azure Portal
.

Create a Resource Group.

Create a Windows 10 VM:

Select the previously created Resource Group.

Allow it to create a new Virtual Network (VNet) and Subnet.

Create a Linux (Ubuntu) VM:

Use the same Resource Group and Virtual Network (must be the same VNet).

Authentication type: Username/Password.

Confirm both VMs are in the same VNet/Subnet.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2 – Observe ICMP Traffic (Part 2)

If using Mac, install Microsoft Remote Desktop.

Use RDP to connect to the Windows 10 VM.

Inside Windows 10 VM:

Install Wireshark.

Start a packet capture.

Filter for ICMP traffic only.

Get the private IP address of the Ubuntu VM.

From Windows 10 VM:

Ping the Ubuntu VM → Observe requests & replies in Wireshark.

Ping a public website (e.g., www.google.com) → Observe ICMP traffic in Wireshark.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3 – Configure Firewall & Observe Other Protocols (Part 3)
🔹 ICMP (Firewall Behavior)

Start a continuous ping from Windows 10 VM → Ubuntu VM.

In Azure → open Ubuntu VM’s Network Security Group (NSG).

Disable inbound ICMP.

Observe failed pings in Wireshark/command line.

Re-enable ICMP → Observe ping success resuming.

Stop ping activity.

🔹 SSH Traffic

In Wireshark → start new capture & filter for SSH.

From Windows 10 VM → SSH into Ubuntu VM:

ssh labuser@<private IP>

Enter credentials, type commands, observe SSH packets in Wireshark.

Exit SSH with exit.

🔹 DHCP Traffic

In Wireshark → filter for DHCP.

From Windows 10 VM (PowerShell as Admin):

Run ipconfig /renew.

Observe DHCP traffic in Wireshark.

🔹 DNS Traffic

In Wireshark → filter for DNS.

From Windows 10 VM (cmd/PowerShell):

Run nslookup google.com and nslookup disney.com.

Observe DNS traffic in Wireshark.

🔹 RDP Traffic

In Wireshark → filter for RDP (tcp.port == 3389).

Observe nonstop RDP traffic.

Reason: RDP streams the full session continuously, not just user activity.
</p>
<br />
