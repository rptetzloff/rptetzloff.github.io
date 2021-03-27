---
layout: post
title: Networking Basics
tags: [cwna, wi-fi, networking, OSI Model]
---

## OSI Model

While this study guide is focused on wireless communications, especially Wi-Fi, an understanding of networking fundamentals is essential to understanding Wi-Fi. This is often taught using the [OSI Model](https://en.wikipedia.org/wiki/OSI_model), which is a model for describing how networking occurs. Understanding how this communications occurs at the different layers, is essential for understanding networking.

| Layer | Name |
|---|:---|
| 7 | Application |
| 6 | Presentation |
| 5 | Session |
| 4 | Transport |
| 3 | Network |
| 2 | Data Link |
| 1 | Physical |

Let's look at each of these levels a little more:

1. Layer 1 - Physical

    This layer describes the physical medium at which communication occurs. A data unit at this layer is basically just a *bit*.
    
    Some of the characteristics this layer describes include:
    
    - The actual medium (i.e. Cat5 cabling, fiber optic, wireless) and their termination means (i.e. RJ-45's TIA/EIA-568-A/B termination standards)
    - The way bits are transmitted on the medium (i.e. voltage fluctuations, light flashes, radio signal modulation)
    - Physical network topologies (i.e. bus, star, ring, mesh)
    - Bandwidth usage: Not in the consumption sense, but rather in the method in which the medium is utilized. This is typically defined as either baseband (single-use medium) or broadband (multiple-use medium). This gets blurred a little bit when a service provider uses a single medium for multiple data streams (digital phone service, Internet, and IPTV), but fundamentally, the medium is used for data in this case.
        - Baseband: The entire bandwidth/frequency of the medium is consumed for data consumption.
        - Broadband: The bandwidth/frequency is devided amongst different communications means. DSL uses the frequencies for phone service and data. Cable technologies use the frequencies for cable television and data services. 
    - The strategy which is used for multiplexing the different communications methods over the medium:
        - Time-Division multiplexing (TDM): Each stream of communication is assigned a time slot in which they are allowed to transmit.
        - Frequency-Division multiplexing (FDM): Each stream of communication is assigned a different frequency on which they are allowed to transmit. This can divide a copper cable into multiple sub-channels that, such as those used in T1 technology.
        - Wavelength-Division multiplexing (WDM): Basically the same thing as FDM, but over a fiber optic medium. WDM allows for different wavelengths of light to be used for different communcations streams over a given fiber optic cable. 
    
    The devices used at this layer include hubs and wireless access points. Bluetooth, Ethernet, USB, and other specifications are described at this layer.
        
1. Layer 2 - Data Link

    This layers describes the method in which data is packaged onto the medium and the way at which devices talk over the same network. Data units described at this layer are referred to as *frames*. The layer can be further broken down into two different sub-layers:

    1. Media Access Control (MAC) Sub-Layer
        This sub-layer describes the following characteristics:
        - Physical addressing (i.e. MAC Address, a 48-bit address assigned to a network interface card (NIC))
        - Logical topology, such as bus or ring
        - Transmission of data on the medium, i.e. controlling who can talk at what time
        
    1. Logical Link Control (LLC) Sub-Layer
        This sub-layer describes the following characteritsics:
        - Flow control, a limit of how much data a sender can transmit at one time
        - Error control, utilizing a checksum to ensure that data is received intact
        - Synchronized transmission of frames
        
    A number of different devices are defined at the data link layer, including network interface card, switches, and bridges. Parts of Ethernet, Wi-Fi, Zig-Bee, PPP and many other protocols operate at the data link layer.
    
1. Layer 3 - Network 

    The third layer, describes the manner in which devices talk over different networks. Data units at this level are called packets. Some tasks described at layer 3 include:
    
    - Logical addressing: IP addresses (both IPv4 and IPv6), as well as less commonly used schemes like AppleTalk
    - Packet forwarding or routing: Using a packet's Layer 3 header information to send packets from one host to another.
    - Route discovery: Using layer 3 information to forward packets between networks, using either static information or dynamic routing protocols such as OSPF.
    - Congestion control: Prevents a sender from flooding a receiver with data
    - Packet reordering: reorder packets in the appropriate sequence in the event that they arrive out of order.
    
    Typical layer 3 devices include routers and layer 3 switches. Aside from IPv4 and IPv6, layer 3 includes routing protocols like OSPF and multicast group management protocols like IGMP. It also includes control message protocols like ICMP.
    
1. Layer 4 - Transport

    In the transport layer, messages are encapsulated into *segments* for transmission from the upper layers to the lower layers. Network traffic is decapsulated into a data stream for upper layers.
    
    Layer 4 offers the following protocols:
    
    - Transmission Control Protocol (TCP): 
        - Connection-oriented
        - Reliable transport, i.e. segments are acknowledged and, if dropped, can be retransmitted
        - Windowing: one or more segments can be sent at a time, and all segments in a window can be acknowledged at one time. Window sizes can vary
    - User Datagram Protocol (UDP):
        - Connectionless
        - Unreliable transport, i.e. dropped segments are just lost

1. Layer 5 - Session

    The session layer describes the process of setting up, maintaining, and closing sessions. Services included in these processes include authentication and authorization, and the transferring of data into and out of the transport layer.

1. Layer 6 - Presentation

    The presentation layer describes the process of formatting and delivering messages between application and networking layers. It performs the functions of formatting data in a compatible format and encrypting data. 

1. Layer 7 - Application

    The application layer interacts directly with end-user facing software to complete the data transfer from network to software. Examples include email protocols (SMTP, POP, IMAP), web protocols (HTTP), file transfer protocols (TFTP, FTP), Shell Protocols (Telnet, SSH), and DNS.

Wi-Fi, like wired communications, are focused more on the lower levels of the OSI model, in particular, definining only communication at Layers 1 and 2.

It's also important to note that this is more of a conceptual model of how networking should work. Its goal is to promote interoperability. In practice, the actual flow of data is going to be a bit different than this. There are other models that relate closely to this model (such as the [TCP/IP model](https://en.wikipedia.org/wiki/Internet_protocol_suite)), but most textbooks will teach this as the main reference model. 

## Architecture

There are several different concepts that come to mind when referring to network architectures, many of which help to define different functions of network devices and how they communicate with each other.

### Design Patterns

One typical network design pattern is comprised of three different heirachical components:

- Core

    The core layer forwards traffic between different distribution areas.

- Distribution

    The distribution layer is where most routing between different areas of the access network occurs. In other words, it routes traffic between different VLANs and subnets.

- Access

    The access layer delivers traffic to end users and receives traffic from the end user. This layer assigns QoS and also should have ACLs and other policies for blocking traffic.

There are  other architectural designs patterns that can be used, but for simplicity's sake, we'll focus on this one. From a wireless perspective, most wireless networks are going to exist at the access layer, delivering traffic to end users. Point-to-point links, however, could also exist at distribution (or even core, I suppose) layers. 

### Planes

Modern network also consist of three different planes that perform different functions on the data being transferred.

- Management Plane

    The management plane is used for monitoring and administering the network. Examples of management plan services include SNMP
    
- Control Plane

    The control plane is what indicates how data should move throughout a network. Examples of services in the control plane include DNS and routing protocols.

- Data Plane

    The data plane forwards the actual data traffic throughout the network. This mostly occurs at layer 2 using a MAC forwarding table to know where to send the data.

### Topologies

## Addressing

## Duplexing

## References

- [OSI Model](https://en.wikipedia.org/wiki/OSI_model)
- [CompTIA Network+ N10-006 Cert Guide](https://www.amazon.com/CompTIA-Network-N10-006-Cert-Guide/dp/0789754088/)
- [TCP/IP Illustrated, Volume 1, 2nd Edition](https://www.amazon.com/TCP-Illustrated-Protocols-Addison-Wesley-Professional/dp/0321336313/)
- [CWNA Study Guide CWNA-107](https://www.amazon.com/Certified-Wireless-Network-Administrator-Study/dp/1119425786/)
- [The Art of Network Architecture](https://www.amazon.com/Art-Network-Architecture-Business-Driven-Networking-ebook/dp/B00JF5CP5O/)
- [Management, Control and Data Planes in Network Devices and Systems](https://blog.ipspace.net/2013/08/management-control-and-data-planes-in.html)
