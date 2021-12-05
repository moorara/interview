# Computer Networks

## Protocol Layers

  - A **protocol** is an agreement between the communicating parties on how communication is to proceed.
  - Most networks are organized as a stack of **layers**, each one built upon the one below it. Between each pair of adjacent layers is an interface.
  - Each layer passes data and control information to the layer immediately below it, until the lowest layer is reached.
  - Each instance of a protocol talks virtually to its peer using the protocol (horizontal).
  - Each instance of a protocol uses only the services of the lower layer (vertical).
  - Lower layer wraps higher layer content, adding its own information to make a new datagram for delivery.
  - Each layer adds its own header. Trailers, compression, encryption, and segmentation and reassembly may also be involved.
  - Layering provide abstraction and modularity, but it also adds overhead and hides information and details.


## OSI Reference Model

  - **Application Layer**
    - Unit of data: Messages
    - Protocols: DNS, HTTP, FTP, SSH, IMAP, ...
    - Services: High-Level APIs, Resource Sharing, Directory Services, ...
  - **Presentation Layer**
    - Unit of data: Messages
    - Protocols: NDR, XDR, TLS/SSL (operation), ...
    - Services: Data Conversion, Character Encoding, Data Compression, Data Encryption/Decryption, ...
  - **Session Layer**
    - Unit of data: Messages
    - Protocols: PAP, RPC, RTP, TLS/SSL (initialization), ...
    - Services: Session Management, Authentication, Authorization, ...
  - **Transport Layer**
    - Unit of data: Segments
    - Protocols: TCP, UDP, DCCP, ...
    - Services: Reliable transmission between nodes on a network, Same-Order Delivery, Connection-Oriented Communication, Multiplexing, ...
  - **Network Layer**
    - Unit of data: Packets
    - Protocols: BGP, IPv4/IPv6, IPsec, ICMP, IGMP
    - Services: Connectionless Communication, Addressing, Routing, Forwarding, Traffic Control, ...
  - **Data Link Layer**
    - Unit of data: Frames
    - Protocols: ARP, MAC, PPP, ...
    - Services: Reliable transmission between two adjacent nodes connected by a physical layer, Logical Link Control, Media Access Control, ...
  - **Physical Layer**
    - Unit of data: Bits
    - Protocols: Ethernet, DSL, Bluetooth, USB, ...
    - Services: Transmission of bit streams over a physical medium, Circuit Switching, Modulation, Multiplexing, ...


## Internet Reference Model

  - **Application Layer**
    - OSI Layers: Application + Presentation + Session
    - Protocols: DNS, HTTP, FTP, SSH, TLS/SSL, ...
  - **Transport Layer**
    - OSI Layer: Transport
    - Protocols: TCP, UDP, DCCP, ...
  - **Internet/Network Layer**
    - OSI Layer: Network
    - Protocols: BGP, IPv4/IPv6, IPsec, ICMP, IGMP, ...
  - **Link Layer**
    - OSI Layer: Data Link + Physical
    - Protocols: ARP, PPP, NDP, MAC, ...


