# on-premises-active-directory-deployed-in-the-cloud-azure
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set up 2 virtual machines in azure
  - windows 2022 server
  - windows 10
- use remote desktop (RDP)
- changing inbound rules within the firewall of the domain controller to allow connectivity between the 2 vm's
- install active directory
- link client vm to our domain controller
- setup rdp for non admin users
- create 1000 users fast with a script and log into our vm with one of the newly created users

<h2>Deployment and Configuration Steps</h2>

- log into Azure, there are a couple of ways to do everything in Azure, the header or center of the page click create virtual machine.
click Azure virtual machine (VM)
<p>
<img src="https://imgur.com/0QMrH4G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
    
- name your VM anything you want in this case we named it dc-1

- resource group is automatically given a name but you can change it.
- change the region to your own, we used west US 3
- choose the size of the server taking into account what you will be using it for. we chose Standard e2 v3- 2vcpus, 16 gib memory
- create a username and password (just remember your credentials!)
- make sure to check your box (bottom left)
- we can go ahead and skip everything else and click review/create
- if you get the go ahead in the form of "validation passed" click create and were good to go, let it set up your machine.

</p>
<br />

<p>
<img src="https://imgur.com/tbajTdo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
    
-Repeat the same process for our 2nd vm but using windows 10 for the operating system.

-again name it whatever you want in this case we named it client-1

-set the resource group to the same one created for the first virtual machine.

-keep the size of the vcpus the same as the first machine

    -also use the same location in the first one we used west US 3
    
-Change authentication to "Password"

-here we are changing the dc controller network interface(nic) from dynamic to static (so it doesn't change)

<p>
<img src="https://imgur.com/nSpyl3O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
1
</p>
<br />

<p>
<img src="https://imgur.com/XyEeLg7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1a
</p>
<br />

<p>
<img src="https://imgur.com/JWI7oFz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2a
</p>
<br />

<p>
<img src="https://imgur.com/WfBAXlc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
6
</p>
<br />

<p>
<img src="https://imgur.com/QgBqoWR.png" height="80%" width="80%"alt="Disk Sanitization Steps"/>
</p>
<p>
8
</p>
<br />

<p>
<img src="https://imgur.com/eF3DpWa.png" height="80%" width="80%"alt="Disk Sanitization Steps"/>
</p>
<p>
8a
</p>
<br />


<p>
<img src="https://imgur.com/gC60m9n.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9
</p>
<br />

<p>
<img src="https://imgur.com/SyYziLJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9a
</p>
<br />

<p>
<img src="https://imgur.com/XOayICj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9b
</p>
<br />

<p>
<img src="https://imgur.com/339lmll.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
10
</p>
<br />

<p>
<img src="https://imgur.com/X8gLd5C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11
</p>
<br />

<p>
<img src="https://imgur.com/mTY2Hl5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11a
</p>
<br />

<p>
<img src="https://imgur.com/KMJwINr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11b
</p>
<br />

<p>
<img src="https://imgur.com/hMdcgNu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
12
</p>
<br />

<p>
<img src="https://imgur.com/jSTbWVp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
13-48
</p>
<br />

<p>
<img src="https://imgur.com/yKURgYH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
13-52
</p>
<br />

<p>
<img src="https://imgur.com/k5mMxPa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14-35
</p>
<br />

<p>
<img src="https://imgur.com/a4eCwKs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14-45
</p>
<br />


<p>
<img src="https://imgur.com/G0x2Aip.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
17
</p>
<br />

<p>
<img src="https://imgur.com/PXLx9i7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
17a
</p>
<br />

<p>
<img src="https://imgur.com/IFT5qjZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
18
</p>
<br />

<p>
<img src="https://imgur.com/hn6yc35.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19
</p>
<br />

<p>
<img src="https://imgur.com/UaxFEXo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19a
</p>
<br />


<p>
<img src="https://imgur.com/aqvkhfY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
23
</p>
<br />


<p>
<img src="https://imgur.com/LTVUuxD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
24
</p>
<br />


<p>
<img src="https://imgur.com/a6AVjiB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
24a
</p>
<br />


<p>
<img src="https://imgur.com/73oekUb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
28
</p>
<br />


<p>
<img src="https://imgur.com/o7V1xZ1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
29
</p>
<br />

<p>
<img src="https://imgur.com/4FaKFBz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
30
</p>
<br />


