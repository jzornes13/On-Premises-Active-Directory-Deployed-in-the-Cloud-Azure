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
    
-  Repeat the same process for our 2nd vm but using windows 10 for the operating system.
-  again name it whatever you want in this case we named it client-1
-  set the resource group to the same one created for the first virtual machine.
-  keep the size of the vcpus the same as the first machine
    -  also use the same location in the first one we used west US 3  
-  Change authentication to "Password"
-  here we are changing the dc controller network interface(nic) from dynamic to static (so it doesn't change)
-  go into dc1 on azure, click networking on left, click network interface "dc-1846 (in blue)

<p>
<img src="https://imgur.com/nSpyl3O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
1

-  click ip configurations 
-  center of page click the box with the info example private ip address, ip version ect.
</p>
<br />

<p>
<img src="https://imgur.com/XyEeLg7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1a

-  then click static to actually change it then save.
</p>
<br />

<p>
<img src="https://imgur.com/JWI7oFz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2a

-  now we are going to open both dc1 and client1 from azure to check to make sure they have the same v-net
-  log into dc1 from azure and copy the private ip address
-  press the windows button on your keyboard, type remote desktop and open it, log into client1 remotely 
-  once inside client1 ping dc1 private ip address(to see it fail), windows button, type cmd prompt, type "ping -t 10.0.0.5(whatever your ip address is)"
-  log into dc1 remotely by copying the ip address from azure and opening the windows prompt and remote desktop connection
-  were going open up the firewall to allow client 1 to successfully ping
-  press the window button, type wfmsc(windows firewall) or type firewall click windows defender firewall with advanced security
-  click inbound rules
-  sort by protocol, your looking for icmpv4(client 1 previous ping failure)
-  in the name section find "icmp echo request", right click and click enable rule as seen below do it for both rules.
-  now check back on client 1 to see the ping is getting a reply instead of timing out.
-  to stop ping press control c 

</p>
<br />

<p>
<img src="https://imgur.com/WfBAXlc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
6

-  now were going to install active directory to make dc 1 and actual domain controller
-  using server manager(if not open click start and search server manager)
-  go to add roles and features, click next, next
-  make sure for destination server it has dc 1
-  then check the box that says active directory DOMAIN SERVICES make sure its the right one then click add features, next all the way through to install.

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

-  at the top right there is an exclamation point, click it and look for the blue writing that says promote this server to a domain controller
</p>
<br />


<p>
<img src="https://imgur.com/gC60m9n.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9

-  click add a new forest, type in what you want to name your domain ex something.com then next
-  make a password (we are never going to use it but good practice to remember it)
-  then next all through to install 
-  wait for it to install and set up domain, it will automatically restart at end so you will have to sign back in using the proper name because its a domain now
-  something.com\whatever user name you had previously signed in with, make sure the slash is facing the right way.
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

-  so as with most things computer related there are a couple of ways you can open active directory, you can go to tools in the server manager dashboard and click active directory users and computers or click start and search active directory.

</p>
<br />

<p>
<img src="https://imgur.com/X8gLd5C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11

-  at the top left you will see the domain name we just created, right click go to new, then organizational unit and create a file name Employees and another file called Admins.

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

-  go to the new admins folder right click, new user, jane doe, user log in jane_admin, next,set password, for this purpose uncheck "user must change password at next login" normally we leave this alone but this is practice, and an unnecessary step in this case.
-  make sure to remember the name and password!
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

-  so now Jane is in the admin folder but not actually and admin, to do that we have to go into the admin folder right click on jane, go to properties, then "member of" tab
-  click add, type domain and the check names button to the right will light up, click that, click domain admins in the multiple names found section, then apply, then ok
</p>
<br />

<p>
<img src="https://imgur.com/k5mMxPa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14-35

-  now log out of remote desktop and log back in as something.com\jane_admin
-  when logging back in if that isn't the selcted name in remote desktop click more choices.
-  we are going to be using this name from now on.
</p>
<br />

<p>
<img src="https://imgur.com/a4eCwKs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14-45

-  now we need to point client 1 dns to use dc 1 and it's domain name server.
-  to do this we have to copy dc 1 private ip address in the azure portal
-  now we go to client 1 (in azure) click networking on left side, then click next to network interface the blue section that says client-1138(or whatever the number say)
-  then click dns servers (on left side of page), click custom, paste dc 1 private ip address in making sure there are no spaces, click save (top left)
-  once it's done updating we are going to restart client 1 from the azure portal (button on top) this will flush it's exsisting dns settings and make it use what we just entered.
-  when we log back in we have to use the original name and password because it isn't joined to the domain just yet do not use jane_admin.
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

-  now that were logged back in under our original name we can do some observations.
-  open the command line by pressing the window button and typing cmd, type whoami, type hostname, type ipconfig/all
-  now we see our new dns server settings making sure they match dc 1 dns we are good to go.

</p>
<br />

<p>
<img src="https://imgur.com/IFT5qjZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
18

-  now we actually point client 1 server to use dc 1, right click the start menu, go to settings or system or system properties as long you find the rename this pc (advanced) button on the right hand side, or advanced system settings or system properties and see rename this computer and click the change button then in computer name/domain changes, click the domain dot and enter your domain in this case it was something.com then ok

</p>
<br />

<p>
<img src="https://imgur.com/hn6yc35.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19

-  the promt will pop up with credentials we will use jane_admin credentials if successful a little window will pop up saying welcome to something.com(it could pop up behind one of your current windows so minimize them and you will see it, click ok

-  the computer will ask to restart say ok
</p>
<br />

<p>
<img src="https://imgur.com/UaxFEXo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19a

-  copy client 1 ip address
-  log back into client one with "domain name" ours was something.com\jane_admin (make sure the slash is the right way
-  click more choices and choose jane_admin for the username
-  right click start menu, go to system, remote desktop(in blue, right hand side), click select users that can remotely access this pc under the user accounts heading.

</p>
<br />


<p>
<img src="https://imgur.com/aqvkhfY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
23

-  click add, type domain users, check names, click ok, ok, now all users can access this pc remotely.
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

-  log back into dc 1 as jane_admin
-  go to the start menu search and open powershell ice as an ADMINISTRATOR
-  create a new page(top left)

</p>
<br />


<p>
<img src="https://imgur.com/73oekUb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
28

-  go to the website below and copy the script to paste into powershell
   -  https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1 
-  after you paste in powershell scroll down to the bottom of the script look for the path "ou=_EMPLOYEES,$(([ADSI]`"").distinguishedName)" `, Now that "_EMPLOYEES" needs to be spelled the same with the underscore as the file we created in active directory or it will not work you will get an error message, also worth noting if you are running powershell as a non-admin it will not work and the same for running powershell from client 1 it has to be in dc 1.
</p>
<br />


<p>
<img src="https://imgur.com/o7V1xZ1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
29

-  observe all the users being created
</p>
<br />

<p>
<img src="https://imgur.com/4FaKFBz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
30
</p>
<br />


