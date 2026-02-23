# How to setup and configure a small office network


**This guide will show how to**   


<br>1. Configure the Wireless Route<br>
<br>2. Configure the Switch<br>
<br>3. Configure the IoT Server<br>
<br>4. Configure the Printers<br>
<br>5. Configure Desktop PCs to connect to the network<br>
<br>6. Configure Laptops to connect to Wireless Router<br>
<br>7.  Configure Smartphone connection to the Wireless Router<br>
<br>8. Configure IoT devices to connect to the network<br>
<br>9. Using the IoT Monitor to monitor and access IoT Devices<br>
<br>10. Glossary<br>

<br>**First you will see a topology of the network to see how the network and devices are connected. You will then see a table of all the devices that are static on the network. You will then see a list of devices that dynamically join and leave the network. Then there will be the step-by-step instructions, and finally a glossary of terms if you are unsure what something means.**

***

## Network Topology 


<img width="1102" height="719" alt="image" src="https://github.com/user-attachments/assets/0b8cc544-8d3f-4ce4-bc85-2a36fa6a1167" />



## Network devices and configuration


| Device | IPv4 Address | Subnet Mask | DNS Server | Gateway | Connection Type | **Port Connection** |
| --- | --- | --- | --- | --- | --- | --- |
| **Wireless Router** | 192.168.25.254 | 255.255.255.0 |  | Is the Gateway | Wireless on LAN port. Ethernet on WAN port | LAN to Swicth GigabitEthernet0/1 |
| **IoT Server** | 192.168.25.1 | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Cat 5e (Ethernet) | FastEthernet0 to Switch port FastEthernet0/1 |
| **Printer 1** | 192.168.25.3 | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Cat 5e (Ethernet) | FastEthernet0 to Switch port FastEthernet0/2 |
| **Printer 2** | 192.168.25.4 | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Wi-Fi |  |
| **PC Client 1** | 192.168.25.10 | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Cat 5e (Ethernet) | FastEthernet0 to Switch port FastEthernet0/3 |
| **PC Client 2** | 192.168.25.11 | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Cat 5e (Ethernet) | FastEthernet0 to Switch port FastEthernet0/4 |
| **PC Client 3** | DHCP | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Cat 5e (Ethernet) | FastEthernet0 to Switch port FastEthernet0/5 |
| **PC Client 4** | DHCP | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Cat 5e (Ethernet) | FastEthernet0 to Switch port FastEthernet0/6 |
| **IoT Device 1 - Coffee Machine** | DHCP | 255.255.255.0 | Internal network access only |  | Wi-Fi |  |
| **IoT Device 2 - Motion Detector** | DHCP | 255.255.255.0 | Internal network access only |  | Wi-Fi |  |
| **IoT Device 3 - Fan** | DHCP | 255.255.255.0 | Internal network access only |  | Wi-Fi |  |
| **IoT Device 4 - Light** | DHCP | 255.255.255.0 | Internal network access only |  | Wi-Fi |  |




### Dynamically connected Devices
| **Device** | **IPv4 Address** | **Subnet Mask** | **DNS Server** | **Gateway** | **Connection Type** |
| --- | --- | --- | --- | --- | --- |
| **Laptop** | DHCP | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Wi-Fi |
| **Smart Phone** | DHCP | 255.255.255.0 | 192.168.25.1 | 192.168.25.254 | Wi-Fi |


***

## **Step-by-step**

### 1. Configure the Wireless Router

When you have accessed the wireless router setup will be from the GUI tab. The Wireless router will be setup with a static IPv4 address. This is because all network devices such as routers, switches, servers and printers form the structure of network and need to have a fixed IPv4 address for other devices to reliably communicate with them.

***Note*** 
*After initial setup the wireless router can be configured from a web browser by typing in the address bar the wireless router's IP address **192.168.25.254** on a device connected on the office network. However, this would only be for IT admin acces and could be disabled*

#### GUI

Upon entering the GUI you will see the Setup tab. 

- Under the Network Setup section enter the IP address for the router 192.168.25.254
- The subnet mask will 255.255.255.0
- Static DNS  set to 192.168.25.1

<img width="934" height="701" alt="image" src="https://github.com/user-attachments/assets/873386c7-1e77-4257-8de2-bba80cffad06" />


- Then click **save settings**

- Next click on the **Wireless** tab and change the **Network Name (SSID)** from Default to SmartOffice.
- Then scroll to bottom and click **save settings**

