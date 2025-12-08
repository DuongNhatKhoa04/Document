# Introduction to Networking

Computer networks allow computers and other devices to share data, services, and resources.  
This first chapter gives you a high-level view of how modern networks are structured, which
devices make them work, and what happens to the bits as they travel across the wire.

---

## Learning Objectives

After studying this chapter, you should be able to:

- Explain the purpose of network models and why we use layers.
- Describe the **TCP/IP five-layer model** and the **OSI seven-layer model**.
- Identify common networking devices: cables, hubs, switches, routers, servers, and clients.
- Describe what happens at the **physical layer** and the **data link layer** of a network.
- Recognize the role of MAC addresses and Ethernet frames in local communication.

---

## 1. Network Models

### 1.1 Why use layers?

Real-world networks are complex. To manage this complexity, networking is described using
**layered models**. Each layer has a clear responsibility and interacts only with the layer
directly above and below it. This brings several benefits:

- Easier design and troubleshooting.
- The ability to replace or upgrade one layer without redesigning the others.
- A common language for vendors, engineers, and standards bodies.

Two models are especially important: the **TCP/IP five-layer model** and the **OSI seven-layer model**.

### 1.2 The TCP/IP Five-Layer Network Model

The TCP/IP model is the practical model most closely aligned with how the Internet works today.
From bottom to top, the five layers are:

1. **Physical layer**  
   - Handles the actual transmission of bits over a medium (copper, fiber, radio, etc.).  
   - Defines voltage levels, timing, connectors, and signaling methods.

2. **Data link layer**  
   - Provides node-to-node delivery across a single physical network segment.  
   - Uses MAC addresses and frames; handles access to the medium and basic error detection.

3. **Network layer**  
   - Provides logical addressing and routing between networks.  
   - Uses IP addresses and routing protocols to move packets across multiple hops.

4. **Transport layer**  
   - Provides end-to-end communication between applications on different hosts.  
   - Implements concepts like ports, connections, reliability (TCP), or best-effort delivery (UDP).

5. **Application layer**  
   - Includes all protocols and services that applications use directly: HTTP, DNS, SMTP, etc.  
   - Responsible for presenting data in a form that users and applications understand.

As data moves down the stack on the sender, each layer adds its own header (encapsulation).
On the receiver, the headers are removed in reverse order (decapsulation).

### 1.3 The OSI Networking Model

The **OSI (Open Systems Interconnection) model** is a more detailed, conceptual model
with **seven** layers:

1. Physical  
2. Data Link  
3. Network  
4. Transport  
5. Session  
6. Presentation  
7. Application  

The top three layers (Session, Presentation, Application) describe how applications establish,
manage, and format communication sessions. In practice, many of their responsibilities are
grouped together in the Application layer of the TCP/IP model, but the OSI model is still very
useful for teaching and troubleshooting because it provides a clear, fine-grained framework.

### 1.4 Comparing TCP/IP and OSI

- Both models start with **Physical**, **Data Link**, **Network**, and **Transport** layers that
  align quite closely.
- The OSI model splits application-level concerns into three layers (Session, Presentation,
  Application), while the TCP/IP model bundles them into a single **Application** layer.
- When troubleshooting, engineers often say things like “this is a Layer 2 issue” or
  “this looks like a Layer 3 problem,” referring to OSI layers as shorthand.

---

## 2. The Basics of Networking Devices

Modern networks rely on a combination of physical media and active devices. At a high level,
you will encounter the following building blocks.

### 2.1 Cables

**Cables** provide the physical path over which bits travel.

- **Twisted-pair copper** (e.g., Cat5e, Cat6) is widely used for Ethernet in local networks.  
  Pairs of wires are twisted to reduce electromagnetic interference.  
- **Fiber-optic cables** use light instead of electricity, allowing much higher speeds and
  longer distances.  
- Each cable type has specified maximum length and performance characteristics; choosing the
  right one is crucial for a reliable network.

### 2.2 Hubs and Switches

- A **hub** is a simple, legacy device that repeats incoming electrical signals out of all
  other ports. It operates purely at the **physical layer**, creates a single collision domain,
  and is rarely used today due to poor efficiency and scalability.
- A **switch** is a smarter device that operates at the **data link layer**. It:
  - Learns **MAC addresses** and builds a forwarding table.
  - Forwards frames only to the correct port instead of broadcasting to all ports.
  - Greatly reduces collisions and improves performance compared to hubs.

In modern Ethernet networks, switches are the standard way to connect hosts within the same LAN.

### 2.3 Routers

A **router** connects multiple networks together and operates primarily at the **network layer**.

- Uses **IP addresses** and routing tables to decide where to send packets next.
- Separates broadcast domains, provides path selection, and often implements basic firewalling,
  NAT, and other edge functions.
- Home “Wi-Fi routers” typically combine several functions: router, switch, wireless access
  point, and sometimes modem.

### 2.4 Servers and Clients

- A **server** is a host that provides services or resources (web pages, files, databases,
  authentication, etc.) to other devices on the network.
- A **client** is a host that requests and consumes these services (web browsers, email apps,
  mobile apps, etc.).
