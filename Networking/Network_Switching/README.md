# Layer2 Network Switching

[Network-switching](https://www.youtube.com/watch?v=VYukAH86d2I&list=PLmVr8r1kmMm3HrwOC3beb96JjrBh46AIt)



# Introduction to Network Switching | Layer 2 Fundamentals Explained

**Source:** [Introduction to Network Switching | Layer 2 Fundamentals Explained](http://www.youtube.com/watch?v=VYukAH86d2I)
**Channel:** telecomTech

---

## 1. Overview of the OSI Model and Layers

* **OSI Model Purpose:** Used to define addressing schemes and communication methodologies across different layers, where each layer encapsulates its Protocol Data Unit (PDU) into the layer below it.
* **Transport Layer (Layer 4):**
* Addressing mechanism: Port numbers (correspond to specific applications on each host).
* Entity exchanged: Segments (communication between specific processes/applications).


* **Network Layer (Layer 3):**
* Addressing mechanism: IP addresses.
* Entity exchanged: Packets (communication from host-to-host / end device-to-end device).


* **Data Link Layer (Layer 2):**
* Addressing mechanism: Media Access Control (MAC) address.
* Entity exchanged: Frames (encapsulates the Layer 3 IP packet as its payload).
* Scope of communication: Hop-to-hop, router-to-router, or routing device-to-routing device.



---

## 2. Encapsulation & Hop-by-Hop Communication

* **Encapsulation:** The Ethernet header is added to the network layer packet, turning it into a frame at the data link layer.
* **Hop-by-Hop Nature:** Layer 2 communication moves data from one directly connected device to the next (host-to-switch, switch-to-router, router-to-router).
* **Address Persistence vs. Change:** While IP addresses remain constant from source to destination, **Layer 2 MAC addressing changes at every single hop** as it gets re-encapsulated across new links.

---

## 3. Sublayers of the Data Link Layer

The Data Link layer is divided into two primary sublayers:

1. **Logical Link Control (LLC) Sublayer:**
* Identifies which network layer protocol is being carried (e.g., IPv4, IPv6).
* Performs basic control functions.


2. **Media Access Control (MAC) Sublayer:**
* Responsible for framing, MAC addressing, and controlling access to the physical medium.
* Network switches operate primarily at this sublayer.
* **Key functions:**
* Defines rules to send/receive frames.
* Adds headers and trailers to perform framing.
* Manages MAC addressing.
* Controls access to the medium using **CSMA/CD** (wired Ethernet) and **CSMA/CA** (wireless Wi-Fi).
* Performs error detection using the **Frame Check Sequence (FCS)** trailer.
* Handles encapsulation and decapsulation of IP packets.





---

## 4. Fundamentals of Switching

* **Definition:** Switching refers to how a switch takes a frame on one port and decides which port to send it out of based on the destination MAC address.
* **MAC Address Table:** A construct maintained within switches that aids in the forwarding decision process.

---

## 5. Upcoming Layer 2 Technologies & Topics Covered in the Series

* Ethernet protocols and frameworks
* Collision domains and broadcast domains
* Virtual LANs (VLANs) and trunks
* Layer 2 loops and loop prevention protocols (Spanning Tree Protocol / STP)
* Security configurations (Port security, private VLANs)


---


Yes, **every time a packet crosses a router (a Layer 3 device), the Layer 2 MAC addresses are completely stripped away and replaced with new ones.**

Here is how this process links directly with how `traceroute` works:

### 1. What Happens to MAC Addresses at Every Hop?

* When a device sends a packet to a router, the destination MAC address of the Ethernet frame is set to that router's incoming interface MAC address.
* Once the router receives the frame, it **decapsulates** it (strips off the Ethernet header and trailer) to inspect the Layer 3 IP packet.
* The router looks up its routing table to find the next hop, decrements the TTL, and **re-encapsulates** the packet into a *brand-new* Ethernet frame.
* In this new frame, the **Source MAC** becomes the router's outgoing interface MAC, and the **Destination MAC** becomes the MAC address of the next router (or final destination).
* Therefore, while the **IP addresses** (source and destination) remain the same across the journey, the **MAC addresses change at every single router hop**.

---

### 2. How This Links with `Traceroute`

`Traceroute` operates primarily at **Layer 3 (Network Layer)**, but it entirely depends on **Layer 2 (Data Link Layer)** framing to move across each physical hop.

* **The Layer 3 Mechanism (TTL):** Traceroute sends packets (usually UDP or ICMP) with an IP header containing a **Time to Live (TTL)** value, starting at 1.
* **The Hop Discovery:**
1. The packet leaves your computer wrapped in a Layer 2 frame destined for your default gateway's MAC address.
2. The first router receives it, decrements the TTL to 0, drops the packet, and generates an ICMP "Time Exceeded" message back to you. The IP address of this router is recorded as "Hop 1."
3. For the next packet, traceroute sets TTL to 2. It reaches Router 1 (which decrements TTL to 1 and forwards it) and then hits Router 2 (which drops it, decrementing TTL to 0). Router 2's IP address is recorded as "Hop 2."


* **The Layer 2 Reality Behind It:** Even though `traceroute` shows you a list of **IP addresses** (routers), every single one of those intermediate steps required the packet to be unzipped from one Layer 2 frame and zipped into a new Layer 2 frame with completely new source and destination MAC addresses to cross that specific wire or link.



<br>

<br>

---

---



# How a Network Switch Works | CCNA Layer 2 Explained Simply

**Source:** [How a Network Switch Works | CCNA Layer 2 Explained Simply](http://www.youtube.com/watch?v=Hw38pPb-XNA)
**Channel:** telecomTech

---

## 1. Overview of Network Switches and Physical Ports

* **Physical Connections:** Switches contain multiple ports designed to connect end devices (PCs, laptops, IP phones, cameras, printers, TVs, wireless access points) or other network gear.
* **Port Types:**
* **RJ-45 Ports:** Used with traditional copper Ethernet cables.
* **SFP Ports:** Used with transceivers to connect various types of fiber optic cables.


* **Scalability:** Switch sizes vary widely (ranging from 4, 8, 24, 48 fixed ports up to modular chassis models supporting hundreds of ports via multiple line cards).

---

## 2. The MAC Address Table

* **Definition:** A dynamic lookup table stored in the memory of a switch that maps specific MAC addresses to specific physical switch ports.
* **Initial State:** When a switch is freshly powered on, its MAC address table is completely **empty**.
* **Core Function:** The switch examines the destination MAC address of an incoming frame, checks this table, and forwards the frame only out of the corresponding port, eliminating the need to broadcast every packet.

---

## 3. Step-by-Step Operation: Learning and Forwarding

When communication starts on a freshly booted switch (e.g., Host A communicating with Host B), the switch executes a two-step process upon receiving a frame:

1. **Source Learning (The Ingress Port):**
* The switch reads the **source MAC address** of the incoming frame.
* It logs that source MAC address in its MAC address table, associating it with the exact physical port the frame just arrived on.


2. **Destination Lookup and Flooding/Forwarding:**
* The switch checks the **destination MAC address** against its table to find the exit port.
* **If the table is empty (Unknown Unicast):** The switch performs **flooding**, sending the frame out of *all* ports except the one it was received on.
* **If the destination is known:** The switch performs selective **switching**, forwarding the frame out of *only* the specific port associated with that destination MAC address.



---

## 4. Handling Local vs. Remote Traffic (Hop-by-Hop Routing)

* **Same Network Segment (Local):**
* If the destination host is on the same local network, the destination MAC address inside the Ethernet frame belongs directly to that target host.


* **Different Network Segment (Remote):**
* If the destination resides on a different network (e.g., reaching across routers to Host Z), the destination MAC address of the very first hop cannot be the remote host.
* Instead, Layer 2 encapsulates the frame using the **MAC address of the default gateway** (router interface) so the switch can deliver it to the router, which then handles subsequent routing hops.



<br>

<br>

---

---

