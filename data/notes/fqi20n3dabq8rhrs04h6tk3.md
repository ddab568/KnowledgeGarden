
Notes on Technical Fundamentals course (https://learn.cantrill.io/p/tech-fundamentals) - summary of technical concepts considered a precursor to aws certification / general tech architecture.

## OSI Model

The Open Systems Interconnection (OSI) model is a conceptual framework that describes the communication functions of a telecommunications or computer system. It is divided into seven layers each of which performs a specific function in the transmission of data between networked devices. This is sometimes known as the Networking Stack.

The 7 layers are split into Host and Media Layers:

**Host Layers:**

    7- Application

    6- Presentation

    5- Session

    4- Transport

**Media Layers:**

    3- Network

    2- Data Link

    1- Physical

### Physical Layer (Layer 1)

- The first and lowest layer in the OSI model
- Responsible for the physical transmission of data over a communication channel such as wire, cable or wireless signal
- All devices on the layer 1 network need to use the same medium for transmitting and receiving
- This layer defines the specifications things like voltage levels, timings, data rates, distances, modulation and connectors
- At layer 1, everything is broadcast in the medium, addresses are not used - this is addressed by layer 2
- Collisions can happen as multiple things can broadcast at the same time. Layer 1 has no collision detection
- For layer 1 to be useful, we need to add layer 2 which runs over the top of it

### Data Link Layer (Layer 2)

- Layer 2/Data Link layer is the second layer in the OSI model responsible for the reliable transfer of data between two nodes on the same network segment
- Runs over layer 1 and requires a functional layer 1 to operate
- MAC address is uniquely assigned to a piece of hardware
- Layer 2 provides frames and layer 1 handles the physical transmission and reception on the medium
- Layer 2 frames have different components:

The mac header:

- **preamble** - the start of the frame - destination and source mac address - destination can be a broadcast or specific
- Ether type specifies which layer 3 protocol is putting its data inside a frame e.g IP
- Then the payload:

**The payload**- the data the frame carries from source to destination provided by layer 3

**The frame check sequence** - allows the destination to check if corruption has occurred or not

- There are several devices that can be used to send data. A hub is a 'dumb' device that sits in layer 1 where as a switch sits in layer 2 and deals with addresses and collisions.

### Network Layer (Layer 3)

Layer 3 handles the process of moving data from a source to a destination.

Any networks using only layer 2 need to use the same protocol e.g. ethernet. Because some networks don't use the same protocols, layer 3 is needed.

Layer 3 can span multiple different layer 2 networks. It adds internet protocol (IP) to assign to devices to be used across different networks. Devices called routers which are layer 3 devices move packets of data across different networks.

There are two versions of IP: version 4 and 6. IP has a packet structure containing a source and destination IP field. There is a protocol field which contains a layer 4 protocol e.g. ICMP, TCP or UDP. There is also a field called TTL or time to live. This defines a maximum number of hops before a packet can be discarded so it doesn't loop forever.

The IP4 address is made up of 4 parts separated by dots with each value up to 255 e.g. 1.2.4.255. IP addresses are only dotted for human format, the actual IP address is in binary format made up of 4 x 8 bits. Each 8 bits is known as an octet. IP addresses should be unique, especially in your local network.

Devices inside a local network communicate to the router. A router has a route table where each row has a destination field and a next hop/target field. Each packet that arrives at the router will have a destination.

### Transport Layer (Layer 4)

Layer 4, the transport layer, is responsible for ensuring that data is delivered reliably from one device to another. Layer 3 does not ensure the ordering of packet arrival nor does it deal with packet loss e.g when TTL is reached. Layer 3 also does not differentiate between the packets therefore packets from different applications are treated the same.

Layer 4 remedies these issues. Layer 4 adds UDP and TCP. These run on top of IP. You would pick TCP when you want reliability and error correction. UDP is faster because it doesn't require the overhead of reliability.

### Session Layer (Layer 5)

TODO

---

### Network Address Translation (NAT)

NAT is technology that allows multiple devices to share a single public IP address. They translate private IP addresses to public ones and also in reverse.

There are different types of NATs:

- Static NAT which is a single 1 to 1 map of a private to fixed address
- Dynamic NAT uses 1 private address against the 1st available public address from a pool of addresses. This is used when you have a large number of private addresses.
- Port Address Translation - Many private addresses to 1 public address

NAT only makes sense for IPv4 because IPv6 adds many more addresses.

### IP Address Space and Subnetting

IPv4 addresses occupy a range from 0.0.0.0 -> 255.255.255.255.255
Although it covers over 4.29 billion addresses, with the current world population it will not suffice. Public IP addresses need to be allocated but private ones can be used freely.

The IPV4 public address space is split into ranges where specific subsets are assigned to specific entities:

- Class A - 0.0.0.0 -> 127.255.255.255 - historically this space was For huge businesses but since it's been given up to the regional managers of the IP address space
- Class B - 128.0.0.0 -> 191.255.255.255 - larger businesses that didn't need class A but as above, they are now addressed to IP managers
- Class C - for those that were not big enough to fit into A or B but as with above, they're now owned by IP managers
- Class D
- Class E

With IPv6, the address space is 340 trillion spaces. IP addresses in IPv6 are no longer a scarce resource and don't need strict management.

Subnetting is the process of breaking up IP address space into smaller pieces. CIDR allows us to break up the IP addresses with a prefix e.g. /16

### Distributed Denial of Service (DDoS) attacks

An attack that is designed to overload websites.

There are different types of DDoS attacks:

- Application layer - flooding HTTP
- Protocol based attacks - SYN floods
- Volumetric - DNS amplification

### VLANS, TRUNKS and QinQ

- A Virtual Area Network (VLAN) is a way to divide a single physical network into multiple logical networks.

// TODO

### SSL and TLS

Secure Sockets Layer (SSL) and Transport Layer Security (TLS) at a high level do the same thing. TLS is newer and more secure.

SSL and TLS provide privacy and data integrity between client and server.

TLS:

- ensures privacy via encryption
- identity (server/client) verification
- ensures a reliable connection by protecting against alteration of data in transit
