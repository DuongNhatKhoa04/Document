# Connecting to the Internet

Modern networks use a wide variety of **physical media** and **access technologies** to
reach the Internet. This chapter looks at how endpoints actually connect, from
legacy dial-up to fiber, WAN links between sites, and today’s wireless and cellular
networks.

---

## 1. POTS and Dial-up

### 1.1 Plain Old Telephone Service (POTS)

The earliest consumer Internet connections used the existing **analog telephone network**,
often called **POTS – Plain Old Telephone Service**.

Characteristics:

- Designed originally for **voice**, not data.
- Uses copper twisted-pair lines from the customer premises to the telephone exchange.
- Limited bandwidth and subject to analog noise and signal degradation.

### 1.2 Dial-up and Modems

**Dial-up Internet** used **modems** (modulator–demodulator) to encode digital data as
analog tones that could travel over POTS lines.

High-level properties:

- Speeds typically from 56 kbps and below – **very slow** by modern standards.
- Connection required dialing a phone number; the line was busy while connected.
- Latency and reliability were limited, but it made early mass-market Internet access possible.

Dial-up is largely obsolete today, but understanding it provides context for why newer
broadband technologies were needed.

---

## 2. Broadband Connections

### 2.1 What Is Broadband?

**Broadband** refers to high-speed, “always-on” Internet access that supports:

- Much higher data rates than dial-up.
- Simultaneous use of **voice and data** on the same line (or separate medium).
- Shared access for many devices in homes and businesses.

Common broadband technologies include **T-carrier**, **DSL**, **cable**, and **fiber**.

### 2.2 T-Carrier Technologies

**T-carrier** systems are digital circuits traditionally used by telecom providers:

- **T1** lines offer 1.544 Mbps, composed of 24 digital channels.
- **T3** lines offer 44.736 Mbps, aggregating multiple T1s.

Key ideas:

- Provide dedicated, point-to-point connectivity between locations.
- Historically popular for business WAN links and early high-speed Internet access.
- Often replaced today by Ethernet-based and fiber services but still useful to know.

### 2.3 Digital Subscriber Lines (DSL)

**DSL (Digital Subscriber Line)** uses higher-frequency ranges on existing copper telephone
pairs to deliver broadband without interfering with analog voice.

High-level concepts:

- **Asymmetric DSL (ADSL)** – higher downstream than upstream bandwidth, optimized for web
  browsing and media consumption.
- **VDSL and VDSL2** – newer DSL variants that provide higher speeds over shorter distances.
- Speeds depend heavily on **line quality** and **distance** from the provider’s equipment.

DSL allowed telcos to upgrade customers from dial-up to broadband using existing copper
infrastructure.

### 2.4 Cable Broadband

**Cable broadband** leverages the **coaxial cable** originally installed for cable TV:

- Uses standards such as **DOCSIS** for data transmission.
- Typically offers higher speeds than DSL, especially in downstream direction.
- Networks are often **shared** among many subscribers in a neighborhood, so available
  bandwidth can vary with usage.

Cable modems connect customer equipment to the provider’s hybrid fiber-coax network.

### 2.5 Fiber Connections

**Fiber-optic broadband** is the current gold standard for access speed and reliability.

Characteristics:

- Uses light over glass fiber; resistant to electrical interference.
- Supports very high bandwidth (hundreds of Mbps to multi-Gbps) and long distances.
- Common deployment models:
  - **FTTH/FTTP (Fiber to the Home/Premises)**
  - **FTTC (Fiber to the Curb/Cabinet)** with copper for the final segment.

Fiber is increasingly common in urban and suburban areas and underpins much of the
global Internet backbone.

### 2.6 Broadband Protocols (High-Level View)

Regardless of the medium, broadband services often rely on higher-level protocols such as:

- **PPP and PPPoE** – encapsulate PPP over Ethernet for authentication and configuration.
- **DOCSIS** – defines how data is transmitted over cable networks.
- Various **Ethernet** and **MPLS**-based technologies for carrier networks.

End users typically see only an Ethernet handoff from their modem or router, while
these protocols operate behind the scenes.

---

## 3. Wide Area Networks (WANs)

### 3.1 WAN Concepts

A **Wide Area Network (WAN)** connects geographically separated sites:

- Corporate offices, data centers, branch locations, and cloud providers.
- Often built using services purchased from telecom carriers.

Key differences from LANs:

- Longer distances, higher latency.
- Links are usually **leased** or provisioned as a service rather than owned outright.
- Reliability, redundancy, and service-level agreements (SLAs) are critical.

### 3.2 WAN Technologies (High-Level)

Common WAN building blocks include:

- **Leased lines / private circuits** – dedicated point-to-point connections.
- **MPLS (Multiprotocol Label Switching)** – carrier technology providing virtual private
  networks over shared infrastructure.
- **Metro Ethernet** – Ethernet-based services connecting sites at metropolitan scale.
- **Satellite and microwave links** – used where wired infrastructure is impractical.

The choice of technology depends on required bandwidth, distance, cost, and availability.

### 3.3 WAN Protocols (Conceptual)

Historically, WANs used protocols such as:

- **Frame Relay**, **ATM**, and **HDLC** on serial links.
- **PPP (Point-to-Point Protocol)** for link-layer framing, authentication, and IP
  configuration on point-to-point links.

Many of these are legacy today, replaced by Ethernet and IP-based solutions, but they
illustrate how WANs evolved.

### 3.4 Point-to-Point VPNs

