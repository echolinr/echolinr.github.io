Deploying Transparent Mode
Transparent mode is also known as bridge mode or transparent bridging mode. Transparent mode is used when the IT administrator does not wish to change its existing network layout, normally the existing network already has set up routers and switches. The firewall will be used as a security device.
Transparent mode has the following advantages:
No need to change IP addresses
No need to set up NAT rule
Under normal circumstances, firewall in the transparent mode is deployed between the router and switch of the protected network, or it is installed between Internet and a company's router. The internal network uses its old router to access Internet, and the firewall only provides security control features.
This section introduces a configuration example of a firewall deployed between a router and a switch. In this example, the administrator use eth0/0 to manage firewall. The firewall's eth0/1 is connected to router (which is connecting to Internet) and eth0/2 is connected to a switch (which is connecting to internal network).

OpenStep 1: Initial log in the firewall
In the administrator's Ethernet properties, set the IPv4 protocol as below.

Connect an RJ-45 Ethernet cable from the computer to the eth0/0 of the device.
In the browser's address bar, type "http://192.168.1.1" and press Enter.
In the login interface, type the default username and password: hillstone/hillstone.
Click Login, and the device's system will initiate.
OpenStep 2: Configure interface and zone
Configure eth0/1 as Internet connected interface.
Select Network > Interface.
Double click ethernet0/1, and configure in the prompt. 

Click OK.
Configure eth0/2 as private network connected interface.
Select Network > Interface.
Double click ethernet0/2, and configure in the prompt. 

Click OK.
OpenStep 3: Configuring policies
Creating a policy to allow visiting Internet.
Select Policy > Security Policy.
Click New.

Click OK.
Creating a policy to allow Internet to visit private network.
Select Policy > Security Policy.
Click New.

Click OK.
The two policies above ensure the communication between private network and Internet. If you want to set up more details, e.g. to limit P2P download, you can add more policies and move new policy above the old one. The match sequence of policy is determined by its position in the policy list, not its ID number.
Open(Optional) Step 4: Configuring VSwitch Interface for managing the firwall.
If you want any PC in the private network to visit and configure the firewall, you can configure a VSwitch interface as management interface.
Select Network > Interface.
Double click vswtichif1.

Click OK.
In any PC of private network, enter the IP address of vswtichif1, you will visit the firewall Web user interface.
 