<img src="https://i.imgur.com/NLKeLBZ.jpeg" height="80%" width="80%">

<H2> Azure Network Protocols </H2>
<p>This lab demonstrates how to create and configure virtual machines (VMs) in Azure, observe network traffic, and manage security settings. It covers setting up a Windows 10 and Ubuntu VM, using Wireshark to capture and analyze ICMP, SSH, DHCP, DNS, and RDP traffic, and configuring a Network Security Group (NSG) to control inbound traffic. The lab also includes tasks like pinging, SSHing, and observing real-time traffic in Wireshark, while learning about network protocols and security configurations./p>

<h2> Requirements </h2>
<p> 
  
 -   Azure Account (free tier works)

 -  Microsoft Remote Desktop (for macOS users)

 -  Wireshark is installed on a Windows 10 VM

 -  Windows 10 VM and Linux VM in Azure

 -  Resource Group and Virtual Network in Azure

 -  Network Security Group (NSG) for traffic management

 -  Basic knowledge of network protocols (ICMP, SSH, DHCP, DNS, RDP)</p>

<h2> Step 1: Create VMs on Azure </h2>
<p> To start, log in to the Azure Portal at https://portal.azure.com/. Next, create a Resource Group by navigating to Resource Groups > Create, then name the resource group and choose the region. Afterward, click Review + Create, then click Create.
<img src="https://i.imgur.com/yCaYnOb.jpeg" height="80%" width="80%">

  
For the Windows 10 VM, go to Virtual Machines > Create > Virtual Machine. Select the previously created Resource Group and choose Windows 10 as the image. For authentication, select Username/Password and allow Azure to create a new Virtual Network (VNet) and Subnet. Click Review + Create, then Create.
<img src="https://i.imgur.com/EaLwgux.jpeg" height="80%" width="80%"> 
<img src="https://i.imgur.com/q3Z4REM.jpeg" heigth="80%" width="80%">


To create the Linux (Ubuntu) VM, navigate to Virtual Machines > Create > Virtual Machine. Select the same Resource Group and Virtual Network as the Windows 10 VM, ensuring both VMs are in the same VNet/Subnet. For authentication, use Username/Password, then click Review + Create, and Create.

<img src="https://i.imgur.com/c4l1xmJ.jpeg" height="80%" widht="80%" >


End Part 1 by keeping both VMs for Part 2.
</p>
<h2> Part 2: Observe ICMP Traffic</h2>
<P>Part 2: Observe ICMP Traffic
Connect to Windows 10 VM

1. Connect to Windows 10VM
   - Use Microsoft Desktop (if on Mac) to connect to oyur Windows 10 Vm

2. Install Wireshark

  - Inside the Windows 10 VM, download and install Wireshark.
    <img src="https://i.imgur.com/0jggAax.jpeg" height="80%" width="80%">
    
3. Start Packet Capture

  - Launch Wireshark and click Start Capture on the main interface.
    <img src="https://i.imgur.com/4SfG2pd.jpeg" height="80%" width="80%">
    
  -  Set the display filter to "icmp" to isolate ping traffic.
    <img src="https://i.imgur.com/vUfZVze.jpeg" height="80%" width="80%" > 

4. Ping Ubuntu VM (Private IP)
 - In the Azure Portal, get the private IP address of your Ubuntu VM.
   <img src="https://i.imgur.com/vCwB6B8.jpeg" height= "80%" width="80%" >   
 - Watch for ICMP request and reply traffic in Wireshark
</P>
<h2> Part3:Configure Firewall Rules (NSG) & Observe SSH Traffic</h2>
<p>Section 1: Configuring a Firewall (Network Security Group)
1. On your Windows 10 VM, start a continuous ping to the private IP address of your Ubuntu VM using Command Prompt or PowerShell.
<img src="https://i.imgur.com/GdlqkoO.jpeg" height="80%" width="80%"> 
  
2. Go to the Network Security Group (NSG) associated with your Ubuntu VM in the Azure Portal.
<img src= "https://i.imgur.com/x78mcOA.jpeg" height="80%" width="80%"> 
3. Edit the Inbound Rules to block ICMP traffic by disabling the rule that allows it.
<img src= "https://i.imgur.com/tZC7tiL.jpeg" height="80%" width="80%" > 
4. Return to the Windows 10 VM and observe:

  - In Wireshark, ICMP reply packets should stop appearing.
