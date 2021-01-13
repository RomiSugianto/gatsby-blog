---
title: "Deny internet access on Mikrotik"
date: "2021-01-13"
draft: false
path: "/blog/second-title"
---

To prohibit Internet access to certain IP addresses on the internal network, you need to click “IP” – “Firewall” in the router settings, add new rules in the “Filter Rules” tab by clicking “Add New” or “+”.

In the window that opens, specify the following basic parameters:
Chain: forward
Src. Address: for example, the ip address is 192.168.88.200 or the subnet 192.168.88.240/29 which must be denied access to the Internet and allow access to the internal network. Instead of IP, you can specify the MAC address in Src. MAC Address
Dst. Address: e.g. 192.168.88.0/24 (subnet mask /24 means the range 192.168.88.1 to 192.168.88.254)
Action: accept
This rule allows packets to reach the specified ip range (Dst. Address), that is, on the internal network.
Also, in the “IP” – “DHCP Server” – “Leases” tab, if IP is used in the rules, it is necessary to statically reserve IP addresses for the MAC addresses of computers for which the rules are specified in the firewall so that they receive the same IP over DHCP.

The following rule prohibits all other traffic that is not specified in the permitting rules for the specified IP, MAC address or subnet.
Chain: forward
Src. Address: or Src. MAC Address: same as permitting rule
Action: drop

In the list of firewall rules it is also necessary to make sure that allowing rules are in front of prohibiting ones.
Done.