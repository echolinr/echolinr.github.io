Deploying Routing Mode
Routing mode deployment often use NAT function as well, so it is also called NAT mode. In routing mode, each interface has its IP address which means interfaces are in the layer 3 zone. A firewall in routing mode can work as a router and a security devcie.
Routing mode is mostly used when the firewall is installed between an internal network and Internet.
This example is based on the topology below to show you how to connect and configure a new Hillstone device in route mode. The device connects a private network to Internet.

Step 1: Connecting to the device
Connect one port (e.g. eth0/1) of Hillstone device to your ISP network. In this way, "eth0/1" is in the untrust zone.
Connect your internal network to another Ethernet interfaces (e.g. eth0/0) of the device. This means "eth0/0" is connected to the trust zone.
Power on the Hillstone device and your PCs.
If one of the internal interfaces already has been configured with an IP address, use a browser to visit that address from one of your internal PCs. 
If it is a new device, use the methods in Initial Visit to Web Interface to visit.
Enter "hillstone" for both username and password.
Step 2: Configuring interfaces
Go to Network > Interface.
Double click eth0/1.

OpenIn the Ethernet Interface dialog box, enter values
Option	Value
Binding Zone
L3-zone
Zone	
untrust
Type	Static IP
IP Address	202.10.1.1 (public IP address provided by your ISP)
Netmask	255.255.255.0
Management	
Select protocols that you want to use to access the device.
Click OK.
Step 3: Creating a NAT rule to translate internal IP to public IP
Go to Policy > NAT > SNAT.
Select New

OpenIn the SNAT Configuration dialog box, enter values
Option	Value
Source Address	Address Entry, Any
Destination Address	Address Entry, Any
Egress	Egress interface, ethernet 0/1
Translated	Egress IP
Sticky	Enable
Click OK.
Step 4: Creating a security policy to allow internal users access Internet.
Go to Policy > Security Policy.
Click New.

OpenIn the Policy Configuration dialog box, enter values.
Source Information
Zone	trust
Address	Any
Destination Information
Zone	untrust
Address	Any
Other Information
Service/Service Group	Any
APP/APP Group	-----
Action	Permit
Click OK.
Step 5: Configuring a default route
Go to Network >Routing > Destination Route.
Click New.

OpenIn the Destination Route Configuration dialog box, enter values.
Option	Value
Destination	0.0.0.0 (means all network)
Subnet Mask	0.0.0.0 (means all subnets)
Gateway	
202.10.1.1 (gateway provided by your ISP)