<img width="934" height="701" alt="image" src="https://github.com/user-attachments/assets/58131611-dd9e-4fd8-877e-d9a6ca0f4ced" /><br>


- Next you click on **Wireless Security** in the same tab


<img width="410" height="50" alt="image" src="https://github.com/user-attachments/assets/efedcdb1-c42c-4fd8-ac40-e77614ff2704" /><br>


- You will see **Security Mode**. Click the down arrow on Disabled and click on WAP2 Personal

<img width="669" height="253" alt="image" src="https://github.com/user-attachments/assets/b44412a1-242e-440c-bce0-8f5f26f6b635" /><br>


- Next enter the **Passphrase** (Currently set to **Office123**)
- Then click **save settings**


***

### 2. Configure the Switch


The switch will be configured with a static IPv4 address.

- At the CLI (Command Line Interface) enter ***enable***

```
Switch> enable
```

- Then enter ***configure terminal***

```
Switch# configure terminal
# or
Switch# conf t
```

- You will then see the output ==*Enter configuration commands, one per line. End with CNTL/Z.*==

- You will then configure the name of the switch with the following command ***hostname*** and the name of the you are going to call the switch. Ensure the name reflects what it is and which building it is situated. eg.

```
Switch(config)# hostname SW1_NE_JustIT_Office
```

- You will then set a password for the console port, which offers direct acess to configure the switch. And also configure secure SSH (Secure Shell) for remote access.

- enable secret = enabling an encrypted password followed by the password

```
SW1_NE_JustIT_Office(config)# enable secret Ju$t!t 
```

- now to secure the console port with a password

```
SW1_NE_JustIt_Office(config)# line console 0

SW1_NE_JustIT_Office(config-line)# password Ju$t!T

SW1_NE_JustIT_Office(config-line)# login
```


- then secure SSH remote access
	- exit command drops executive user back to switch config

```
SW1_NE_JustIT_Office(config-line)# line vty 0 15

SW1_NE_JustIT_Office(config-line)# pasword Ju$t!t

SW1_NE_JustIT_Office(config-line)# login

SW1_NE_JustIT_Office(config-line)# exit
```

- then to encrypt all plaintext passwords

```
SW1_NE_JustIT_Office(config)# service password-encryption
```

- next to put a warning message for anyone unauthorised to access the switch

```
SW1_NE_JustIT_Office(config)# banner motd #Warning! No unathorised access allowed. Password required.#
```

- next to configure an ip address to remotely access the switch

```
SW1_NE_justIT_Office(config)# interface vlan 1

SW1_NE_JustIT_Office(config-if)# ip address 192.168.25.253 255.255.255.0
```

- the no shutdown command will change the vlan1 interface state to up

```
SW1_NE_JustIT_Office(config-if)# no shutdown
```

- next type exit and press enter. Then to configure the default-gateway ip address so that all data packets that need to reach the wireless router and out to other networks can.
	- after typing command then type exit and enter and enter again.

```
SW1_NE_JustIT_Office(config)# ip default-gateway 192.168.25.254
```


- next to save the configurations

```
SW1_NE_JustIT_Office# copy running-config startup-config
```
 

- to show switch configurations ensure executive mode is enabled after login. Then type the following to show startup-config and or the running-config

```
SW1_NE_JustIT_Office# show start-config

SW1_NE_JustIT_Office# show running-config
```


- Finally connect a **Cat 5e** Ethernet cable in the **GigabitEthernet0/1** port of the switch, which is its WAN port for accessing the other networks and the internet via the router, and connect the other end to one of the wireless router LAN ports.



***



### 3. Configure the IoT Server

The IoT server will be configured with a static IPv4 address

**Note**
***The IoT server is also the DNS server in this instance***

- First click on the **Services** tab
- Then click on **DNS** option on left side and click the **on** radial button.

<img width="726" height="290" alt="image" src="https://github.com/user-attachments/assets/502975be-c4ab-498f-9267-f875c8859371" /><br>

- Next click on the **IoT** option on left side and click the **on** radial button, if not already on.<br>

<img width="723" height="362" alt="image" src="https://github.com/user-attachments/assets/05845995-b4ab-4960-b935-a6378b5b88cd" /><br>


- Next click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **Static**
- Then enter the IPv4 address for the **Default-gateway** which is the IPv4 address for the wireless router - ***192.168.25.254***
- Then enter the IPv4 address for the **DNS server** - ***192.168.25.1*** (which is is also the the IPv4 address for the **IoT server**)<br>