- In many environments, a single physical machine may act as both client and server,
  depending on the role it plays in the communication.

---

## 3. The Physical Layer

The **physical layer** is all about getting individual bits from one device to another.

### 3.1 Moving Bits Across the Medium

- Data is encoded as electrical signals, light pulses, or radio waves depending on the medium.  
- The physical layer defines how 0s and 1s are represented (line coding), bit timing,
  and how devices detect collisions or link failures.
- Transmission can be **simplex** (one direction), **half-duplex** (both directions, but
  not at the same time), or **full-duplex** (both directions simultaneously).

### 3.2 Twisted Pair Cabling and Duplexing

Twisted-pair Ethernet cabling uses multiple wire pairs:

- Different pairs handle sending and receiving signals.  
- Proper **duplex configuration** (half vs full) is essential to avoid collisions and
  performance problems.
- Modern switches and network interface cards (NICs) usually auto-negotiate speed and duplex,
  but mismatches can still occur in misconfigured environments.

### 3.3 Ethernet Over Twisted Pair and Crossover Cables

- **Straight-through cables** connect devices of different types (e.g., host to switch, switch
  to router) in older standards, with transmit wires on one side matching receive wires on the other.
- **Crossover cables** were traditionally used to connect similar devices directly
  (switch-to-switch, host-to-host) by swapping the transmit and receive pairs.
- Today, most modern interfaces support **auto-MDI/MDI-X**, which automatically adjusts to
  either configuration, making crossover cables largely unnecessary but still important
  to understand historically.

### 3.4 Network Ports and Patch Panels

- **Network ports** on wall outlets, switches, and routers provide standardized connection
  points for network cables.
- **Patch panels** gather many cable runs into a single, organized location (e.g., a rack).
  Short patch cables connect ports on the panel to switch ports.
- Proper labeling and cable management at this level are critical for scalable, maintainable networks.

### 3.5 Cabling Tools

Network technicians rely on several tools at the physical layer:

- **Cable crimpers** to attach connectors (e.g., RJ-45) to copper cables.
- **Cable strippers** to prepare the cable jacket without damaging the inner pairs.
- **Cable testers and certifiers** to verify correct pin-out, continuity, and performance.
- **Tone generator and probe** to trace cable runs in complex environments.

---

## 4. The Data Link Layer

The **data link layer** sits directly above the physical layer and is responsible for reliable
local delivery of frames between nodes on the same network segment.

### 4.1 Ethernet and MAC Addresses

Ethernet is the dominant technology at the data link layer in wired LANs.

- Each network interface card (NIC) has a **MAC (Media Access Control) address**, typically
  a 48-bit value written in hexadecimal (for example, `00:1A:2B:3C:4D:5E`).
- MAC addresses are used for **local identification** on a single broadcast domain.
- Switches build a **MAC address table** mapping MAC addresses to specific switch ports,
  allowing them to forward frames efficiently.

### 4.2 Unicast, Multicast, and Broadcast

Ethernet supports three basic types of frame delivery:

- **Unicast**  
  - One-to-one communication.  
  - Frame is addressed to a single destination MAC; switches forward it only to the correct port.

- **Multicast**  
  - One-to-many communication.  
  - Frame is addressed to a special multicast MAC; hosts that have joined the multicast group
    process the frame, others ignore it.

- **Broadcast**  
  - One-to-all communication on the local network.  
  - Destination MAC is the broadcast address (`FF:FF:FF:FF:FF:FF`); all hosts on the LAN
    receive and process the frame.  
  - Broadcasts are necessary for some protocols (e.g., ARP) but must be limited because
    excessive broadcast traffic can degrade performance.

### 4.3 Dissecting an Ethernet Frame

An **Ethernet frame** wraps higher-layer data with data link layer information. At a high level,
a frame contains:

- **Destination MAC address**  
- **Source MAC address**  
- **EtherType / Length field** (indicates which protocol is encapsulated, such as IPv4 or IPv6)  
- **Payload** (the network-layer packet and any higher-layer data)  
- **Frame Check Sequence (FCS)** for error detection

At this layer, Ethernet provides:

- **Framing** – clear start and end of each unit of data.  
- **Local delivery** – moving frames from one NIC to another on the same network segment.  
- **Error detection** – corrupted frames are detected and discarded.

---

## 5. Summary

This introductory chapter established the foundation for the rest of your networking notes:

- We use **layered network models** to manage complexity and standardize communication.
- The **TCP/IP five-layer model** is the practical model of the Internet, while the **OSI
  seven-layer model** is a more detailed conceptual reference.
- Basic networking devices—**cables, hubs, switches, routers, servers, and clients**—work
  together to move data and provide services.
- At the **physical layer**, raw bits travel as electrical signals or light across various media,
  using structured cabling and specialized tools.
- At the **data link layer**, **Ethernet** uses **MAC addresses** and **frames** to provide
  reliable local delivery, using unicast, multicast, and broadcast communication patterns.

In the next chapter, you will dive deeper into the **network layer**, where IP addressing and
routing allow communication across multiple interconnected networks.