## Protocols

  - **ARP**
    - Layer: Link
    - The Address Resolution Protocol is used for converting of network layer addresses (IPv4) into link layer addresses (MAC).
  - **NDP**
    - Layer: Link
    - The Neighbor Discovery Protocol is used with Internet Protocol Version 6 (IPv6).
      - Discovery of other nodes on the link
      - Determining the link layer addresses of other nodes
      - Finding available routers and DNS servers
  - **BGP**
    - Layer: Internet/Network
    - The Border Gateway Protocol (BGP) is designed to exchange routing and reachability information among autonomous systems (AS) on the Internet.
      - The Internet is a network of networks. It is broken up into hundreds of thousands of smaller networks known as autonomous systems (ASes).
    - BGP is responsible for looking at all of the available paths that data could travel and picking the best route (hopping between autonomous systems).
    - External BGP (eBGP)
      - Routes are exchanged and traffic is transmitted over the Internet using external BGP (eBGP).
    - Internal BGP (iBGP)
      - Autonomous systems can also use an internal version of BGP to route through their internal networks (iBGP).
      - Using internal BGP is NOT a requirement for using external BGP.
      - Autonomous systems can choose from a number of internal protocols to connect the routers on their internal network.
  - **ICMP, ICMPv6**
    - Layer: Internet/Network
    - The Internet Control Message Protocol (ICMP) is used by network devices to send error messages or query messages.
      - Echo Request
      - Echo Reply
      - Source Quench
      - Time Exceeded
  - **IPv4, IPv6**
    - Layer: Internet/Network
    - The Internet Protocol defines packet structures and addressing methods that are used to label the datagram with source and destination.
    - IP is responsible for delivering packets from the source host to the destination host solely based on the IP addresses in the packet headers.
  - **IPsec**
    - Layer: Internet/Network
    - Internet Protocol security uses cryptographic security services to protect communications over Internet Protocol networks.
      - Data origin authentication
      - Data integrity
      - Data confidentiality (encryption)
    - IPsec can be configured to operate either in Transport mode or in Tunnel mode.
  - **TCP**
    - Layer: Transport
    - TCP provides reliable, ordered, and error-checked delivery of datagrams between hosts/applications communicating over an IP network.
    - TCP is a reliable stream delivery service which guarantees all bytes received will be identical with bytes sent and in the correct order.
    - A technique known as positive acknowledgment with retransmission is used to guarantee reliability of packet transfers.
    - The sender maintains a timer for the packet, and retransmits a packet if the timer expires before the packet has been acknowledged.
    - TCP is optimized for accurate delivery rather than timely delivery, and therefore, TCP sometimes incurs relatively long delays.
  - **UDP**
    - Layer: Transport
    - UDP uses a simple connectionless transmission and exposes the host/application to any unreliability of the underlying network protocol.
    - UDP has no guarantee of delivery, ordering, or duplicate protection.
    - UDP is for purposes where error checking and correction is either not necessary or is performed in the application.
    - Real-time and time-sensitive applications often use UDP because dropping packets is preferable to waiting for delayed packets.
    - UDP provides checksums for data integrity, and port numbers for addressing different functions at the source and destination.
  - **DHCP**
    - Layer: Application
    - DHCP is a protocol used on IP networks for dynamically distributing network configuration parameters, such as IP addresses.
      - DHCPDISCOVER: the client broadcasts messages on the network subnet. A DHCP client may also request its last-known IP address.
      - DHCPOFFER: the server reserves an IP address for the client, makes a lease offer, and broadcast it.
      - DHCPREQUEST: the client broadcasts a message requesting the offered address.
      - DHCPACK: the server sends an acknowledgement to the client including the lease duration and any other configuration information.
  - **DNS**
    - Layer: Application
    - The Domain Name System is a hierarchical distributed naming system for hosts, services, or any resource connected to the Internet.
    - DNS translates domain names, which can be easily memorized by humans, to the numerical IP addresses.
  - **TLS/SSL**
    - Layer: Application
    - The TLS protocol provide authentication, integrity and confidentiality (encryption) for client-server applications.
    - Other protocols can operate either with or without TLS/SSL.
    - Client and server negotiate a stateful connection by a handshaking procedure to agree on parameters used during the secure session.


## Network Addressing

### Classful Network

| **Class** | **Leading Bits** | **Network Bits** | **Per Network Bits** | **Address Range** | **No. of Networks** | **Address per Network** |
|-----------|------------------|------------------|----------------------|-------------------|---------------------|-------------------------|
| A             | `0`    | `8`   | `24`  | `0.0.0.0`   - `127.255.255.255` | 2<sup>7</sup>  | 2<sup>24</sup> |
| B             | `10`   | `16`  | `16`  | `128.0.0.0` - `191.255.255.255` | 2<sup>14</sup> | 2<sup>16</sup> |
| C             | `110`  | `24`  | `8`   | `192.0.0.0` - `223.255.255.255` | 2<sup>21</sup> | 2<sup>8</sup>  |
| D (Multicast) | `1110` | _N/A_ | _N/A_ | `224.0.0.0` - `239.255.255.255` | _N/A_          | _N/A_          |
| E (Reserved)  | `1111` | _N/A_ | _N/A_ | `240.0.0.0` - `255.255.255.255` | _N/A_          | _N/A_          |


