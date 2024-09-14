<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<!--
<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)
-->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 24.04

<h2>High-Level Steps</h2>

1. Create a Windows 10 Pro and Ubuntu Server virtual machine under the same virtual network
2. Remote connect into the Windows virtual machine
3. Install Wireshark
4. Execute various Windows networking commands and inspect packets in Wireshark

<h2>Actions and Observations</h2>


With Azure, we can deploy a virtual machine to the cloud and connect to it via Remote Desktop Protocol. Let's deploy a Windows 10 Pro VM under a resource group, which we'll call `azure-networking`. For our case, 2 CPUs and 16 GB of RAM will be enough.


<p float="left">
  <img src="images/Step1_WindowsVMCreation.png" height="80%" width="80%"/>
  <!-- <img src="images/Step1_WindowsVMCreation2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> -->
</p>

The Ubuntu Server VM is not as resource heavy, so we can opt to use one of the cheaper hardware size. To ensure connectivity between the two VMs, we can put this VM under the same virtual network.

<p>
  <img src="images/Step1_UbuntuServerVMCreation.png" height="80%" width="80%"/>
  <img src="images/Step1_UbuntuServerVMCreation_NetworkSettings.png" height="80%" width="80%"/>
</p>

Now that the VMs are created, we can use **Remote Desktop Connection** to connect to our Windows 10 Pro VM. Once the Windows setup is complete, download [Wireshark](https://www.wireshark.org/download.html). We will download the `Windows x64 Installer` and stick with the default settings. Note that the Wireshark installer will also install `Npcap`. Now, open Wireshark and you will be greeted with the following screen:

<img src="images/WiresharkMainScreen.png" height="80%" width="80%"/>

With Wireshark we can inspect all incoming and outgoing packets from our computer. We will inspect the following traffic:
- ICMP
- SSH
- DHCP
- DNS
- RDP

Notice that we can filter our packets. As I am using an Ethernet connection, I will select that caputuring traffic. Let's first filter by ICMP traffic by typing `icmp` into the filter text field at the top and hit apply.

<img src="images/WiresharkICMPFilter.png" height="80%" width="80%"/>

Then we can start the packet trace by clicking the button on the top left.

<img src="images/WiresharkICMPFilter2.png" height="80%" width="80%"/>

We should then be greeted with the following screen:

<img src="images/WiresharkICMPBlank.png" height="80%" width="80%"/>
