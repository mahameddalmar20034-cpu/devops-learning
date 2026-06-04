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
 - Your Public Ip is the actual adress on the internet .It is the adress of the router and is what the outside world sees.All the devices at home  have different private IPs but share one public IP through the router using a NAT.

## MAC Adresses
- Every device has a mac adress embroided into it at the factory behaving as the unique hardware identifier.
- The IP is simply where you are on the network  this can change when connecting to different networks.The MAC adress is something permanently instilled within the device.

## Ports and Protocols

- The protocol of SSH which remote terminal access occurs at port 22.SSH stands for secure shell.It is the rules for securely accessing a remote machines terminal.SSH lsitens at port 22 when your connect and authemticate with a key it gives you remote access with a command list .Everything is encrypted including your commands as you sshed into the server.

- THe protocol of HTTP which stands for Hyper Text Transfer Protocol occurs at port 80.This is protocol is the rules for how web pages are requested and delivered.The browser sends a HTTP request to that server on port 80 saying "Give me this page".The server has either a web server like NGINX listening on that port 80 waiting for a response. It sends back a HTTP response with the HTML , images, etc. However this is all in plain text none of this is encrypted so who ever is watching the traffic can read it.

-The protocol of HTTPS is pretty much the exact same hting as HTTP but it occurs on port 443 and is encrypted.When the browswer data reaches the port they do a handshake to set up encryption (using SSL/TLS certificates).

-The protocol of DNS which stands for Domain Name Server occurs at port 53.When the  browswer needs to look up an IP for a domain it sends a query to the DNS server on port 53.The server looks up the A record and sends back the IP adress.

 - Essentially every port has a specicific service waiting behind it.

## TCP and UDP

- These are two different protocols and each of them have their specific use
 
- TCP stands for transimission control protocol these rules allow for reliable delivery.This is done by setting a connection first making sure every packet arrives, resending anything that gets lost and keeps things in order.It is slower yet reliable and is used in by HTTP,HTTPS and SSH.

- UDP stands for user datagram protocol.It prioritises fast delivery.No connection set up nor checking of packets arriving and no resending.It just fires data and moves on.Fast yet unreliable,it used in streaming, gaming and DNS queries.


## OSI Model

-This is a framework that breaks down how the internet works in 7 layers.Each layer entails a specific focus.


### Layer 1 : Physical
- This is the actual hardware.This consists of the cables ,wifi and electrical signals.If the ethernet is unplugged the layer is broken.

### Layer 2: Data link
- This the layer that handles communication within a local network.This is where the MAC adresses lives.Switches also operate here.Data is packaged into frames.It gets the right device on the LAN.

### Layer 3: Network
- Handles communication across networks.This is where IP adresses live aswell routers. Data is packaged into packets.It figures out the path from your device to a server on the other side.

### Layer 4: Transport

-Handles reliable (TCP) or fast (UDP) delivery.Ports live here.It is broken into segments and manages flow and control and makes sure things arrive properly. (FOR TCP)

### Layer 5: Session

- Manages the connections between applications.Opens maintains and closes sessions.Keeps conversations seperate.

### Layer 6: Presentiation
- This part handles data formatting and encryption.It translates the data into a format the application can understand.This is where SSL/TLS encryption occurs.

### Layer 7: Application
- These are the things that you interact with. HTTP,SSH,DNS and email.This is the actual apps and protocls you use.

## TCP/IP model

-This OSI model is more of a theoretical teaching framework solely to solidify understanding.
- The TCP/IP model is a simpler more practical model consisting of 4 layers.
### Layer 1 - Network (access) or link

-


 


