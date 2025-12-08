# Networking Services

Above the core transport and network protocols, real-world networks rely on a set of
**networking services**. These services make the Internet usable, scalable, and more secure.

This chapter covers the most important ones:

- **DNS** – turning names into IP addresses.
- **DHCP** – automatically assigning IP configuration.
- **NAT** – extending IPv4 address space.
- **VPNs and proxies** – adding privacy, security, and control.

---

## 1. Name Resolution and the Domain Name System (DNS)

### 1.1 Why Do We Need DNS?

Humans prefer **names** like `www.example.com`.  
Routers and hosts, however, forward traffic using **IP addresses**.

The **Domain Name System (DNS)** is the distributed database that maps **domain names** to
**IP addresses** and other information. Without DNS, users would have to remember numeric
addresses, and changing a server’s IP would break every client configuration.

DNS provides:

- A global, hierarchical namespace (`example.com`, `sub.example.com`).
- Flexible mapping from names to IPv4/IPv6 addresses.
- Additional records for email routing, service discovery, and more.

### 1.2 The Many Steps of Name Resolution

When you type a URL into a browser, a number of components cooperate to resolve the name:

1. **Application** checks its own cache (browser cache).
2. **Operating system resolver** checks the local DNS cache and configuration (e.g., `/etc/hosts`).
3. If not found, the request is sent to a **recursive resolver** (often a DNS server run by
   your ISP or organization).
4. The recursive resolver may:
   - Answer from its own cache, or
   - Perform **iterative queries** on your behalf:
     - Ask a **root server** which **top-level domain (TLD)** server to contact.
     - Ask the TLD server (e.g., `.com`) which **authoritative server** handles `example.com`.
     - Ask the authoritative server for the specific record (e.g., `www.example.com`).
5. The answer is cached at each step for a defined **time to live (TTL)** to reduce load and
   speed up future queries.

The user only sees a short delay before the website loads, but under the hood DNS performs
this multi-step process quickly and efficiently.

### 1.3 DNS and UDP

DNS most commonly uses **UDP port 53**:

- UDP’s low overhead is ideal for short request/response messages.
- DNS messages fit within a single UDP datagram in the common case.

In some situations, DNS uses **TCP** instead:

- When responses are too large for a single UDP packet (e.g., many records).
- For specific operations such as **zone transfers** between DNS servers.

From the application’s perspective, this is transparent; the resolver library handles the
transport details.

---

## 2. DNS in Practice

### 2.1 Resource Record Types

A DNS **zone** contains **resource records (RRs)**, each storing specific information.

Common record types (high-level view):

- **A** – Maps a name to an IPv4 address.
- **AAAA** – Maps a name to an IPv6 address.
- **CNAME** – Canonical name; an alias that points one name to another name.
- **MX** – Mail exchanger; specifies mail servers for a domain.
- **NS** – Name server; identifies authoritative DNS servers for a zone.
- **TXT** – Free-form text; often used for verification and security (SPF, DKIM).
- **SRV** – Service locator; specifies host and port for particular services.

Clients typically request A/AAAA records, but administrators work with many record types
to support email, authentication, and advanced services.

### 2.2 Anatomy of a Domain Name

A domain name is **hierarchical**, read from right to left:

- `www.mail.example.com`
  - `.com` – **Top-Level Domain (TLD)**.
  - `example` – **Second-level domain**, registered to an organization.
  - `mail` – Subdomain created by that organization.
  - `www` – Host or service label.

Each level represents administrative control. Organizations can create subdomains to
organize services, locations, or departments (`eu.example.com`, `api.example.com`, etc.).

### 2.3 DNS Zones

A **zone** is a portion of the DNS namespace that is managed by a particular organization
or administrator.

Key concepts:

- A zone contains the records for one or more **domains**.
- **Authoritative DNS servers** host the zone data and provide official answers.
- Zones can be split or delegated:
  - `example.com` might be managed by one team.
  - `us.example.com` could be delegated to another team with their own servers.
- **Zone transfers** (AXFR/IXFR over TCP) synchronize data between primary and secondary
  authoritative servers for redundancy.

This distributed design allows DNS to scale to the entire Internet while still allowing
local control.

---

## 3. Dynamic Host Configuration Protocol (DHCP)

### 3.1 Overview of DHCP

Manually assigning IP addresses and settings to every device does not scale.  
The **Dynamic Host Configuration Protocol (DHCP)** automates this process.

DHCP can provide:

- IP address and subnet mask.
- Default gateway.
- DNS servers.
- Other options (NTP servers, domain name, etc.).

### 3.2 DHCP in Action (Conceptual DORA Process)

