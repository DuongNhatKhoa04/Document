# The Network Layer

The **network layer** is responsible for moving packets between different networks.
While the data link layer focuses on local delivery within a single segment, the
network layer enables **end-to-end communication across multiple hops**. On the
Internet, this role is primarily fulfilled by the **Internet Protocol (IP)**.

---

## 1. Role of the Network Layer

At a high level, the network layer provides:

- **Logical addressing** – assigning IP addresses that identify hosts and networks.
- **Routing** – choosing a path across interconnected networks.
- **Forwarding** – moving packets from one interface to another based on routing decisions.
- **Fragmentation (legacy)** – splitting packets when they exceed a link’s maximum
  transmission unit (MTU).

Routers operate mainly at this layer. They examine the destination IP address of a packet,
consult a **routing table**, and forward the packet closer to its destination.

---

## 2. IPv4 Addresses

### 2.1 Address Structure

An **IPv4 address** is a 32-bit value, typically written in **dotted-decimal** form,
such as `192.168.10.25`.

- 32 bits → four octets (8 bits each).
- Each octet ranges from 0–255.
- Conceptually, an IP address has two parts:
  - **Network portion** – identifies the network.
  - **Host portion** – identifies a specific device within that network.

The boundary between network and host is defined by a **subnet mask** or **prefix length**
(e.g., `/24`).

### 2.2 IPv4 Address Classes (Historical View)

Originally, IPv4 addresses were grouped into fixed **classes**:

- **Class A** – `0.0.0.0` to `127.255.255.255` (default mask `/8`).
- **Class B** – `128.0.0.0` to `191.255.255.255` (default mask `/16`).
- **Class C** – `192.0.0.0` to `223.255.255.255` (default mask `/24`).
- **Class D** – `224.0.0.0` to `239.255.255.255` (multicast).
- **Class E** – `240.0.0.0` to `255.255.255.255` (experimental).

Classful addressing is mostly **historical**. Modern networks use **Classless Inter-Domain
Routing (CIDR)**, which allows flexible prefix lengths instead of fixed classes. However,
understanding classes is still useful when reading older documentation or legacy networks.

---

## 3. IPv4 Datagram and Encapsulation

The basic unit at the network layer is the **IP datagram** (often called an IP packet).

### 3.1 Encapsulation

When an application sends data:

1. The data is handed to the **transport layer** (e.g., TCP or UDP), which adds its own header.
2. The resulting segment is passed to the **network layer**, which encapsulates it in an IP header,
   forming an **IP datagram**.
3. The datagram is then encapsulated in a **data link layer frame** (e.g., Ethernet frame) and
   transmitted over the physical medium.

Each router along the path decapsulates the frame, inspects the **IP header** to determine
where to send the packet next, and then re-encapsulates it in a new frame for the next link.

### 3.2 Key Fields in the IPv4 Header (High Level)

Important IPv4 header fields include:

- **Source IP address** – where the packet originated.
- **Destination IP address** – where the packet is going.
- **Time To Live (TTL)** – a counter decremented at each hop; when it reaches 0, the packet
  is discarded. This prevents packets from circulating forever.
- **Protocol** – indicates the encapsulated transport protocol (e.g., TCP = 6, UDP = 17, ICMP).
- **Total Length** – size of the entire datagram.
- **Identification, Flags, Fragment Offset** – used for fragmentation and reassembly when a packet
  must be split across links with smaller MTUs.
- **Header Checksum** – error detection for the IP header itself.

Routers primarily care about the **destination address**, **TTL**, and **protocol** fields
during forwarding.

---

## 4. Address Resolution Protocol (ARP)

At the network layer we use **IP addresses**, but at the data link layer (Ethernet) we use
**MAC addresses**. **Address Resolution Protocol (ARP)** bridges this gap.

- When a host wants to send a packet to another IP on the same network, it must know the
  **destination MAC address**.
- If it only knows the IP, it sends an **ARP request** (broadcast) asking:
  “Who has IP X.X.X.X? Tell Y.Y.Y.Y.”
- The host with that IP replies with an **ARP reply** (unicast), providing its MAC address.
- The sender caches this mapping in an **ARP table** for future use.

Routers also use ARP to learn the MAC addresses of neighboring devices on directly connected networks.

---

## 5. Subnetting and Subnet Masks

### 5.1 Why Subnet?

**Subnetting** is the process of dividing a larger IP network into smaller, logical networks.

Benefits:

- Better use of limited IPv4 address space.
- Improved performance and reduced broadcast traffic.
- Logical separation of departments, locations, or security zones.
- Clearer routing and easier troubleshooting.

### 5.2 Subnet Masks and Prefix Lengths

A **subnet mask** is a 32-bit number that indicates which part of an IP address is the
network portion and which part is the host portion.

- Written in dotted-decimal: e.g., `255.255.255.0`.
- Written in prefix notation: e.g., `/24`.
- Bits set to **1** mark the **network**; bits set to **0** mark the **host**.

Example:

- IP: `192.168.10.25`
- Mask: `255.255.255.0` → `/24`
- Network: `192.168.10.0`
- Host part: last 8 bits.

### 5.3 Basic Binary Math (Conceptual)

Subnetting calculations rely on **binary**:

- Each octet is 8 bits, e.g., `255` = `11111111₂`, `0` = `00000000₂`.
- Masks are contiguous 1s followed by 0s (e.g., `/26` is `11111111.11111111.11111111.11000000`).
- The number of host bits determines how many usable IP addresses are in a subnet:
  - `2^(host bits) − 2` (subtracting network and broadcast addresses for traditional IPv4 subnets).