<img width="731" height="472" alt="image" src="https://github.com/user-attachments/assets/1bea465e-20ec-4aee-bd54-7417235676d8" /><br>


- Next click on the **FastEthernet0** option on left side
- Under **IP configuration** section ensure the radial button is set to **Static**
- Enter the **IPv4 address** - ***192.168.25.1***
- The **Subnet Mask** will automatically appear and for the IPv4 addres set will be ***255.255.255.0***<br>


<img width="731" height="472" alt="image" src="https://github.com/user-attachments/assets/5e1759b3-298b-4c47-aee2-4cfd22bfe3c8" /><br>


- Next click on the **Desktop** tab and then scroll down and double click on the **IoT Monitor**
- This will open the **IoT server monitor** login page
	- the monitor is used for monitoring and accessing the IoT devices on the network.<br>


<img width="731" height="472" alt="image" src="https://github.com/user-attachments/assets/adb1d330-870a-4616-bf97-d4df13edbed2" /><br>


- If an account login has been set up just login
	- currently set as username***admin*** and password ***justit***
		- if no account present, after first login attempt with ***admin*** ***admin*** there will be a prompt to register. Enter a username and password and login.
	 
**Note**
***You will need the username and password for configuring IoT device access.***


- Finally conenct a **Cat 5e** Ethernet cable to the **FastEthernet0** port of the server and the other end to **FastEthernet0/1** port of the **Switch**<br>


***


### 4. Configure the Printers

The printers will be configured with static IPv4 addresses.

#### Printer 1 (Ethernet connected)

- Next click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **Static**
- Then enter the IPv4 address for the **Default-gateway** which is the IPv4 address for the wireless router - ***192.168.25.254***
- Then enter the IPv4 address for the **DNS server** - ***192.168.25.1***<br>


<img width="1024" height="487" alt="image" src="https://github.com/user-attachments/assets/f99d0459-582e-41d3-ac32-f40d9eeeea1a" /><br>


- Next click on the **FastEthernet0** option on left side
- Under **IP configuration** section ensure the radial button is set to **Static**
- Enter the **IPv4 address** - ***192.168.25.3***
- The **Subnet Mask** will automatically appear and for the IPv4 addres set will be ***255.255.255.0***<br>


<img width="1024" height="487" alt="image" src="https://github.com/user-attachments/assets/ee920604-da85-475a-bc68-261f1ea0b512" /><br>


- Finally conenct a **Cat 5e** Ethernet cable to the **FastEthernet0** port of Printer 1 and the other end to **FastEthernet0/2** port of the **Switch**


#### Printer 2 (wireless)

This printer is configured to DHCP

**Note**
*Ensure that wireless module is connected. For this printer it is the WMP300N module provides one 2.4GHz wireless interface suitable for connection to wireless networks. The module supports protocols that use Ethernet for LAN access.*


- Click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **Static**
- Then enter the IPv4 address for the **Default-gateway** which is the IPv4 address for the wireless router - ***192.168.25.254***
- Then enter the IPv4 address for the **DNS server** - ***192.168.25.1***<br>


<img width="1024" height="487" alt="image" src="https://github.com/user-attachments/assets/2406008a-7e17-47d5-ba8f-95164b89107f" /><br>


- Next click on the **Wireless0** option on left side
- In the first section change the default for **SSID** to the SSID for the **Wireless Router** which is *SmartOffice*
- In the next section **Authentication** click the radial button for WPA2-PSK
	- Next enter the **PSK Pass Phrase** *Office123*, which is the SSID password for the Printer to be able to wirelessly connect to the wireless router
- Under **IP configuration** section ensure the radial button is set to **Static**
- Enter the **IPv4 address** - ***192.168.25.4***
- The **Subnet Mask** will automatically appear and for the IPv4 addres set will be ***255.255.255.0***<br>


<img width="1030" height="607" alt="image" src="https://github.com/user-attachments/assets/40041439-e84d-4202-a888-355d989a9744" /><br>


- Printer 2 is now wirelessly connected to the wireless router.


***

### 5. Configure Desktop PCs to connect to the network

Ethernet connected with Static IP address Desktop PC configuration

- Click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **Static**
- Then enter the IPv4 address for the **Default-gateway** which is the IPv4 address for the wireless router - ***192.168.25.254***
- Then enter the IPv4 address for the **DNS server** - ***192.168.25.1***<br>


