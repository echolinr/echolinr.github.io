Authentication
Authentication is a behavior to identify a user or a host. Authentication is one the key features for a security product. When a security product enables authentication, users or hosts can be denied or allowed to access certain networks.
From a user's point of view, authentication is divided into the following categories:
If you are a user from internal network who wants to access Internet, you can use:
Web Authentication
Single Sign-On
PKI
If you are a user from Internet who wants to visit an internal network (usually with VPN), you can use:
SSL VPN
IPSec VPN (IPSec VPN (with radius server)+Xauth)
L2TP VPN (L2TP over IPsec VPN)
Authentication Process
A user uses his/her terminal to connect the firewall. The firewall calls user data from AAA server to check the user's identity.

User: authentication applicant. The applicant initiate an authentication request, and enters his/her username and password to prove his/her identity.
Authentication system (i.e. the firewall in this case): Firewall receives username and password and send the request to AAA server. It is an agent between applicant and AAA server.
AAA Server: authentication server. This server stores user information like username and password, etc. When AAA server receives a legitimate request, it checks if the applicant has the right to user network services, and sends back the decision. For more information, refer to AAA Server. AAA server has the following four types:
Local server
Radius server
LDAP server
AD server
TACACS+server