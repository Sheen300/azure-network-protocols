<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create an admin and normal user account in DC-1 Active Directory Users and Computers. This will allow two account types to enter into the portal but with limited abilities depending on their Organizational Unit types. One will be created for Employees, and one will be created for Users. Open remote desktop connection and grab the public IP address from DC-1's virtual machine to enter the remote desktop. Enter the credentials as whatever credentials were selected when creating the virtual machine from within Azure originally. 

- Step 2: While in DC-1. Click Start. Type Active Directory Users and Computers. Right-click "mydomain.com". Click New. Organizational Unit. Create a folder for _EMPLOYEES. Repeat and create one for _ADMINS. Go to _ADMINS folder, Right-click. New. First name: Jane. Last name: Doe. Create a name and password for her. Go back to her name in the folder. Right-click. Click Properties. Click on "Member of" up at the top. Add. Type "domain" in the box. Domain Admins. Apply. Done. You should see this.

![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/975c013c-cf58-4adc-b004-eb2873c65852)
![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/be91789e-1b29-4a4b-95f3-4c1e4e0f7e54)
![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/530e8775-f336-4797-b16f-756135f58941)



- Step 3: If you have a Windows PC click on Start and type "remote desktop connection". For MAC, download remote desktop connection from the marketplace. Once remote desktop is up, grab the PUBLIC IP address from 'DC-2' and paste it into the remote desktop connection. See in the images below. Enter into DC-2 Virtual machine that was created. Click on 'Networking' on the left. Grab the NIC PRIVATE IP address. Copy it. You should see an image such as the one below.
- 
![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/29aff6d8-fa0f-49a4-95d1-3afbfe0c94e1)

- Step 4: If you have a Windows PC click on Start and type "remote desktop connection". For MAC, download remote desktop connection from the marketplace. Once remote desktop is up, grab the IP address from 'Client-2' and paste it into the remote desktop connection. See in the images below.

- ![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/dc955308-07cc-4d76-9709-c838744c1f00)
- ![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/622727ca-c6df-4071-adef-2aa876f14826)


- Step 3: While in DC-2 remote desktop, ping the private IP address from Client-2. You should get a reply such as the one seen below. This shows that connectivity between both virtual machines has been successful.

- ![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/a99d3c11-13bb-4e4d-b08d-14ab712364d0)
 

- 
- Step 4: Go back to the Client-2's remote desktop. Click Start. Type cmd. In the command line type "hostname". This shows you that you are in the correct Virtual Machine entitled "Client-2". The same can be done for DC-2 if you are ever confused about which remote desktop connection you are logged in under. 

![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/ef7e81da-7f3f-4b3d-a606-ef9daed1e42e)

- Step 5: In the Client-2's remote desktop, right-click the Start menu, click on Systems, clikc Remote Desktop, click "Select Users that can remotely access this PC". You should see the following image below.

- ![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/b2664602-00d7-4806-a0a1-4b6249a0c05b)

This will ultimately allow other users to access the network without being an Admin, or, only those in which the Admins allow to gain access within specified groups. Type "Domain Users". Click Add. Clikc OK. In the cmd line in Client-2, simply type "logoff". 

- Step 6: Log back into the Client-2's remote desktop with the Client-2's Public IP address found within portal.azure.com Virtual Machines section.

- Step 7: Under DC-2's remote desktop while being logged in as Jane Doe, right-click the Start menu, type PowershellISE, right-click. Enter as an administrator. Copy the script that was given for this specific lab, create a New file in Powershell. Paste the script. See how the new users are created, approximately 10,000 of them. Go back to Active Directory. Users. Domain Users. Observe how many new users have been, and are being currently created.

- ![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/d49fc5c5-63d1-4d66-90eb-77b64cbb4a88)


These new Domain Users now have the ability to log into the remote desktop because Jane has enabled them to do so. Simply click on one of the names. Copy it. Logoff of the Client-2's remote desktop. Re-enter with the User's name and password that you created when initiating the setup. You should be able to log in with the User's credentials. Such as below: 

![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/ccc615a7-4123-4e32-817f-d22ceb2b3f22)
![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/6227d682-4d98-4e35-8b86-51347e5799be)
![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/ffbe0097-f47f-4ef5-bed9-d43aa5ccfd4f)
![image](https://github.com/Sheen300/azure-network-protocols/assets/150862861/f715473c-e46a-4c5d-a424-dc26938c832b)


