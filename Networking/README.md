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

- This layer combines OSI layer 1 and layer 2.This is physical hardware aswell as local delivery (cables,switches MAC adresses wifi).This gets the data across the local network.

### Layer 2 - Internet

- This consists of the IP adresses and the routers.It gets the data across networks handling routing from source to destination.

### Layer 3 - Transport
- This consists of TCP and UDP as well as the ports.It handles reliable or fast delivery.

### Layer 4 - Application
- This combines OSI layers 5,6 and 7.As well as all the protocols you interact with. HTTP, SSH, DNS and email ie the actual applications.


## DNS
- DNS stands for domain name system its a system that translates human readable names into IP adress. It is much easier for the human brain to remember.
- DNS exists not in a signle system but rather a distrubuted sytem.This consists of thousands of servers across the globe working together.
- If you were to search a domain the browser would need an IP adress to connect and thus the DNS behaves as the internet's phonebook.

## How does DNS work
1. When the browser searches a domain it checks locally to see if it is inside of it's own cache.If not there it asks the operating system as the OS has its own cache.If not found it then moves on.
2. It now asks the resolver.This device sends a query to a DNS resolver.This is ran by your ISP or a public one.
3. If the resolver doesnt know the IP it begins at the top going to the root server.The root server doesnt actualy know but it does what handles the TLD (top level domain) so for google.com it wouldnt know the ip but it does know to send the resolver to the designated .com TLD server.
4. The resolver asks the TLD server.That TLD server then points to the google authorative server.
5. The resolver now requests the authorative server this is googles actual own dns server.The server hands over the A-record.The Resolver now has the IP it caches it for next time and sends it back to your device.Your browser then connects to your IP.
- This is all done in milliseconds.

## A-records
Here are different types of A records:
A-record: This is the standard and most common it maps a domain to an Ipv4 adress
AAAA record: This is similar to an A record but is for IPV6 adresses.It has 4 A's due to IPv6 being four times larger than IPv4
CNANME record: THis is an alias it points one domain to another domain
MX record:Also known as Mail exchange. it tells the email servers where to deliver mail for that domain.
TXT record: THis is just used for verification and other info.COmpanies use it prove domain ownership when you connecct.
NS record:Also known as Name server.It informs you about which domain server is authorative for that domain.


## Routing: 
-THis is essentially how data finds its way across networks.
-It doesnt go in a straight line rather it hops multiple routers with each deciding where to send it next.
- Each router contains a routing table that entails directions for the router depending on the network and sends out a certain port.
- This is completed by thr router looking at the destination IP and checking the router table forwading it onto the next hop.

  ## Static routing vs Dynamic Routing
  ### Static routing
  - This is manually configured by a human.
  - It is instructed by to reach a certain network (and IP) and send traffic out of the desired port.
  - This allows for simplicity and predictable networking.
  - However it is unable to adapt if a link goes down or traffic fails
  - It must be updated manually
  - It is mainly used in small networks or fixed specific paths
 
    ## Dynamic routing
    -This is the routes communicating with each other to fingure out the most optimal path
    -If a link goes down it is able to recalculate to find an alternative path
    -It is self healing and reliable
    -Used in larger networks like the internet

    ### Routing protocols
    Dynamic routing displated that routers communicate with each other sharing information about which networks they are able to reach and how good that path is.Routing protocols are the rules for how they operate this.
    ###OSPF
    -Stands for Open Shortest Path First
    -Used in organisations networks
    -Each router builds a complete map of the network and calculates the shortest path to each destination
    -Able to adaps due to errors
    -They also take into account costs (based on link speed)
    -This means a fast connection has a lower cost thatn a slow connection
    -Used by companies,universities and large internal networks
    ###BGP
  - Stands for Border Gateway Protocol
  - Used between organisations
  - This is what runs the internet
  - Google,Your isp and amazon all have networks this is how they communicate between each other
  - This is how speperate networks tell each other that it can reach that certain IP adress
  - Does not take into account the shortest path but rather prioritises policies
  - The policies are based on trust and business relationship.
  - Internet outtages can occur due to BGP misconfiguration.In where organisations adverrtised the incorrect routes and broken paths effecting millions across the internet
 
    ### Subnetting 
    Subnets are useful for these reasons:
    -Security:It enables you to keep departments seperate
    -Performance:Less broadcast traffic clogging things up
    -Organisation:It is easier to manage small chunks
    Subnetting allows you to carve one big network into smaller pieces

    ###CIDR
    An example of a CIDR notation is 192.168.1.0/24
    -The /24 tells you how many bits are in the network portion
    -The total is 32 bits for an IPv4 adress.
    -This means that there are 24 bits for network and 8 bits for hosts
    -This means there are 254 usable adress not 256 this is because there are two reserved adresses
    -One adress to identifiy the network and the other acts as the broadcast adress used to send info to all devices on that network.

    ###NAT
    -This stands for network adress translation
    -It is what translates the private ips of your decices to your routes singular public IP

    ###Types of NAT
    1.Static nat: This means that one private ip always maps to one public IP.This means each time a device sends traffic it uses the same public IP.
    2.Dynamic NAT: This uses a pool of public Ips.When a device needs to go live it gets assigned an IP from the pool.when it is no longer need it is sent back to the pool.
    3.PAT (Port Adress translation):This what your home router uses.It uses the ports where two devices send a request from different Ips.The router translates both of the same public Ips but keeps track of the source of the ports.
    This means when the responses come back the router checks the port and sends it to the right device.

    ##Troubleshooting tools
    These are the diagnost commands used when something isnt working on a network:
    Ping: Texts if you can reach a destination.It sensd a small packet and waits for the reply. ``` ping google .com ```
          If it times out then something is blocking the path, either the server down, the internet is broken or the firewall is blocking it.A slow response time hints at a slow connection.

    Traceroute: This shows the path the traffic takes. ``` traceroute google.com``` it shows a list of routers your packet passes through.If one hop times out or show latency thats where the problem is.

    nslookup:This tests the DNS.It reqests the IP for that specific domain. ```nslookup google.com```.If no IP is returned it might be that the DNS server may be down or misconfigured.

    dig: This is the same as nslookup but is much more detailed.It shows the DNS response including record types, TTL and which server has answered.```dig google.com```.This is mainly used to see exactly what DNS is returning.
 
    
    
    
    
 
    

    

 


