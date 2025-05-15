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
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- Create a Resource Group and Virtual Machines
- Install Wireshark
- ICMP Traffic
- SSH Traffic
- DHCP Traffic
- DNS Traffic
- RDP Traffic

<h2>Actions and Observations</h2>

<b>Create a Resource Group in Azure</b>

1. In Azure, create a Resource Group by clicking on <b>Resource Groups</b> and then <b>+ Create</b>.
2. Make a note of the <b>Region</b> (you'll need it later). Name the resource group <em>Network-Activities</em>. Click on the blue `Review + Create` button at the bottom.

<p>
<img src="https://github.com/user-attachments/assets/4ed7b0e5-a2c6-43d0-aa48-ffcbcbe42bf0" height="80%" width="80%" alt="Create Resource Group"/>
</p></br>


<b>Create a Windows 10 and a Linux virtual machine (vm)</b>

1. In Azure, navigate to "virtual machines". Click on the <b>+ Create</b> tab and select <b>Azure virtual machine</b>.
2. Name the resource group is <em>Network-Activities</em>. Name the VM <b>Windows-vm</b> and make sure the selected Region is the same as the Resource Group's.
3. For <b>Image</b> select <b>Windows 10 Pro, version 22H2</b>. For size, select a size that has at least 2 vcpus.
4. Create a username and password. Click `Next` until you get to the <b>Networking</b> section.
5. In the <b>Networking</b> section, allow it to create a new Virtual Network (Vnet) and Subnet
6. Click on the blue `Review + Create` button and then `Create`.
7. Once you've created your Windows VM, now we'll create a Linux VM. To start, repeat step 1.
8. Select the same resource group as the Window's VM and name the new VM <b>Linux-VM</b>.
9. For image, select <b>Ubuntu Server 22.04</b> and select a size that has at least 2 vcpus.
10. Use the same username and password as the Windows VM and in the <b>Networking</b> section, select the same network as the Windows VM.
11. Click on the blue `Review + Create` button and then `Create`.

<p>
<img src="https://github.com/user-attachments/assets/ba98d46e-ed87-419e-8505-d526ae5377ee" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Use Remote Desktop to connect to your Windows 10 Virtual Machine</b>

1. Type <em>mstsc</em> in your Windows search bar and select <b>Remote Desktop Connection</b>
2. Copy and paste the Windows VM Public IP address and click `Connect`
3. Type in your username and password and click `OK`

<p>
<img src="https://github.com/user-attachments/assets/e79dc1b8-6286-41dd-bfec-377ed61968af" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Install Wireshark</b>

Wireshark is a network protocol analyzer used to capture, inspect, and analyze data packets traveling over a network in real time. It lets users see detailed information about each packet, such as source and destination IP addresses, protocol types (e.g., TCP, UDP, HTTP), and the actual data payload.

1. Open a browser and type www.wireshark.org in the address bar. Press Enter.
2. Click on the <b>Download</b> button and select <b>Windows x64 Installer</b>
3. Once downloaded, open the file. You can close the browser.
4. Click `Next` throughout the installation process. When you get to the section where it says <b>Install Npcap 1.79</b> make sure that the checkbox is checked.
5. Click `Install`. It will download a few files and then you'll have to agree to some terms and click `Install` again.

<p>
<img src="https://github.com/user-attachments/assets/631147d9-c26a-44a7-8b8c-d536ef317e3f" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<p>
<img src="https://github.com/user-attachments/assets/79daeb55-34c7-4114-bd4d-9de17b1df388" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Open Wireshark and Start Packet Capture</b>

A packet capture in Wireshark helps you look closely at all the little pieces of data traveling on a network. This helps if you're investigating security threats or searching for the root cause of network or performance issues.

1. Type <em>Wireshark</em> in the virtual machine's search box and select <b>Run as administrator</b>
2. Click on <b>Ethernet</b> and then click on the blue shark fin icon under the <b>File</b> menu. This will begin packet capture.

<p>
<img src="https://github.com/user-attachments/assets/9bc7a788-0a25-4b7a-9ed3-1b50bdaef1e9" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Within Wireshark, filter for ICMP traffic only</b>

 Internet Control Message Protocol (ICMP) is a network layer protocol used by network devices to communicate. It is used to report network conditions, errors, and perform diagnostics.

1. In the Wireshark search bar, type <em>icmp</em> and press <b>Enter</b>. Since there are no other network devices connected there should be no ICMP traffic.

<p>
<img src="https://github.com/user-attachments/assets/fa349981-860d-420c-956e-0ba508daf220" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Retrieve the private IP address of the Ubuntu VM (Linux-VM) and attempt to ping it from within the Windows 10 VM</b>

1. Go to the Azure portal on your actual computer, click on the Linux virtual machine's name and copy the Private IP address. In this case it's <em>10.0.0.5</em>
2. Open PowerShell on your Windows VM and type, for this example, <em>ping 10.0.0.5</em>. Note that the Linux VM has to be running, but you don't have to have remoted into it.
3. Observe the ping data in Powershell as well as the isolated ICMP traffic in Wireshark

<p>
<img src="https://github.com/user-attachments/assets/990abae6-b856-4a18-ad83-93814eca7c1d" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<p>
<img src="https://github.com/user-attachments/assets/679a78eb-1ade-4788-a148-710d7d73361b" height="80%" width="80%" alt="Create VM's"/>
</p>

Note that due to all the traffic, you need to isolate the ICMP traffic in order to see it 

While still isolating ICMP traffic, ping <b>Google</b> by typing <em>www.google.com</em> in Powershell. You'll see the traffic in Wireshark. This is because ICMP operates at the <b>Network Layer</b> of the <b>OSI (Open Systems Interconnection) model</b>, alongside <b>IP (Internet Protocol)</b>. 


<p>
<img src="https://github.com/user-attachments/assets/96d9641e-d17d-4113-a4c2-c2f382007226" height="80%" width="80%" alt="Create VM's"/>
</p>

<p>
<img src="https://github.com/user-attachments/assets/c2c70506-1dd4-4864-bccc-62f311befad5" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<b>Configuring a Firewall [Network Security Group]</b>

Now, we will configure a firewall for the Linux VM by going into its Network Security Group and adding an inbound security rule. This will stop ICMP traffic from the Windows VM.
First we will initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.

1. In the Windows VM, open <b>Powershell</b>, type <em>ping 10.0.0.5 -t</em> and press <b>Enter</b>. In this case <em>10.0.0.5</em> is the Linux VM's Private IP address and the `-t` flag makes the ping run continuously until you manually stop it (Ctrl+C).
2. In Wireshark, after isolating for ICMP traffic, you will see that there will be continuous traffic between the Windows VM (10.0.0.4) and the Linux VM (10.0.0.5)


<p>
<img src="https://github.com/user-attachments/assets/0fd5dc75-9eaa-4dd4-b85a-ddba7f84e602" height="80%" width="80%" alt="Create VM's"/>
</p>

<p>
<img src="https://github.com/user-attachments/assets/9009e5af-5d32-480e-a8cc-a6e2f261f4f7" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<b>Now, we will configure an inbound security rule in the Linux VM that will block requests from the Windows VM</b>

1. Go to the Azure portal and click on  <b>Virtual machines</b>. Click on the Linux VM name. On the left side-panel expand <b>Networking</b> and click on <b>Network settings</b>.
2. In the <b>Network settings</b> window, go to the <b>Network security gr...</b> line and click on the name link (it will end with <em>-nsg</em>). This will open a window with the Network security group name.
3. Once there, go to <b>Settings</b> on the left side-panel, click on <b>Inbound security rules</b>, and click on the <b>+ Add</b> symbol at the top.
4. Another window will open on the right side. In the <b>Destination port ranges</b> box type an asterisk. This stands for “any”.
5. In the <b>Protocol</b> section select <b>ICMPv4</b>
6. In the <b>Action</b> section select <b>Deny</b>
7. In the <b>Priority</b> box, type <em>290</em>. This will put the rule as the highest priority, therefore, the first to evaluate when the ping happens.
8. Click `Add` at the bottom

<p>
<img src="https://github.com/user-attachments/assets/cf41c88f-5a31-4301-b373-5bb4b8d41edb" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<b>Back in the Windows VM, observe the PowerShell ping activity and the ICMP traffic in WireShark</b>

Once the rule takes effect, all Powershell ping activity will say <b>Request timed out</b> and all ICMP traffic in Wireshark will appear as request, without a reply.

<p>
<img src="https://github.com/user-attachments/assets/49bc50c3-fd51-4a24-ac7b-63cc10602099" height="80%" width="80%" alt="Create VM's"/>
</p>

<p>
<img src="https://github.com/user-attachments/assets/6bc60cc4-c043-417a-a05d-5d9199a13b0f" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Re-enable ICMP traffic for the Linux VM</b>

For this, you can just delete the rule you created that disabled incoming ICMP traffic.
1. Go to the Inbound security rules section of your Linux VM (<b>Home</b> > <b>Virtual machines</b> > <b>Linux-VM</b> > <b>Networking</b> > <b>Network settings</b> > <b>Network security group</b> <em>link</em>)
2. Locate the security rule that was created and click on the trash can symbol at the end in order to delete the rule. Click `Yes` to confirm.

<p>
<img src="https://github.com/user-attachments/assets/0d635b0a-e6c1-4bc2-9c42-614f49c07ec3" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Back in the Windows VM, observe the Powershell ping activity and the ICMP traffic in Wireshark</b>

The Powershell ping activity will resume and the ICMP traffic in Wireshark will initiate the request and reply sequence.

<p>
<img src="https://github.com/user-attachments/assets/5bda7f17-5648-4d0c-8c13-c6bfcf5f835a" height="80%" width="80%" alt="Create VM's"/>
</p>

<p>
<img src="https://github.com/user-attachments/assets/f6fdf95d-a1dc-48fc-a8fb-7f38e6d28458" height="80%" width="80%" alt="Create VM's"/>
</p></br>


<b>Stop the ping activity</b>

To do this, press <b>Ctrl+C</b>. Control+C is a general-purpose way to interrupt or terminate a running process in most command-line environments.

<p>
<img src="https://github.com/user-attachments/assets/ec6a7870-5db4-4ca4-8033-3529aea9b15b" height="80%" width="80%" alt="Create VM's"/>
</p>

<p>
<img src="https://github.com/user-attachments/assets/207a8f38-0437-483a-a98c-ed2b4a0b2868" height="80%" width="80%" alt="Create VM's"/>
</p>

Click on the red square (stop) button in Wireshark. Click on the blue shark fin under <b>File</b> and select `Continue without Saving`. This will clear the packet capture, and with the icmp filter, will clear all traffic.

<p>
<img src="https://github.com/user-attachments/assets/8376ab51-8db9-4e7a-9326-57d8804e32c4" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<b>Filter for SSH (Secure Shell or Secure Socket Shell) traffic only</b>

SSH is a cryptographic network protocol used for secure communication over an unsecured network
1. Back in Wireshark, filter for SSH traffic only. You shouldn't see any traffic.

<p>
<img src="https://github.com/user-attachments/assets/a4798a4f-ceef-4516-992c-13ad7d6762d3" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<b>Secure Remote Access into the Linux VM</b>

Now we will remote into the Linux VM via PowerShell in the Windows VM

1. Open PowerShell as an Administrator and type: ssh your username@private IP address for linux vm. In this case it's <em>ssh azurevmuser25@10.0.0.5</em>. Press <b>Enter</b>. You will see traffic in Wireshark.
2. When asked <b>Are you sure you want to continue connecting (yes/no/[fingerprint])?</b> type <em>yes</em> and press <b>Enter</b>. You will see additional traffic in Wireshark.
3. Enter the Linux VM password. Note, however, that due to security reasons you won't be able to see the password as you're entering it. Your prompt will change and now you're inside the Linux VM.


<p>
<img src="https://github.com/user-attachments/assets/3521957b-d6d2-4e05-bb77-081b77928852" height="80%" width="80%" alt="Create VM's"/>
</p>

<p>
<img src="https://github.com/user-attachments/assets/9d7fd885-c049-43ac-a41d-2bf2a7701f03" height="80%" width="80%" alt="Create VM's"/>
</p></br>

<b>Type commands (id, hostname, uname -a, etc) into the Linux SSH connection and observe SSH traffic spam in WireShark</b>

Now we'll enter a few commands to get more information about the Linux VM

1. Type <em>id</em> and press <b>Enter</b>. This will display your username plus other information. The <b>id</b> command displays user identity information, including the user ID (UID), group ID (GID), and all groups the user belongs to, including secondary groups

<p>
<img src="https://github.com/user-attachments/assets/39bf4b7d-16f4-44fb-bc96-dbed19b153bc" height="80%" width="80%" alt="Create VM's"/>
</p>


2. Type <em>hostname</em> and press <b>Enter</b>. The <b>hostname</b> command in Linux displays or sets the system’s hostname, which is the name assigned to the computer on a network.

<p>
<img src="https://github.com/user-attachments/assets/f1e9a257-6fae-4d84-a0b3-2d0b3aec4f24" height="80%" width="80%" alt="Create VM's"/>
</p>


3. Type <em>uname -a</em> and press <b>Enter</b>. The <b>uname -a</b> command in Linux displays detailed system information about the kernel and operating system. Specifically, it shows Kernel name, Hostname (network name of the machine), Kernel version, Build number, distro info, and compile date, Machine hardware name (architecture), Processor type, Hardware platform, and Operating system.

<p>
<img src="https://github.com/user-attachments/assets/aa733daf-f874-4696-804d-b046fb06ca34" height="80%" width="80%" alt="Create VM's"/>
</p>


4. Type <em>pwd</em> and press <b>Enter</b>. The <b>pwd</b> command in Linux stands for <b>print working directory</b> and displays the current working directory — that is, the full path of the directory you're in.

<p>
<img src="https://github.com/user-attachments/assets/d7f29ac4-6fd7-4468-a5d5-7fce4e796c88" height="80%" width="80%" alt="Create VM's"/>
</p>


5. Let's create a text file in the Linux VM. Type <em>touch file.txt</em> and press <b>Enter</b>. The <b>touch</b> command is used to create an empty file or update the timestamp of an existing file. 

<p>
<img src="https://github.com/user-attachments/assets/1395ca31-d784-418a-9f8e-495111be5649" height="80%" width="80%" alt="Create VM's"/>
</p>


6. Let's display the names of files and folders in the current directory by typing <em>ls</em>. In this case it will display the <em>file.txt</em> file.

<p>
<img src="https://github.com/user-attachments/assets/946a7601-2e26-4eb0-b603-9c67a5b54231" height="80%" width="80%" alt="Create VM's"/>
</p>


7. Back in Wireshark you will see all the SSH traffic generated by just a few commands.

<p>
<img src="https://github.com/user-attachments/assets/246b6ef1-7963-4866-8193-c381eb6ec0cf" height="80%" width="80%" alt="Create VM's"/>
</p>


8. Exit the SSH connection by typing <em>exit</em> and pressing <b>Enter</b>. This will close the connection to the Linux VM and your prompt will change back to the Windows VM.

<p>
<img src="https://github.com/user-attachments/assets/928de481-c660-4ef4-b29e-8258ec5e5574" height="80%" width="80%" alt="Create VM's"/>
</p>