<img src="https://i.imgur.com/EuMLny0.jpeg" height="80%" width="80%" > 
  - In Command Prompt, the ping should start failing or timing out.
<img src= "https://i.imgur.com/wCZ5IKs.jpeg" height="80%" width="80%">
5. Return to the NSG settings and re-enable ICMP traffic by restoring the inbound rule.
 <img src="https://i.imgur.com/w60Kmmq.jpeg" height="80%" width="80%">
6. Back in the Windows 10 VM, confirm that the ping is working again and ICMP packets are visible in Wireshark.
 <img src= "https://i.imgur.com/TNrXQAp.jpeg" height="80%" width="80%">
7. Stop the ping activity once confirmed.

</p>

<h2> Observe SSH Traffic</h2>
<p> 
1. Reconnect to your Windows 10 VM using Remote Desktop.

2. Open Wireshark and start a new packet capture session.

3. Apply a filter to display only SSH traffic.
<img src="https://i.imgur.com/773Sybj.jpeg" height="80%" width="80%">
4. From the Windows 10 VM, initiate an SSH connection to the Ubuntu VM using its private IP address.
<img src="https://i.imgur.com/oHwN14E.jpeg" height="80%" width="80%">  
5. Log in by entering the Ubuntu VM’s username and password when prompted.
<img src="https://i.imgur.com/94qJl9U.jpeg" height="80%" width="80%" >
6. Type a few commands within the SSH session to generate traffic.
<img src="https://i.imgur.com/kBrnnP3.jpeg" height="80%" width="80%" >
7. In Wireshark, observe the flow of encrypted SSH packets between the two VMs.
<img src="https://i.imgur.com/wAgtqIk.jpeg" height="80%" width="80%" >
8. Exit the SSH session once complete.

</p>

<h2>  Observe DHCP Traffic </h2>
<p>
1. In Wireshark, apply a filter to display only DHCP traffic.
<img src="https://i.imgur.com/TSdsllH.jpeg" height="80%" width="80%">
2. On the Windows 10 VM, attempt to renew the IP address by issuing a command that triggers DHCP.
<img src="https://i.imgur.com/TSdsllH.jpeg" height="80%" width="80%">
3. Monitor Wireshark as it displays DHCP request and response packets, showing the lease renewal process in action.</p>
<img src="https://i.imgur.com/GCeQQAD.jpeg" height="80%" width="80%> 

<h2>Observe DNS Traffic</h2>
<p>
1. In Wireshark, apply a filter to show only DNS traffic.
<img src="https://i.imgur.com/nZuUpS5.jpeg" height="80%" width="80%">
  2. On the Windows 10 VM, use a command to look up domain names like google.com and disney.com.
<img src="https://i.imgur.com/KapVTIi.jpeg" height="80%" width="80%">
  3. Watch Wireshark display DNS query and response packets as the domain names are resolved into IP addresses.</p>
<img src= "https://i.imgur.com/UpFzG5n.jpeg" height="80%" width80%">

<h2>   Observe RDP Traffic </h2>
<p>
1. In Wireshark, set a filter to display RDP traffic only.

2. Notice the continuous stream of packets even when you're not actively clicking or typing.
<img src="https://i.imgur.com/tpmM23O.jpeg" height="80%" width="80%"> 
3. This constant activity happens because the Remote Desktop Protocol (RDP) maintains a live session view between your local machine and the VM, which requires ongoing traffic transmission</p>

<h2> Congratulations!</h2>
<P> You've successfully completed the Azure Networking & Protocol Analysis Lab! 

In this hands-on project, you:

 - Deployed and configured virtual machines in Azure

 - Explored how ICMP, SSH, DHCP, DNS, and RDP traffic flows through a network

 - Captured and analyzed live network packets using Wireshark

 - Modified Network Security Group (NSG) rules to control traffic flow

These skills are foundational for roles in IT support, cloud operations, and cybersecurity. </P>
