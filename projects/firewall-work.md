How a Firewall Works
A firewall is a network security device. It protects a network by controlling the traffic that comes in and out of a network. The basic mechanism of how a firewall works is allowing or disallowing data packets by matching its policy rules. Besides security functions, a firewall can also works as a bridging device to connect a trust zone (internal network) and untrust zone (external network).
StoneOS System Architecture
The elements that consist StoneOS system architecture are:
Zone: Zones divide network into multiple segments, for example, trust (usually refers to the trusted segments such as the Intranet), untrust (usually refers to the untrusted segments where security treats exist), and so on.
Interface: Interface is the inlet and outlet for traffic going through security zones. An interface must be bound to a security zone so that traffic can flow into and from the security zone. Furthermore, for the Layer 3 security zone, an IP address should be configured for the interface and the corresponding policy rules should also be configured to allow traffic transmission between different security zones. Multiple interfaces can be bound to one security zone, but one interface cannot be bound to multiple security zones.
VSwitch: VSwitch is short for Virtual Switch. A VSwitch functions as a switch in Layer 2. After binding a Layer 2 zone to a VSwitch, all the interfaces in the zone are also bound to the VSwitch. There is a default VSwitch named VSwitch1. By default, all Layer 2 zones will be bound to VSwitch1. You can create new VSwitches and bind Layer 2 zones to VSwitches. Each VSwitch is a Layer 2 forwarding zone with its own MAC address table which supports the Layer 2 traffic transmission for the device. Furthermore, the VSwitchIF helps on the traffic transmission between Layer 2 and Layer 3.
VRouter: VRouter is Virtual Router and also abbreviated as VR. A VRouter functions as a router with its own routing table. There is a default VR named trust-vr. By default, all the Layer 3 zones will be bound to trust-vr automatically. The system supports the multi-VR function and the max VR number varies from different platforms. Multiple VRs make the device work as multiple virtual routers, and each virtual router uses and maintains its own routing table. The multi-VR function allow a device to achieve the effects of the address isolation between different route zones and address overlapping between different VRs, as well as to avoid route leaking to some extent, enhancing route security of network.
Policy: Policy is to control the traffic forwarding between security zones/segments. By default Hillstone devices will deny all traffic between security zones/segments, while the policy can identify which flow between security zones or segments will be permitted, and which will be denied, specifically based on policy rules
For the relationship between interface, security zone, VSwitch and VRouter, see the following diagram:

