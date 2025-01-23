# FortiGate Firewall - NAT & Transparent Mode LAB

## Objective

The FortiGate FW - NAT & Transparent Mode Lab project is aimed to provide hands-on experience with configuring and managing the FortiGate firewall in both NAT (Network Address Translation) and Transparent modes. Mastering the setup and configuration of FortiGate in different operational modes and improving the understanding of NAT, IP pools, and port forwarding to manage network traffic effectively by enhancing security posture through policy-based traffic control.

### Skills Learned

- Basic FortiGate configuration
- Network Management 
- Security Management Skills
- Deploying and configuring FortiGate firewall
- Mastering the use of (NAT, IP pools, and Port Forwarding) for Network Address Management.
- Security policy enforcement


### Tools Used

- FortiGate VM: A virtual appliance used in virtualized environments, such as VMware or Hyper-V
- FortiOS Web Interface (GUI)
- FortiOS Command Line Interface (CLI)
- FortiView Dashboard: Built-in monitoring tool for real-time traffic and event analysis.
- Backup and Restore Tools
- FTP/HTTP/HTTPS Servers: For uploading firmware or serving configurations during the lab.
- Traffic Generation Tools
- GNS3 for simulated network devices (e.g., routers, PCs, or switches) to test


*Ref 1: Network Diagram*
 ![image](https://github.com/user-attachments/assets/2dac4155-d22b-4322-933c-e2f07e9898f3)



## STEPS

# FortiGate Operation Modes

* FortiGate have two Operations Modes:

- NAT: this mode is commonly used, by default FortiGate Come in NAT Mode.
	In Nat Mode our FortiGate Behaves as a Router (Routing, NAT, VPN, ...)
	Each Interface of our unit is on a different Subnet.

- Transparent (TP): We use TP Mode when our FortiGate is behind a Router or another Firewall.
		    In TP Mode our FortiGate Behaves as a Switch.
		    We Can't Assign IP@ To interfaces.
		    All Interfaces are on same Subnet.
		    We Must assign a MGMT IP@ For Administration Access.

## TP MODE Configuration ##

** In Order to switch our FGT From Nat mode to TP Mode we need to disable fortilink first **
![image](https://github.com/user-attachments/assets/2e1a6aef-c396-4fee-b454-4a855cc19257)
 

Changing to TP mode

Our FortiGate operation mode is transparent.
So to access our FortiGate, we need to enable HTTP access to this interface here.
![image](https://github.com/user-attachments/assets/0e5f05d1-48bd-4dc7-902c-bf6b892be7e3)
 
Now I will access my web browser.
And they will type the IP address of my FortiGate.
I will access to it, and here in system information in mode, we can see that our FortiGate is successfully transformed to transparent.
![image](https://github.com/user-attachments/assets/96b58fb4-3731-4d88-bced-7743cddfb501)

 

## Note: In "TP mode" we can access to our unit from any interface that have access services enabled (HTTP, SSH ...).



If we go to system settings and we scroll down here, we will find our configuration here in system operating settings.

We find that the current operating mode is transparent and this is the IP that we gave to our FortiGate through the CLI.
 ![image](https://github.com/user-attachments/assets/15671b0b-9f99-43b7-9655-f4cbb1dc7fb4)


# Check operation mode from CLI
![image](https://github.com/user-attachments/assets/4fc207f7-fed5-4e00-b929-c86904fb3112)
 


## ROUTER Configuration ##

Now let's see how to give our FortiGate Internet Access, so to give it an Internet access, I need to go back and configure my router here, I've already gave it a IP address, these interfaces.
![image](https://github.com/user-attachments/assets/c1a8cc20-8972-49ef-848b-a6fbebebdd99)
 
 

interface FastEthernet0/0
![image](https://github.com/user-attachments/assets/36543056-d4a5-404c-b9b9-8f91277ccdd2)
 
interface FastEthernet1/0


In order to access the Internet, we need to we need to configure NAT in our router.
So, to do it, I will go to config terminal and first I will create an access list.
A standard access list and they will permit my subnet.
![image](https://github.com/user-attachments/assets/8d2a75fd-642f-425d-bc14-8ad127a77b8b)
 

NAT Translations
![image](https://github.com/user-attachments/assets/bd957713-d742-464f-b4bc-8b2ca0615cfa)
 

Now let's try to ping the internet from our router.
Perfect, it's working.
![image](https://github.com/user-attachments/assets/f1d6c64e-f53b-46da-b14b-d780aca0ddc7)
 

Now let's come back to our FortiGate firewall and PING again, perfect.
Now we can ping internet.
![image](https://github.com/user-attachments/assets/f739719e-8e5b-44a7-95c7-537100acdb00)
![image](https://github.com/user-attachments/assets/bb54944e-ea53-4acb-be59-fbb2d5e4e264)
 
 


### Enabling NAT On TP ###

- Type two IP@ on the MGMT IP one for Administrative Access (LAN) and the second for gateway (WAN).

- Configure IPPOOL With the WAN IP@

- Create a policy and enable nat on it.

- Create a default static route

* MGMT IP@
![image](https://github.com/user-attachments/assets/76b55af4-f135-46ee-928d-6f39ba736e5d)
![image](https://github.com/user-attachments/assets/cd16e971-6acb-41e2-a9b5-4f21a3dd2540)
 
 


* IPOOLL Creation
![image](https://github.com/user-attachments/assets/b73fb26c-d412-4277-ba46-bdc44e8063f9)
 

* NAT Policy Creation
![image](https://github.com/user-attachments/assets/a4626fda-9974-444a-9013-c8e865d81ce1)
 

* Default Static route
![image](https://github.com/user-attachments/assets/c8abd253-9899-4590-8c6f-1e5cbf24eec8)
![image](https://github.com/user-attachments/assets/7b07aa29-6b39-4d66-8603-8bb0e4d46922)
![image](https://github.com/user-attachments/assets/3d85322e-4bd9-42e2-ab2b-461194e406a3)
 
 
 

TEST ping internet
![image](https://github.com/user-attachments/assets/b968a4a0-0353-4822-8ddf-6bfbbae99d82)
![image](https://github.com/user-attachments/assets/c9ad1ff7-6955-41fd-8072-fa5fa8cd0fce)
 
 


#### NAT Configuration ####

In FortiGate We Have 4 Types of NAT:

- Overload: is called also "PAT= Port Address Translation" in this type we can NAT multiple internal IPs to one Public IP using Source and Destination Ports.

- One-To-One: in one-to-one NAT one internal IP@ can be translated to one external IP@ at the same time, we don't use "PAT", So if we have 4 internal clients, we need 4 Public IP@ to Do NAT.

- Fixed Port range: This Nat type is also a "PAT" we can specify the range of internal IP@ that we want them to use our Public IP@.

- Port Block Allocation: This Nat type is also a "PAT" but the difference is that he is allowing us to specify the number of ports that a user (Internal Ip@) can use.

		       Block Size: how many ports are in each block. 128 Port
										   = 1024 PORT.
		       Block Per User: how many Block can each user use. 8 Block 
![image](https://github.com/user-attachments/assets/ceff913c-a83b-4ea4-b6fb-bab743237b4e)
 

# Overload Configuration
![image](https://github.com/user-attachments/assets/fcb06a2d-e8c3-46f4-ad21-9dd309f13994)
![image](https://github.com/user-attachments/assets/6763e134-7530-46ae-9b2b-baeb7a760df0)
![image](https://github.com/user-attachments/assets/e64acdff-1a55-4bd2-bfc3-c264aa93932f)
![image](https://github.com/user-attachments/assets/c6333d87-f239-4e8d-a32c-5ec6d4d4e3d2)
 
 

 

 

# TEST

# One To One NAT Configuration
![image](https://github.com/user-attachments/assets/32fbaa5c-fed1-4759-a900-941db3303eaa)
![image](https://github.com/user-attachments/assets/5790ea80-e175-4ede-8c55-ee3665130fe4)
 
 
Firewall Policy
![image](https://github.com/user-attachments/assets/4316bbc3-f28a-4740-adda-b104ac0101aa)
![image](https://github.com/user-attachments/assets/29b5e842-c728-4006-8d90-6c07c8f9f793)

 
 


# FPR Configuration
![image](https://github.com/user-attachments/assets/e3338956-15a6-4d42-818f-62b092c58e27) 
![image](https://github.com/user-attachments/assets/7b988c32-e493-4cf4-97f9-8afd5f842e83)
 


Configure FW policy
![image](https://github.com/user-attachments/assets/d4e341ea-5d11-426c-98aa-463e18e6f204)
![image](https://github.com/user-attachments/assets/4394a2ea-a9bd-4b8d-ad0c-ff902a381e7b)
![image](https://github.com/user-attachments/assets/6a6f1987-6d8f-402e-a191-7187f25f41e4)
 
 
 

# Clear Users Sessions


# Port Block Allocation Configuration.
![image](https://github.com/user-attachments/assets/6dac7cc8-670a-4edf-bb2b-dc7754ce005e)
 














### DNAT = Destination NAT ###

DNAT help us to publish an internal server to the internet so we can access to it from anywhere.
![image](https://github.com/user-attachments/assets/d6eafac4-7497-4543-99a8-0e548255b9a1)
 

# DNAT Configuration
![image](https://github.com/user-attachments/assets/66cca379-0306-46d2-a0e2-8c4397bdac15)

 

* Web Server:

root@WEB:~# apt update

root@WEB:~# apt install apache2 -y

root@WEB:~# apachectl -D FORGROUND

* VIP Creation


* DNAT Policy Creation
![image](https://github.com/user-attachments/assets/4e078394-561d-4205-9231-229979394f9d)
![image](https://github.com/user-attachments/assets/ce3ac613-a463-4cd9-812c-79e7cc56b0a8)
![image](https://github.com/user-attachments/assets/c6b8b36e-69fa-4404-9cb3-adb9b688b7d8)
 
 
 



# Please Note that you should choose the "VIP OBJECT" in the destination Address

# Port Forwarding
![image](https://github.com/user-attachments/assets/7f21bece-25e1-41ba-8cda-4e532f34d7c9)
 


### Any traffic going through a FortiGate unit has to be associated with a policy ####


# Allow traffic between two interfaces
