<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<b>Create a Resource Group in Azure</b>

1. In Azure, create a Resource Group by clicking on <b>Resource Groups</b> and then <b>+ Create</b>.
2. Make a note of the <b>Region</b> (you'll need it later). Name the resource group <em>Network-Activities</em>. Click on the blue `Review + Create` button at the bottom.

<p>
<img src="https://github.com/user-attachments/assets/4ed7b0e5-a2c6-43d0-aa48-ffcbcbe42bf0" height="80%" width="80%" alt="Create Resource Group"/>
</p></br>


<b>Create a Windows 10 Virtual Machine (VM)</b>

1. In Azure, navigate to "virtual machines". Click on the <b>+ Create</b> tab and select <b>Azure virtual machine</b>.
2. Make sure the resource group is <em>Network-Activities</em>. Name the VM <b>Windows-vm</b> and make sure the selected Region is the same as the Resource Group's.
3. For <b>Image</b> select <b>Windows 10 Pro, version 22H2</b>. For size, select a size that has at least 2 vcpus.
4. Create a username and password. Click `Next` until you get to the <b>Networking</b> section.
5. In the <b>Networking</b> section, make sure the <b>Virtual network</b> is <em>Active-Directory-VNet</em>.
6. Click on the blue `Review + Create` button and then `Create`.

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p></br>















