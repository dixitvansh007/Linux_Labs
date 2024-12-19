
# Linux Labs

### Lab Project - 4

#### Objective: Neetworking with Linux 

#### DURATION: 2 - 3 Hourse

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### Lab 1: Basic Network Configuration and Testing
#### Objective:
•	Understand how to configure and test basic network settings on a Linux system.
#### Tasks:
    1.	Check Network Interfaces:
     
     o	Use ip or ifconfig to list all available network interfaces on the system.

bash

Copy code

ip a

#or

ifconfig

    2.	Configure IP Address Manually:
     
     o	Use the ip command to assign a static IP address to an interface.

bash

Copy code

sudo ip addr add 192.168.1.100/24 dev eth0

sudo ip link set eth0 up

    3.	Verify the Configuration:
     
     o	Verify the IP address configuration using ip or ifconfig.

bash

Copy code

ip a

    4.	Test the Network Connectivity:
     
     o Use ping to test the network connectivity between the local machine and a remote host.

bash

Copy code

ping -c 4 8.8.8.8

    5.	Configure Default Gateway:
     
     o Use ip to add a default gateway for routing.

bash

Copy code

sudo ip route add default via 192.168.1.1

    6.	Verify Routing Table:
     
     o Check the routing table to ensure that the default gateway is correctly configured.

bash

Copy code

ip route

    7.	DNS Configuration:
     
     o Edit /etc/resolv.conf to configure DNS servers:

bash

Copy code

sudo nano /etc/resolv.conf

nameserver 8.8.8.8

nameserver 8.8.4.4

    8.	Test Name Resolution:

     o Test the DNS configuration by pinging a domain.

bash

Copy code

ping -c 4 google.com

#### Outcome:
You will have configured the network interface with a static IP address, default gateway, and DNS, and tested connectivity using ping.
________________________________________
#### Lab 2: Dynamic IP Address Configuration using DHCP

#### Objective:
•	Learn how to configure and test dynamic IP address assignment using DHCP.

#### Tasks:

    1.	Configure DHCP Client:
    
     o	Ensure that the system is set to obtain an IP address automatically from a DHCP server. Modify the network interface configuration file, usually located at /etc/network/interfaces (Debian/Ubuntu) or /etc/sysconfig/network-scripts/ifcfg-eth0 (CentOS/RHEL):

#Debian/Ubuntu:

bash

Copy code

sudo nano /etc/network/interfaces

auto eth0

iface eth0 inet dhcp

#CentOS/RHEL:

bash

Copy code

sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0

BOOTPROTO=dhcp

ONBOOT=yes

    2.	Restart Networking Service:
    
     o Restart the networking service to apply changes:

#Debian/Ubuntu:

bash

Copy code

sudo systemctl restart networking

#CentOS/RHEL:

bash

Copy code

sudo systemctl restart network

    3.	Verify DHCP Assignment:

     o Use ip a or ifconfig to check if the IP address has been assigned by the DHCP server.

    4.	Verify Network Connectivity:
     
     o	Use ping to test network connectivity and confirm that the DHCP-assigned IP works:

bash

Copy code

ping -c 4 google.com

#### Outcome:
You will configure a system to obtain an IP address dynamically via DHCP and verify the network connectivity.
________________________________________
#### Lab 3: Network Troubleshooting Tools

#### Objective:
•	Use networking tools to troubleshoot common network issues in Linux.

#### Tasks:
    1.  Ping Test:
     
     o Use the ping command to check the network connectivity to another system.

bash

Copy code

ping -c 4 192.168.1.1

    2.	Traceroute:
     
     o Use traceroute to track the route that packets take to reach a destination.

bash

Copy code

sudo apt install traceroute  # Ubuntu/Debian

sudo yum install traceroute  # CentOS/RHEL

traceroute google.com

    3.	Check DNS Resolution:
     
     o	Use dig or nslookup to check DNS resolution for a domain.

bash

Copy code

dig google.com

#or