<img width="817" height="674" alt="image" src="https://github.com/user-attachments/assets/4bd63cde-9609-4f77-a158-484564f2eb8e" /><br>


- Next click on the **FastEthernet0** option on left side
- Under **IP configuration** section ensure the radial button is set to **Static**
- Enter the **IPv4 address** - ***192.168.25.10*** (See the table above for the correspnding IPv4 address)
- The **Subnet Mask** will automatically appear and for the IPv4 addres set will be ***255.255.255.0***<br>


<img width="817" height="674" alt="image" src="https://github.com/user-attachments/assets/d81c1f3a-4597-44f9-bfd8-78880961e3ea" /><br>


Ethernet connected DHCP configured Desktop PC

- Click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **DHCP**
- The **Default-gateway** IPv4 address for the wireless router - ***192.168.25.254*** and the IPv4 address for the **DNS server** - ***192.168.25.1*** will automatically appear once a connection to the wireless router has been established.<br>


<img width="817" height="674" alt="image" src="https://github.com/user-attachments/assets/78f6ff19-bea4-4ebc-affd-c6a52530acdf" /><br>


- Next click on the FastEthernet0 section on left side.
- Under **IP configuration** section ensure the radial button is set to **DHCP**
	- The Desktop PC will then broadcast a request to the **Wireless Router** via ethernet for an IPv4 address.
	- Once a connection has been achieved an IPv4 address will appear.<br>


  <img width="817" height="674" alt="image" src="https://github.com/user-attachments/assets/5154c18f-60aa-48c8-92af-c2e787187869" /><br>


  ***


  ### 6. Configure Laptops to connect to Wireless Router

**Note**
*Ensure that wireless module is connected. For the laptop it is the Linskeys-WMP300N module provides one 2.4GHz wireless interface suitable for connection to wireless networks. The module supports protocols that use Ethernet for LAN access.*


- Click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **DHCP**
- The **Default-gateway** IPv4 address for the wireless router - ***192.168.25.254*** and the IPv4 address for the **DNS server** - ***192.168.25.1*** will automatically appear once a connection to the wireless router has been established.

- Next click on the **Wireless0** option on left side
- In the first section change the default for **SSID** to the SSID for the **Wireless Router** which is *SmartOffice*
- In the next section **Authentication** click the radial button for WPA2-PSK
	- Next enter the **PSK Pass Phrase** *Office123*, which is the SSID password for the Printer to be able to wirelessly connect to the wireless router
- Under **IP configuration** section ensure the radial button is set to **DHCP**
	- The laptop will then broadcast a request to the **Wireless Router** for an IPv4 address.
	- Once a connection has been achieved an IPv4 address will appear.<br>


  <img width="1035" height="702" alt="image" src="https://github.com/user-attachments/assets/3502965f-7e10-4f2b-b2ed-a563213b1e86" /><br>


  <img width="1035" height="702" alt="image" src="https://github.com/user-attachments/assets/699a1e65-43e7-4ba5-b35d-9a5e0785e929" /><br>


  
- With a connection established the laptop is ready to communicate on the network.


***


### 7.  Configure Smartphone connection to the Wireless Router


- Click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **DHCP**
- The **Default-gateway** IPv4 address for the wireless router - ***192.168.25.254*** and the IPv4 address for the **DNS server** - ***192.168.25.1*** will automatically appear once a connection to the wireless router has been established.

- Next click on the **Wireless0** option on left side
- In the first section change the default for **SSID** to the SSID for the **Wireless Router** which is *SmartOffice*
- In the next section **Authentication** click the radial button for WPA2-PSK
	- Next enter the **PSK Pass Phrase** *Office123*, which is the SSID password for the Printer to be able to wirelessly connect to the wireless router
- Under **IP configuration** section ensure the radial button is set to **DHCP**
	- The laptop will then broadcast a request to the **Wireless Router** for an IPv4 address.
	- Once a connection has been achieved an IPv4 address will appear.<br>


  <img width="1035" height="702" alt="image" src="https://github.com/user-attachments/assets/ad662ac8-1ef6-4a9c-953b-d1fc8ecde4c5" /><br>


  <img width="1035" height="702" alt="image" src="https://github.com/user-attachments/assets/880ad02f-be74-4a43-9bf4-fe0c61a1dea9" /><br>


  ***


  ### 8. Configure IoT devices to connect to the network