### Classless Inter-Domain Routing (CIDR)

  - CIDR is a method for allocating IP addresses and IP routing.
  - It is introduced to replace the classful network addressing architecture.
  - CIDR notation is a concise representation of an IP address and its associated routing prefix (mask bits).


### Private Networks

  - A private network is a network that uses a private IP address space.
  - Private IP addresses are commonly used for home, office, and enterprise local area networks.
  - IPv4 Private Address Spaces:
    - 24-bit block:
      - single class A network
      - CIDR: `10.0.0.0/8`
      - Address range: `10.0.0.0` - `10.255.255.255`
    - 20-bit block:
      - 16 class B networks
      - CIDR: `172.16.0.0/12`
      - Address range: `172.16.0.0` - `172.31.255.255`
    - 16-bit block:
      - 256 class C networks
      - CIDR: `192.168.0.0/16`
      - Address range: `192.168.0.0` - `192.168.255.255`


## Network Address Translation

  - NAT is a methodology for mapping one IP address space into another.
  - NAT modifies network address information in Internet Protocol (IP) packet headers while they are in transit across a traffic routing device.
  - There are three different types of NAT implementation:
    - **Static NAT**
      - Static NAT is one-to-one mapping of a private IP address to a public IP address.
      - Static NAT is useful when a network device inside a private network needs to be accessible from internet.
    - **Dynamic NAT**
      - Dynamic NAT establishes a one-to-one mapping between a private IP address to a public IP address.
      - Dynamic NAT is mapping of a private IP address to a public IP address from a group of public IP addresses called as NAT pool.
      - The public to private mapping may vary based on the available public IP address in NAT pool.
    - **PAT/Overloading**
      - Port Address Translation is another type of dynamic NAT which can map multiple private IP addresses to a single public IP address.
      - When a client from inside network communicate to a host in the internet, the router changes the source port number with another.
      - When the router receives from internet, it will refer the port mappings table and forward the data packet to the original sender.
  - Port forwarding is an application of network address translation (NAT).
  - It redirects a communication request from one IP address and port number to another while the packets are traversing a network gateway.
  - It is used to make services on a host residing on a protected or internal network available to hosts on the other side of gateway (external network).
  - Port forwarding can be divided into the following types:
    - Local port forwarding
    - Remote port forwarding
    - Dynamic port forwarding


## Network Topologies

  - Bus Network
  - Star Network
  - Ring Network
  - Mesh Network
  - Tree Network
  - Hybrid Network


## Network Devices

  - **Repeater**
    - A device which amplifies or regenerates digital signals received while sending them from one part of a network into another.
    - A repeater works at the physical layer (layer 1) of the OSI model.
  - **Bridge**
    - A bridge connects multiple network segments.
    - In the OSI model, bridging is performed in the first two layers, below the network layer.
  - **Hub**
    - A hub connects multiple Ethernet segments, making them act as a single segment.
    - A hub works at the physical layer (layer 1) of the OSI model.
    - A hub re-broadcasts any data entering any port to all other ports.
  - **Switch**
    - A switch connects devices together on a network, by using packet switching to receive, process and forward data to the destination device.
    - A switch works at the link layer (layer 2) of the OSI model.
    - A switch splits the network traffic and sends it to different destinations using hardware addresses rather than to all systems on the network.
  - **Router**
    - A router forwards data packets between computer networks. Routers perform the "traffic directing" functions on the Internet.
    - A router works at the network layer (layer 3) pf the OSI model.
    - The routers exchange information about destination addresses using a dynamic routing protocol.