You do not need to perform every calculation by hand in real networks, but understanding the
binary structure makes CIDR and routing behavior much clearer.

### 5.4 Classless Inter-Domain Routing (CIDR)

**CIDR** replaces classful boundaries with flexible prefixes:

- Networks are written as `<network address>/<prefix length>`, e.g. `10.0.0.0/8`,
  `192.168.10.0/24`, `172.16.0.0/16`.
- Allows service providers and enterprises to allocate address blocks that better fit
  their actual size.
- Enables **route aggregation (supernetting)**, where multiple networks can be summarized
  into a single shorter prefix to keep routing tables smaller.

CIDR is fundamental to scalable Internet routing.

---

## 6. Routing Fundamentals

### 6.1 Basic Routing Concepts

**Routing** is the process of selecting a path for traffic in a network, while
**forwarding** is the act of sending packets out of the correct interface based on that path.

Key ideas:

- Every router maintains a **routing table**.
- Routes typically consist of:
  - Destination network (in CIDR notation).
  - Next hop (IP of the next router) or outgoing interface.
  - Metric or preference value.
- When a packet arrives, the router performs a **longest prefix match**:
  - It selects the route whose prefix most specifically matches the destination IP.

Routers can learn routes in three main ways:

1. **Directly connected networks** – interfaces configured with IP addresses and masks.
2. **Static routes** – manually configured by an administrator.
3. **Dynamic routing protocols** – routers exchange information automatically.

### 6.2 Routing Tables

A routing table might contain entries such as:

- Directly connected network: `192.168.10.0/24 via interface eth0`.
- Static route: `10.0.0.0/8 via next hop 203.0.113.1`.
- Default route: `0.0.0.0/0 via ISP gateway`.

The **default route** acts as a “catch-all” for destinations not covered by more specific
entries and is especially important on edge routers and end hosts.

### 6.3 Interior Gateway Protocols (IGPs)

Within a single organization or **autonomous system (AS)**, routers typically use an
**Interior Gateway Protocol (IGP)** to share routing information.

Conceptually, there are two main families:

- **Distance-vector protocols**  
  - Routers share information about the “distance” to networks (hop count or metrics).  
  - Classic example: RIP (Routing Information Protocol).

- **Link-state protocols**  
  - Routers build a complete map of the network’s topology and compute the best path using
    algorithms like Dijkstra’s shortest path.  
  - Examples: OSPF (Open Shortest Path First), IS-IS.

IGPs aim for **fast convergence**, scalability inside the organization, and resilience.

### 6.4 Exterior Gateway Protocols, Autonomous Systems, and IANA

On the global Internet, different organizations (ISPs, large enterprises, content providers)
are represented as **autonomous systems** (AS). To exchange routes between these ASes,
networks use an **Exterior Gateway Protocol (EGP)**.

- The dominant EGP is **BGP (Border Gateway Protocol)**.
- Each AS has a unique **AS number (ASN)**.
- Routing between ASes considers policies, business relationships, and traffic engineering,
  not just shortest path.

Global coordination of IP address blocks and AS numbers is handled by the **Internet Assigned
Numbers Authority (IANA)** and regional Internet registries. This ensures uniqueness and
prevents conflicts.

---

## 7. Non-Routable Address Space

Certain IPv4 ranges are **non-routable on the public Internet** and are reserved for
special purposes.

### 7.1 Private Address Ranges (RFC 1918)

Reserved for private networks:

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

These addresses can be used freely inside organizations. Traffic to the Internet is typically
translated via **Network Address Translation (NAT)** at the edge.

### 7.2 Other Special Addresses

- **Loopback** – `127.0.0.0/8` (commonly `127.0.0.1`) used for testing local networking stacks.
- **Link-local** – `169.254.0.0/16` for automatic addressing when DHCP is unavailable.
- **Broadcast** – `255.255.255.255` (local broadcast) and per-subnet broadcast addresses.
- Various other reserved ranges exist for documentation, testing, and other special uses.

Understanding these ranges helps avoid misconfigurations and routing issues.

---

## 8. Standards and RFCs

Internet protocols are documented in **Requests for Comments (RFCs)**, maintained by the
Internet Engineering Task Force (IETF).

- RFCs describe standards, best practices, and experimental ideas.
- Core IPv4 behavior, addressing rules, and routing protocols are all defined in specific RFCs.
- Network engineers frequently refer to RFCs when implementing, debugging, or validating
  protocol behavior.

While you do not need to memorize every RFC, it is important to know that they are the
authoritative source for protocol specifications.

---

## 9. Summary

In this chapter, you learned the high-level concepts that define the **network layer**:

- IPv4 provides **logical addressing** and forms the basis of global internetworking.
- IP datagrams encapsulate transport segments and are forwarded hop-by-hop across routers.
- **ARP** resolves IP addresses to MAC addresses on local networks.
- **Subnetting**, **subnet masks**, and **CIDR** allow flexible, efficient use of IPv4 space.
- **Routing** uses routing tables, static routes, and dynamic protocols to move traffic across
  complex topologies.
- Distinct routing domains (autonomous systems) exchange reachability information using BGP,
  while internal networks use IGPs such as OSPF or RIP.
- **Private** and other non-routable address ranges are reserved for special uses and must be
  handled carefully at network edges.
- Underlying all of this, **RFCs** capture the formal standards that make the Internet
  interoperable.

These concepts provide the foundation for the next chapter, where you will study the
**transport and application layers** and see how applications build on top of IP to deliver
end-to-end services.