As shown above, the binding relationships among them are:
Interfaces are bound to security zones. Interfaces bound to Layer 2 security zones and Layer 3 security zones are known as Layer 2 interfaces and Layer 3 interfaces respectively. One interface can be only bound to one security zone; interface and its sub interface can belong to different security zones.
Security zones are bound to a VSwitch or VRouter. Layer 2 security zones are bound to a VSwitch (by default the predefined Layer 2 security zone is bound to the default VSwitch1), and Layer 3 security zones are bound to a VRouter (by default the predefined Layer 3 security zone is bound to the default trust-vr), thus realizing the binding between the interfaces and VSwitch or VR. One security zone can be only bound to one VSwtich or VR.
General Rules of Security Policy
By default, all interfaces, even in the same zone, cannot communicate. Traffic in different zone are not allowed to be transferred either. In order to change the rule, you need to set up new policy rules to allow traffic forwarding.
To allow bidirectional traffic, you need to set up two policies: one is from source to destination, the other is from destination to source. If there is only one-direction initiative access, the responsive direction only need to respond to that visit, you will need to create only one-way policy (from source to destination).
This part explain what policy is needed to allow interfaces in different zones, VSwtiches or Vrouteres to communicate. The rules are:
Interfaces in the same zone 
To allow interfaces in one same zone to communicate, you need to create a policy whose source and destination are both the zone the interfaces belong. 
For example, to allow eth0/0 and eth0/1 to communicate, you need to create an "allowing" policy with source L3-zone and destination L3-zone. 
Zones of two interfaces are under the same VSwtich 
To allow communication of interfaces in different zones under one same VSwitch, you need to create two policies: one policy to allow traffic from a zone to another; the other policy to allow traffic in the opposite direction. 
For example, to allow eth0/2 and eth0/3 to communicate, you should create a policy whose source is L2-zone1 and destination is L2-zone2, then create another policy to allow traffic from L2-zone2 to L2-zone1. 
Zones of two interfaces are under different VSwitches 
Each VSwtich has its VSwtich interface (VSwitchIF) which is bound to a Layer-3 zone. To allow interfaces in different zones under different VSwtiches, you need to create an "allowing" policy in which the source is the zone of one VSwtichIF and the destination is the the zone of the other VSwtichIF. After that, create another policy of the opposite direction.
Zones of two L3 interfaces are under the same VRouter 
To allow two L3 interfaces to communicate, you need to create a policy allowing one zone to the other zone. 
For example, to allow communication between eth0/0 and eth0/5, you should create a policy from L3-zone1 to L3-zone2, and then create an opposite direction policy.
Zones of two L3 interfaces are under different VRouters 
To allow two L3 interfaces in two different zones of different VRouters, you need to create a policy with source being one VRouter and destination with the other VRouter, then you create an opposite direction policy.
An L2 interface and an L3 interface under the same VRouter 
To allow communication between an L2 interface and an L3 interface under the same VRouter, you will need to create a policy whose source is the zone which binds the VSwithIF of L2 interface and the destination is the zone of L3 interface. After taht, create an opposite direction policy. 
For example, to allow eth0/0 and eth0/2 to communicate, create a policy from L3-zone1 to L2-zone1, and its opposite direction policy.
Packet Processing Rule
Forwarding Rule in Layer 2
Forwarding within Layer 2 means it is in one VSwitch. The StoneOS system creates a MAC address table for a VSwitch by source address learning. Each VSwitch has its own MAC address table. The packets are forwarded according to the types of the packets, including IP packets, ARP packets, and non-IP-non-ARP packets.
The forwarding rules for IP packets are:
Receive a packet.
Learn the source address and update the MAC address table.
If the destination MAC address is a unicast address, the system will look up the egress interface according to the destination MAC address. And in this case, two situations may occur:
If the destination MAC address is the MAC address of the VSwitchIF with an IP configured, the system will forward the packet according to the related routes; if the destination MAC address is the MAC address of the VSwitchIF with no IP configured, the system will drop the packet.
Figure out the egress interface according to the destination MAC address. And if the egress interface is the source interface of the packet, the system will drop the packet; otherwise, forward the packet from the egress interface.
If no egress interfaces (unknown unicast) is found in the MAC address table, jump to Step 6 directly.
Figure out the source zone and destination zone according to the ingress and egress interfaces.
Look up the policy rules and forward or drop the packet according to the matched policy rules.
If no egress interface (unknown unicast) is found in the MAC address table, the system will send the packet to all the other L2 interfaces. The sending procedure is: take each L2 interface as the egress interface and each L2 zone as the destination zone to look up the policy rules, and then forward or drop the packet according to the matched policy rule. In a word, forwarding of unknown unicast is the policy-controlled broadcasting. Process of broadcasting packets and multicasting packets is similar to the unknown unicast packets, and the only difference is the broadcast packets and multicast packets will be copied and handled in Layer 3 at the same time.
For the ARP packets, the broadcast packet and unknown unicast packet are forwarded to all the other interfaces in the VSwitch, and at the same time, the system sends a copy of the broadcast packet and unknown unicast packet to the ARP module to handle.
Forwarding Rule in Layer 3

Identify the logical ingress interface of the packet to determine the source zone of the packet. The logical ingress interface may be a common interface or a sub-interface.
The system performs sanity check to the packet. If the attack defense function is enabled on the source zone, the system will perform AD check simultaneously.
Session lookup. If the packet belongs to an existing session, the system will perform Step 11 directly.
DNAT operation. If a DNAT rule is matched, the system will mark the packet. The DNAT translated address is needed in the step of route lookup.
Route lookup. The route lookup order from high to low is: PBR > SIBR > SBR > DBR > ISP route.
Till now, the system knows the logical egress and destination zone of the packet.
SNAT operation. If a SNAT rule is matched, the system will mark the packet.
VR next hop check. If the next hop is a VR, the system will check whether it is beyond the maximum VR number (current version allows the packet traverse up to three VRs). If it is beyond the maximum number, the system will drop the packet; and if it is within the maximum number, return to Step 4. If the next hop is not a VR, go on with policy lookup.
Policy lookup. The system looks up the policy rules according to the packet’s source/destination zones, source/destination IP and port, and protocol. If no policy rule is matched, the system will drop the packet; if any policy rule is matched, the system will deal with the packet as the rule specified. And the actions can be one of the followings:
Permit: Forwards the packet.
Deny: Drops the packet.
Tunnel: Forwards the packet to the specified tunnel.
Fromtunnel: Checks whether the packet originates from the specified tunnel. The system will forward the packet from the specified tunnel and drop other packets.
WebAuth: Performs WebAuth on the specified user.
First time application identification. The system tries to identify the type of the application according to the port number and service specified in the policy rule.
Establish the session.
If necessary, the system will perform the second time application identification. It is a precise identification based on the packet contents and traffic action.
Application behavior control. After knowing the type of the application, the system will deal with the packet according to the configured profiles and ALG.
Perform operations according to the records in the session, for example, the NAT mark.
Forward the packet to the egress interface.