- Click on the **Config** tab.
- In the first option under **Global settings** change the **Display Name**
- In the section below display name ensure the **Gateway/DNS IPv4** is set to **DHCP**
- The **Default-gateway** IPv4 address for the wireless router - ***192.168.25.254*** and the IPv4 address for the **DNS server** - ***192.168.25.1*** will automatically appear once a connection to the wireless router has been established.
- Next scroll down to **IoT Server** section.
- Click on the **Remote Server** radial button
- For **Server Address** enter the IPv4 address for the **IoT Server** *192.168.25.1*
- For **Username** enter *admin*
- For **Password** enter *justit*
	- these are the login details for the **IoT Monitor**. Once connected all IoT devices can be monitored and accessed remotely.<br>


  <img width="1880" height="867" alt="image" src="https://github.com/user-attachments/assets/88b4e3f8-c2c9-48da-94bc-65e6ab9f454b" /><br>


- Next click on the **Wireless0** option on left side
- In the first section change the default for **SSID** to the SSID for the **Wireless Router** which is *SmartOffice*
- In the next section **Authentication** click the radial button for WPA2-PSK
	- Next enter the **PSK Pass Phrase** *Office123*, which is the SSID password for the Printer to be able to wirelessly connect to the wireless router
- Under **IP configuration** section ensure the radial button is set to **DHCP**
	- The laptop will then broadcast a request to the **Wireless Router** for an IPv4 address.
	- Once a connection has been achieved an IPv4 address will appear.<br>


  <img width="1038" height="760" alt="image" src="https://github.com/user-attachments/assets/ed2c9cf7-a7b0-4df9-941e-e4544537abb5" /><br>


  ***


  ### 9. Using the IoT Monitor to monitor and access IoT Devices

**Note**
*The IoT Monitor can be accessed by any device with a web browser*

- Open a browser and enter the IPv4 address for the IoT server *192.168.25.1*<br>


<img width="1038" height="760" alt="image" src="https://github.com/user-attachments/assets/9b7825e4-a12a-4b53-bb39-ffe96450c04f" /><br>


- Next enter the **username** *admin* and **password** *justit* and then press **enter**
- You will then see the **Home** page where you will see the all the IoT devices configured to be on the network.<br>


<img width="1038" height="760" alt="image" src="https://github.com/user-attachments/assets/00e91802-f486-4176-93e2-07b20d0f6ad9" /><br>


- Click on any of the IoT devices listed and a box will drop showing what you can do. For example, the **Coffee machine** can be turned on from the IoT Monitor by simply clicking the red button to green, turning the coffee machine on.<br>


<img width="1002" height="732" alt="image" src="https://github.com/user-attachments/assets/8c01df26-5431-4407-a872-79933a180d68" /><br>


<img width="1002" height="732" alt="image" src="https://github.com/user-attachments/assets/5961b6b9-dbc3-4a34-a27d-988ec5a1b722" /><br>


***


## **Glossary:**

**Cat 5e (Ethernet)**

**Cat 5e** refers to the **Category 5 Enhanced** cabling standard, an improved version of the original Cat 5 cable, designed for modern computer networks. It supports data transfer rates up to **1 Gbps (Gigabit Ethernet)** and operates at a bandwidth of **100 MHz**, making it suitable for most home and small business networks.


**DHCP (Dynamic Host Configuration Protocol)**

- DHCP assigns devices an IP address, and for the purposes of this guide the focus is IPv4 addresses.
	- DHCP can also provide IPv6 address, but that is out of scope for this guide
 
- IP addresses are typically dynamic and will be on a short lease, a day or two. This allows for devices, such as wireless devices to connect and leave a local network without DHCP running out of IP addresses.
- Devices that are a fixture of a network, such as servers, router, switches and printers are configured to have a reserved IP addresses. This means that until the device is removed from a network other devices can reliably discover abd communicate with the device.
- whether connecting wirelessly or via an Ethernet cable, for example, a device will request a IP address to communicate. This is called DORA

DORA

Discover, Offer, Request, Acknowledge

Discover – Broadcasts on the global network for MAC addresses. FF:FF:FF:FF:FF:FF. All machines will receive that packet on that network. Only the DHCP server will accept it.

Offer – Looks for available leases, and offer the first available leasable IP to the machine on the available/lease list.

Request – Machine accepts the IP.