nslookup google.com

    4.	Network Interface Status:
     
     o Use ethtool to check the status of the network interface (whether it's up, down, speed, etc.).

bash

Copy code

sudo apt install ethtool  # Ubuntu/Debian

sudo yum install ethtool  # CentOS/RHEL

sudo ethtool eth0

    5.	View Routing Table:
     
     o Use ip route or netstat -r to view the current routing table.

bash

Copy code

ip route

#or

netstat -r

    6.	Check Active Connections:
     
     o Use netstat or ss to view active network connections on the system.

bash

Copy code

netstat -tuln

#or

ss -tuln
    
    7.	Check Network Configuration with ifconfig or ip:
     
     o Verify network interface configuration using ifconfig or ip.

bash

Copy code

ifconfig

#or

ip a

#### Outcome:
You will have gained experience using various Linux network troubleshooting tools to diagnose and resolve network issues.
________________________________________
#### Lab 4: Configuring Advanced Network Settings (Static Routes, VLANs, etc.)

#### Objective:
•	Learn how to configure advanced network settings such as static routes and VLANs on a Linux system.

#### Tasks:

    1.	Add a Static Route:

     o Use ip to add a static route. For example, to route traffic destined for 192.168.2.0/24 via a gateway 192.168.1.1:

bash

Copy code

sudo ip route add 192.168.2.0/24 via 192.168.1.1

    2.	View Routing Table:

     o View the routing table to ensure the static route has been added:

bash

Copy code

ip route

    3.	Configure a VLAN Interface:
     
     o Create a VLAN interface using vconfig or ip commands. For example, to create VLAN 10 on interface eth0:

bash

Copy code

sudo ip link add link eth0 name eth0.10 type vlan id 
10

sudo ip addr add 192.168.10.1/24 dev eth0.10

sudo ip link set eth0.10 up

    4.	Verify VLAN Configuration:
     
     o Verify the VLAN interface is up and has the correct IP address:

bash

Copy code

ip a show eth0.10

    5.	Enable IP Forwarding (for Routing Between Networks):

     o	Enable IP forwarding to allow routing between different subnets:

bash

Copy code

sudo sysctl -w net.ipv4.ip_forward=1

    6.	Configure NAT for Internet Sharing:
     
     o Configure Network Address Translation (NAT) using iptables to share the internet connection with a local network:

bash

Copy code

sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

sudo sysctl -w net.ipv4.ip_forward=1

#### Outcome:
You will have learned how to configure static routes, VLANs, and network address translation (NAT) on Linux.
________________________________________
#### Lab 5: Securing Linux Network Services

#### Objective:
•	Learn how to secure network services on a Linux system by configuring firewalls and using SSH for secure communication.

#### Tasks:
    1.	Configure UFW (Uncomplicated Firewall) on Ubuntu/Debian:

     o Install and configure UFW to allow only certain services (e.g., SSH, HTTP):

bash

Copy code

sudo apt install ufw

sudo ufw allow ssh

sudo ufw allow http

sudo ufw enable

sudo ufw status
    2.	Configure FirewallD on CentOS/RHEL:
     
     o Install and configure firewalld to allow only certain services:

bash

Copy code

sudo systemctl start firewalld

sudo firewall-cmd --permanent --zone=public 
--add-service=ssh

sudo firewall-cmd --permanent --zone=public --add-service=http

sudo firewall-cmd --reload

sudo firewall-cmd --list-all

    3.	Secure SSH Access:

     o Disable root login and change the SSH port by editing /etc/ssh/sshd_config:

bash

Copy code

PermitRootLogin no

Port 2222

     o	Restart the SSH service:

bash

Copy code

sudo systemctl restart sshd
    
    4.	Verify Firewall Configuration:

     o Use ufw status or firewall-cmd --list-all to verify that only the required services are accessible.

#### Outcome:
You will have configured firewalls to secure network services and restricted SSH access for enhanced security.
________________________________________
#### Conclusion:
These Linux Networking Labs provide you with the foundational knowledge needed to configure and troubleshoot networking on a Linux system. You will learn how to set up basic and advanced networking configurations, diagnose connectivity issues, and secure Linux network services through firewalls and SSH. By completing these labs, you'll gain hands-on experience that will help you manage and secure Linux-based networks.
