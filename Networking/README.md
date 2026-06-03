# Networking Notes

## What is networking?
- A networking is simply the connection between devices so that they can communicate together and share sources.From your phone to your laptop they all are connected creating a network.

 ## LAN vs WAN
 - LAN stands for local area network.It is primarly used for devices in close proximity for e.g. in a school or a house.

 - WAN stands for wider area network.This is essentially LANs connected over a larger distance creating a WAN.The internet  is an example of the biggest WAN.
 - When you use the internet you go from:   Your LAN -> A WAN -> To someone elses LAN (This is where the server is)


## Key Components

 - Switch: It connects devices within a LAN by learning which devices is on what port and only sends data to that port.
 - Router: This connects your LAN to other networks.It essentiallys behaves as the exit door for traffic leaving the LAN.
  - Firewall: This is the security guard.Checks incoming as well as outgoing traffic and blocks anything that shouldnt pass(e.g the ec2 sg group acts as a firewall).

 ## IP adressing
 - An IP adress is an unique adress for a device on a network.It is like a house adress but for hte internet
 - There are two versions Ipv4 and IPv6
 - IPV4 is old and is limited it consists of four numbers "X.X.X.X." This means that there is 32 bits so there is a possibility of 4.3 billion adresses.
 - IPv6 is new and is much longer uses colons and has 128 bits.Making it unlimited in number.It is slowly being adapted but the original IPv4 remains dominant.
 ## Private and Public Ips

 - Private Ips are used inside of your LAN.Your Laptop has an IP of 192.168.1.10 and your phone 192.168.1.11 however these only work and are recognised inside the LAN.