Organizations increasingly use **point-to-point VPNs** over the public Internet instead
of dedicated circuits:

- Secure, encrypted tunnels between sites or between a site and a cloud provider.
- Achieve private-network semantics while leveraging inexpensive public connectivity.
- Often implemented with technologies like IPsec or modern site-to-site VPN appliances.

From the perspective of internal routers, a VPN tunnel behaves much like a private WAN link.

---

## 4. Wireless Networking

### 4.1 Introduction to Wireless Networking Technologies

Wireless networks replace copper or fiber with **radio waves**:

- Provide mobility and flexible deployment.
- Operate under various standards and frequency bands (Wi-Fi, Bluetooth, cellular, etc.).
- Require careful planning for **coverage**, **capacity**, and **security**.

### 4.2 Wi-Fi and the 802.11 Family

**Wi-Fi** is the common name for IEEE **802.11** wireless LAN standards.

High-level features:

- Operates mainly in **2.4 GHz**, **5 GHz**, and newer **6 GHz** bands.
- Standards such as 802.11n, 802.11ac, and **802.11ax (Wi-Fi 6)** introduce higher
  throughput and better efficiency.
- Uses access points to provide coverage and manage access for many clients.

**Wi-Fi 6** improves:

- Performance in dense environments (stadiums, offices, apartments).
- Efficiency through technologies like OFDMA and improved scheduling.
- Battery life for clients via better power-saving mechanisms.

### 4.3 “Alphabet Soup” and IoT Data Transfer Protocols

The wireless world includes many specialized protocols, often known by acronyms:

- **Bluetooth / Bluetooth Low Energy (BLE)** – short-range personal area networking.
- **Zigbee, Thread, Z-Wave** – low-power mesh networks for sensors and home automation.
- **LoRaWAN, Sigfox, NB-IoT** – long-range, low-bit-rate technologies for IoT devices.

These protocols trade speed for **range**, **power efficiency**, or **simplicity**, depending
on the use case.

### 4.4 Wireless Network Configurations

Common Wi-Fi deployment models:

- **Infrastructure mode** – standard model with access points and clients.
- **Ad hoc mode** – peer-to-peer communication without central infrastructure.
- **Mesh networks** – multiple access points relay traffic for wider coverage.
- **Hotspots** – public access provided by ISPs, venues, or mobile devices.

Network design balances coverage, capacity, and roaming behavior.

### 4.5 Wireless Channels

Wireless networks share the air, so **channel planning** is critical:

- Different channels correspond to different frequency slices within a band.
- In 2.4 GHz, only a few channels are non-overlapping, so interference is common.
- 5 GHz and 6 GHz bands offer more non-overlapping channels and higher potential throughput.
- Proper channel selection and transmit-power control help reduce interference
  and improve performance.

### 4.6 Wireless Security

Because radio signals can be received by anyone within range, **security** is a primary concern.

Key ideas:

- **Authentication** – verifying who is allowed to join the network.
- **Encryption** – protecting data in transit from eavesdropping.
- **Network segmentation** – separating guest, corporate, and management traffic.

Best practices avoid legacy mechanisms like open networks and WEP, and instead rely on
modern encryption methods.

### 4.7 Protocols and Encryption (High-Level)

Common Wi-Fi security mechanisms:

- **WPA2-Personal (PSK)** – shared passphrase; suitable for home networks.
- **WPA2-Enterprise / WPA3-Enterprise** – uses 802.1X and a RADIUS server for per-user
  authentication and dynamic keys.
- **WPA3** – introduces stronger cryptography and better protection against offline attacks.

Beyond Wi-Fi, many wireless protocols (Bluetooth, cellular, IoT) include their own
encryption and authentication schemes to protect data.

### 4.8 Cellular Networking

Cellular networks provide wide-area wireless connectivity using licensed spectrum and
a network of base stations.

High-level overview:

- **GSM/2G → 3G → 4G LTE → 5G** – each generation improves speed, latency, and capacity.
- Mobile devices connect to the nearest **cell**, handing off between cells as they move.
- The **SIM (Subscriber Identity Module)** securely identifies the subscriber to the network.
- Carriers provide data, voice, and messaging services, often integrated with the Internet.

Cellular networks are essential for mobile Internet access, IoT, and broadband in areas
where wired infrastructure is limited.

### 4.9 Mobile Device Networks

Mobile devices typically use a combination of:

- **Wi-Fi** – for local high-speed access (home, office, public hotspots).
- **Cellular data** – for wide-area connectivity.
- **Tethering / hotspot** features – sharing one device’s connection with others.

Considerations:

- Roaming between networks and coverage areas.
- Data caps and performance differences between Wi-Fi and cellular.
- Security practices when using public or untrusted networks.

---

## 5. Summary

This chapter explored how devices physically and logically **connect to the Internet**:

- Legacy **POTS and dial-up** connections introduced mass-market Internet access but are
  now replaced by faster broadband technologies.
- **Broadband** options—T-carrier, DSL, cable, and fiber—provide always-on, high-speed
  connectivity using different media and protocols.
- **WANs** connect sites across large distances using leased lines, MPLS, Metro Ethernet,
  and increasingly **point-to-point VPNs** over the public Internet.
- **Wireless networking** (Wi-Fi, IoT protocols, cellular) delivers mobility and flexibility,
  while channel planning, encryption, and authentication keep these networks secure.

Together, these technologies form the access layer of the Internet, bridging end users,
organizations, and the global network infrastructure described in earlier chapters.