Acknowledge – DHCP server assigns the IP, and moves that IP from the lease list to the assigned list.

**DNS (Domain Name System)**

DNS is essentially a server that is a phonebook for the internet. 
- Users only know websites by human readable text, such as (https://bbc.co.uk) 
- Behind the text is an IPv4 address, typically, however, users would not remeber these.
- DNS is a server that will translate the website url into a machine readable format

**for a detailed explanation of DNS - [Wikipedia](https://en.wikipedia.org/wiki/Domain_Name_System)

**Gateway (Default)**

A **default gateway** is the node in a computer network—typically a router—that serves as the **forwarding host to other networks** when no specific route matches the destination IP address of a packet. It acts as the **"exit point"** for traffic leaving a local network, enabling communication with devices on external networks, including the internet.

This gateway is essential for any device that needs to send data beyond its local subnet. Without it, devices could only communicate within their immediate network.


**IoT Device**

IoT devices are devices such as sensors, thermostats, doors, lights, security cameras, or even coffee machines that can connect to a network either via an ethernet cable, wirelessly, bluetooth, or Zibeewave, for example. 


**IPv4 Address**

An **IPv4 address** is a 32-bit numerical label assigned to devices on a network, enabling communication over the internet or local networks.  It is typically represented in **dotted decimal notation**, consisting of four numbers separated by dots (e.g., `192.168.1.1`), with each number ranging from 0 to 255. 

### Key Features:
- **32-bit Address Space**: Supports approximately **4.3 billion unique addresses**. 
- **Structure**: Divided into **four octets** (8 bits each), used to identify both the **network** and **host** portions. 
- **Address Classes**: Originally divided into classes (A, B, C, D, E) based on size and use:
  - **Class A**: Large networks (1–126), supports millions of hosts.
  - **Class B**: Medium networks (128–191), up to 65,534 hosts.
  - **Class C**: Small networks (192–223), up to 254 hosts.
  - **Class D**: Reserved for multicast.
  - **Class E**: Reserved for experimental use. 

### Special IPv4 Ranges:
- **Private IPs**: Used internally in networks:
  - `10.0.0.0/8`
  - `172.16.0.0/12`
  - `192.168.0.0/16`
- **Loopback**: `127.0.0.0/8` (e.g., `127.0.0.1` for localhost). 
- **Link-local**: `169.254.0.0/16` (used when DHCP fails).

### Modern Usage:
- **CIDR (Classless Inter-Domain Routing)**: Replaced class-based system for flexible subnetting (e.g., `192.168.1.0/24`). 
- **NAT (Network Address Translation)**: Allows multiple devices to share a single public IP, conserving IPv4 addresses. 
- **IPv4 Exhaustion**: The limited address pool is depleted, leading to the adoption of **IPv6**. 

Despite the rise of IPv6, IPv4 remains widely used due to its established infrastructure.

Static IP Address

- **Fixed**: Remains the same over time.

- **Manual Setup**: Configured manually or reserved via DHCP.

- **Use Cases**: Hosting servers (web, email, FTP), remote access, VoIP, DNS hosting, port forwarding, IP allowlisting.

- **Pros**: Reliable remote access, stable DNS, consistent geolocation, easier firewall rules.

- **Cons**: Higher cost, less privacy, greater security risk (easier to target), requires manual management.

Dynamic IP Address

- **Changes Over Time**: Automatically assigned by DHCP and can change periodically.

- **Automatic Configuration**: No user setup required.

- **Use Cases**: General internet browsing, streaming, gaming, home networks, IoT devices.

- **Pros**: Cost-effective (usually free), enhanced security through obscurity, efficient use of IPv4 space.

- **Cons**: Unreliable for hosting, issues with remote access and DNS, may disrupt services requiring fixed addresses.

**LAN (Local Area Network)**

A **Local Area Network (LAN)** is a network that connects computers and devices within a limited geographic area, such as a home, office, school, or building. It enables devices to **share resources** like files, printers, and internet access, and supports high-speed data transfer using **Ethernet** or **Wi-Fi**.

**Router**

A **router** is a networking device that connects multiple networks and directs data traffic between them by forwarding packets based on IP addresses. It operates at the **network layer (Layer 3)** of the OSI model and is essential for communication between devices on different networks, including internet access.

Key Functions:

- **Traffic Direction**: Routes data packets between networks using IP addresses.

- **Connectivity**: Links LANs to WANs (e.g., home network to the internet).

- **DHCP Server**: Assigns IP addresses to devices on the local network.

- **Firewall & Security**: Provides built-in protection against unauthorized access.

- **Wireless Access**: Most modern routers include Wi-Fi capabilities.


**Server**

A **server** is a computer or software system that provides data, resources, or services to other devices (called **clients**) over a network.  It operates within the **client-server model**, where clients send requests and the server responds with the requested information or service. 

Key Functions:
- **Resource Sharing**: Hosts files, databases, applications, websites, email, printers, and more. 
- **Request-Response Model**: Processes incoming client requests and delivers appropriate responses. 
- **Continuous Operation**: Designed to run 24/7 with high reliability, often using specialized hardware and operating systems. 

Common Types of Servers:
- **Web Server**: Hosts websites (e.g., Apache, Nginx). 
- **File Server**: Stores and manages shared files. 
- **Database Server**: Manages and provides access to databases (e.g., MySQL, PostgreSQL). 
- **Mail Server**: Handles sending and receiving emails (e.g., Microsoft Exchange). 
- **Game Server**: Enables multiplayer online gaming.
- **Proxy Server**: Acts as an intermediary for requests between clients and other servers.
- **Virtual Server**: Runs multiple isolated virtual environments on a single physical machine. 

Servers are typically housed in **data centers** and form the backbone of the internet and enterprise networks.


**SSID**

An **SSID (Service Set Identifier)** is the **name** of a Wi-Fi network that uniquely identifies it.  When you see a list of available Wi-Fi networks on your device, the names displayed are SSIDs. 

Key Points:
- **Purpose**: Helps devices distinguish between different wireless networks in range. 
- **Length**: Up to **32 characters**, case-sensitive. 
- **Broadcast**: Routers broadcast the SSID so nearby devices can find and connect to the network. 
- **Default vs. Custom**: Routers come with a default SSID (e.g., "Linksys123"), but it's recommended to change it for security and clarity. 
- **Security**: The SSID itself does not provide security—authentication is done via password (e.g., WPA2/WPA3). 


**Subnet Mask**

A **subnet mask** is a 32-bit number that divides an IPv4 address into two parts: the **network portion** and the **host portion**.  It determines which part of an IP address identifies the network and which identifies the specific device (host) on that network. 

For example:
- IP Address: `192.168.1.10`
- Subnet Mask: `255.255.255.0`
  - Network: `192.168.1.0`
  - Host: `.10`

This setup allows **254 usable host addresses** (from `.1` to `.254`) in the same subnet. 

Subnet masks enable efficient routing, improve network performance, and enhance security by segmenting large networks into smaller subnets (subnetting).


**Switch**

A **switch** is a networking device that connects multiple devices within a **local area network (LAN)** and forwards data based on **MAC addresses** at the **data link layer (Layer 2)** of the OSI model.  Unlike a hub, which broadcasts data to all devices, a switch intelligently directs traffic only to the intended recipient, improving network efficiency and security. 

Key Features:
- **Intelligent Traffic Management**: Learns and stores MAC addresses to forward data precisely. 
- **Dedicated Bandwidth**: Each port gets full bandwidth, enabling faster, collision-free communication. 
- **Full-Duplex Communication**: Allows simultaneous sending and receiving of data. 
- **Types**:
  - **Unmanaged Switch**: Plug-and-play, no configuration.
  - **Managed Switch**: Offers advanced control (VLANs, QoS, security).
  - **Layer 3 Switch**: Can route between networks using IP addresses. 

Switches are essential in modern networks for high-speed, reliable internal communication.


**WAN**

A **WAN (Wide Area Network)** is a telecommunications network that spans a large geographic area, connecting multiple **local area networks (LANs)** across cities, countries, or even continents.  It enables communication and data sharing between geographically dispersed locations, such as corporate offices, data centers, and cloud resources. 

Key Features:
- **Connects LANs**: Uses routers to link separate local networks. 
- **Long-Distance**: Designed for extended reach, unlike LANs which are limited to a single location. 
- **Uses Public or Private Infrastructure**: Relies on leased lines, MPLS, VPNs, or cellular networks (4G/5G). 
- **Managed by ISPs or Carriers**: Often operated by third-party providers, unlike LANs which are user-controlled. 
- **Example**: The **Internet** is the largest WAN.

WANs are essential for businesses with remote branches, enabling centralized access to applications, data, and cloud services.



















