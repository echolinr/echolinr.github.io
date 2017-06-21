Deploying Tap Mode
In most cases, the security device is deployed within the network as a serial node. However, in some other scenarios, an IT administrator would just want auditing and statistical functions, like IPS, antivirus, Internet behavior control. For these features, you just need to connect the device to a mirrored interface of core network. The traffic is mirrored to the security device for auditing and monitor.

The bypass mode is realized by binding a physical interface to Tap zone, then the interface becomes a bypass interface. The device will monitor, scan, or record the traffic received in the bypass interface.

Use an Ethernet cable to connect e0 of Switch and e1 of the Hillstone device. The interface e1 is the bypass interface and e2 is the bypass control interface. The interface e0 is the mirror interface of the switch.The switch mirrors the traffic to e1 and Hillstone device will monitor, scan, and log the traffic received from e1. After configuring IPS, AV, or network behavior control on the Hillstone device, if the device detects network intrusions, virus, or illegal network behaviors, it will send TCP RST packet from e2 to the switch to tell it to reset the connections.
Before configuring tap mode in the device, you need to set up interface mirroring in your primary switch. Mirror the traffic of the switch from e0 to e1, and the device can scan, monitor and count the mirrored traffic.
Here provides an example of monitoring IPS in tap mode.
OpenStep 1: Creating tap mode by binding an interface
Select Network > Zone, and click New. 

Option	Value
Zone	enter a name, e.g. "tap-zone" .
Type	TAP
Binding Interface	Select the bypass interface (only a physical interface, aggregate interface or redundant interface can apply, sub-interface is not allowed).
Click OK.
OpenStep 2: Creating an IPS rule
Select Object > Intrusion Prevention System.
Click New.
Enter the rule name.
Configure the signatures settings.
Configure the protocol settings.
Click OK to complete IPS rule configuration.
OpenStep 3: Add IPS rule into Tap zone
Select Network > Zone, and double-click the tap zone created in step 1.
In the Treat Prevention tab, enable IPS and select the IPS rule just created.

Click OK.
Open(Optional) Block traffic in switch
A bypass control interface is used to send control packets (TCP RST packet is supported in current version). After configuring IPS, AV, or network behavior control on the Hillstone device, if the device detects network intrusions, virus, or illegal network behaviors, it will send TCP RST packet from e2 to the switch to tell it to reset the connections.
By default, the bypass interface itself is the control interface. However, you may also change the control interface.
To change a bypass control interface, you can only use command line interface:
tap control-interface interface-name
interface-name - Specifies which interface is used as bypass control interface.
 
 