When a client joins a network and needs an IP configuration, a typical sequence is:

1. **Discover** – Client broadcasts a DHCPDISCOVER message to find available DHCP servers.
2. **Offer** – One or more servers respond with a DHCPOFFER, proposing an IP address and config.
3. **Request** – Client chooses an offer and sends a DHCPREQUEST, indicating its selection.
4. **Acknowledge** – The chosen server sends a DHCPACK, confirming the lease.

Key ideas:

- Addresses are leased for a configurable **lease time** and can be renewed.
- DHCP can reserve fixed addresses for specific MAC addresses (“DHCP reservations”).
- DHCP is typically delivered over UDP (client port 68, server port 67).

DHCP radically simplifies client configuration and helps avoid IP conflicts.

---

## 4. Network Address Translation (NAT)

### 4.1 Basics of NAT

**Network Address Translation (NAT)** allows multiple internal devices with **private IP
addresses** to share a smaller number of **public IP addresses**.

At the edge router (often called a NAT gateway):

- Outbound packets have their **source IP** replaced with the router’s public IP.
- The router keeps a **translation table** to match returning traffic back to the correct
  internal host.

Benefits:

- Conserves scarce IPv4 addresses.
- Hides internal addressing structure from the public Internet (basic privacy and security).
- Enables flexible internal addressing independent of ISP assignment.

### 4.2 NAT and the Transport Layer (PAT)

Most home and small-business networks actually use **Port Address Translation (PAT)**,
a form of NAT that also translates **transport ports**:

- Multiple internal clients can share a single public IP.
- The NAT device rewrites:
  - Source IP and source port for outbound packets.
  - Destination IP and destination port for inbound replies.
- The mapping `(internal IP, internal port)` ↔ `(public IP, public port)` is stored in a table.

Implications:

- Outbound connections generally work without special configuration.
- **Inbound** connections (unsolicited traffic from the Internet) are blocked unless you set up
  **port forwarding**, use protocols that assist with NAT traversal, or use a VPN.

### 4.3 IPv4 Address Exhaustion (High-Level Context)

NAT became widespread due to **IPv4 address exhaustion**:

- IPv4 provides about 4.3 billion addresses, which is not enough for every device on Earth.
- Private address space plus NAT stretches the usable pool but introduces complexity and
  breaks strict end-to-end connectivity.
- **IPv6** is designed to solve this long-term with a vastly larger address space, but NAT
  will remain relevant for many years during the transition.

---

## 5. VPNs and Proxy Services

### 5.1 Virtual Private Networks (VPNs)

A **Virtual Private Network (VPN)** creates an **encrypted tunnel** over a public or untrusted
network.

High-level goals:

- Allow remote users to securely access private networks (corporate intranets, home networks).
- Protect data from eavesdropping on untrusted networks (e.g., public Wi-Fi).
- Sometimes provide a different apparent public IP location for policy or access reasons.

Concepts:

- VPN endpoints encapsulate private traffic (IP packets) inside encrypted outer packets.
- Common technologies: IPsec, SSL/TLS-based VPNs (e.g., OpenVPN, WireGuard).
- Once connected, the client often behaves as if it were physically on the remote network,
  using private addresses and accessing internal services.

### 5.2 Proxy Services

A **proxy server** acts as an intermediary for requests from clients to other servers.

Types (conceptual):

- **Forward proxy**  
  - Clients send requests to the proxy; the proxy fetches content on their behalf.  
  - Used for content filtering, caching, access control, or hiding client IPs from the
    destination.

- **Reverse proxy**  
  - Sits in front of one or more servers and receives requests from the Internet.  
  - Performs load balancing, caching, TLS termination, and security filtering.  
  - External clients see only the proxy’s address, not the individual backend servers.

Differences from VPN:

- A VPN typically carries all or most network traffic from a device; a proxy usually handles
  only specific protocols or applications (e.g., HTTP).
- VPNs create virtual interfaces and routes; proxies operate at the application layer.

---

## 6. Summary

In this chapter, you explored the **networking services** that sit on top of the core
protocol stack:

- **DNS** resolves human-friendly names to IP addresses and uses resource records, zones,
  and caching to scale globally.
- **DHCP** automatically provides IP configuration to clients, simplifying network
  management.
- **NAT** (and PAT) extend IPv4 address space and alter how connections traverse the
  Internet, particularly affecting inbound traffic and end-to-end reachability.
- **VPNs** and **proxies** provide secure tunnels, privacy, load balancing, and control.

These services are essential for operating real networks.  
The next chapters will show how devices connect to the Internet and how to troubleshoot
issues across the entire stack.
