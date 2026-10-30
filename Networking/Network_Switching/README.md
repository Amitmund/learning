# Layer2 Network Switching

[Network-switching](https://www.youtube.com/watch?v=VYukAH86d2I&list=PLmVr8r1kmMm3HrwOC3beb96JjrBh46AIt)



# Introduction to Network Switching | Layer 2 Fundamentals Explained

**Source:** [Introduction to Network Switching | Layer 2 Fundamentals Explained](http://www.youtube.com/watch?v=VYukAH86d2I)

**Channel:** telecomTech

<br>

<br>

---

---

<br>

<br>


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

<br>

<br>



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

<br>

<br>


# Introduction to Ethernet | CCNA Layer 2 Basics

**Source:** [Introduction to Ethernet | CCNA Layer 2 Basics](http://www.youtube.com/watch?v=BaC80OGlaTg)
**Channel:** telecomTech

---

## 1. Overview and History of Ethernet

* **Dominant Technology:** Ethernet is the dominant technology functioning at Layer 2 (Data Link Layer) for virtually all modern network switches.
* **Origins:** Created on May 22, 1973, connecting two computers via coaxial cable at 2.94 Mbps.
* **IEEE Standards:** Adopted in the early 1980s by the IEEE under the standard **IEEE 802.3**.

---

## 2. Structure of the Ethernet Frame

At the core of Ethernet is the Ethernet frame, which encapsulates Layer 3 IP packets as its payload and wraps them with a header and trailer.

### Header Fields:

1. **Destination MAC Address:** The physical address of the intended recipient (or next-hop router) on the local network segment.
2. **Source MAC Address:** The physical address of the sending device.
3. **EtherType (or Length Field):**
* Identifies the upper-layer network protocol contained in the payload (e.g., IPv4 or IPv6).
* Alternatively used to indicate the length of the payload in bytes/octets.



### Preamble and Start of Frame Delimiter (SFD):

* **Preamble (7 Bytes / 56 Bits):** Consists of alternating ones and zeros, used to help receiving devices synchronize their clocks with transmitters at the bit level.
* **Start of Frame Delimiter (SFD):** Indicates the exact start of the frame so the receiver can begin interpreting the header bits.

### Trailer Fields:

* **Frame Check Sequence (FCS):** A 4-byte field containing a Cyclic Redundancy Check (CRC) value computed from the frame's bits.
* **Error Detection:** The receiver runs the same algorithm; if the computed value doesn't match the FCS value, the frame is deemed corrupted and **dropped**. Ethernet detects errors at the physical level but relies on upper layers for error correction.



---

## 3. MAC Addresses in Ethernet

* **Format & Structure:** 48-bit physical addresses typically represented in hexadecimal for humans, but handled in binary by devices.
* **Factory Assignment:** Hardwired directly into network interface cards (NICs) at the factory with unique identifiers to prevent duplication on a network segment.
* **Universal Scope:** Found on all network devices (PCs, printers, cameras, wireless access points) utilizing Ethernet or Wi-Fi to enable local Layer 2 identification and switching.

---

## 4. Optional Fields: VLAN Tags (IEEE 802.1Q)

* **Location:** Inserted between the Source MAC address and the EtherType field.
* **Contents:** Contains VLAN ID tags and Quality of Service (QoS) information.
* **Usage:** Primarily utilized on trunk links between switches to manage segmented traffic and prioritize data flows.




<br>

<br>

---

---

<br>

<br>


# What Is a MAC Address? | Ethernet & Layer 2 Simply Explained!

**Source:** [What Is a MAC Address? | Ethernet & Layer 2 Simply Explained!](http://www.youtube.com/watch?v=7CvW0zmZT_g)
**Channel:** telecomTech

---

## 1. Overview and Core Uses of MAC Addresses

* **Definition:** A 48-bit unique value assigned to every network device supporting Ethernet and Wi-Fi standards.
* **Key Functions in Layer 2:**
* **MAC Address Learning:** Populates the switch MAC address table for proper frame forwarding.
* **ARP (Address Resolution Protocol):** Resolves MAC addresses from destination IP addresses.
* **Port Security & Filtering:** Allows or blocks network devices based on their MAC addresses.
* **Spanning Tree Protocol (STP):** Utilizes MAC addresses in its operation to prevent Layer 2 loops.
* **Wi-Fi Association:** Used for client and access point identification.



---

## 2. Structure and Notation of MAC Addresses

* **Format:** Composed of 48 bits, read in binary by devices, but represented in hexadecimal for humans.
* **Common Notation Styles:**
* **Cisco:** Three sets of four hex digits separated by dots (e.g., `aabb.ccdd.eeff`).
* **Windows:** Six groups of two hex digits separated by hyphens (e.g., `aa-bb-cc-dd-ee-ff`).
* **Linux / macOS:** Six groups of two hex digits separated by colons (e.g., `aa:bb:cc:dd:ee:ff`).



---

## 3. Assignment: OUI and Manufacturer Unique Identification

* **Globally Administered Addresses (Burned-In):** Hardwired into the non-volatile memory of network interfaces by manufacturers. Assigned per interface, not per device.
* **IEEE Breakdown (48 bits):**
* **First 24 Bits (OUI - Organizationally Unique Identifier):** Identifies the vendor/manufacturer (e.g., Cisco, Intel, Apple). Allows tools to determine the manufacturer from the MAC address.
* **Last 24 Bits:** Assigned uniquely by the manufacturer for each individual interface, ensuring global uniqueness.



---

## 4. Software Modification, Virtual MACs, and the U/L Bit

* **MAC Spoofing / Overriding:** While burned into hardware, operating systems can override the active MAC address in memory for legitimate or malicious purposes.
* **Virtual Devices & LAA (Locally Administered Addresses):**
* Virtual machines and containers generate virtual MAC addresses via hypervisors.
* **U/L Bit (Universal/Local Bit):** The second least significant bit of the first byte of the MAC address.
* If **0**: Universally administered (factory assigned).
* If **1**: Locally administered (LAA / software or administrator generated).


<br>

<br>

---

---

<br>

<br>


When you create a virtual interface (such as a Docker bridge, a KVM/QEMU virtual machine interface, a Linux `macvlan`, or a VLAN sub-interface), the operating system or hypervisor generates a MAC address for it.

To prevent network collisions and conflicts, virtual interfaces follow specific allocation methods:

---

### 1. Locally Administered Addresses (LAAs) and the U/L Bit

Because virtual interfaces are created via software rather than burned into physical silicon by a hardware manufacturer, they use **Locally Administered Addresses**.

* **The U/L Bit Trick:** The hypervisor or OS sets the **Universal/Local (U/L) bit** (the second least significant bit of the first byte of the MAC address) to **1**.
* This signals to any physical or virtual switch on the network that the MAC address is software-generated, locally managed, and not tied to a physical factory registry.

---

### 2. How Different Platforms Generate Unique MACs

* **Linux Kernel (Bridge / Tap / Macvlan):**
* When you create a virtual interface (like a Linux bridge or a dummy interface), the kernel automatically generates a random MAC address.
* It starts with a locally administered prefix (commonly `52:54:00:` for QEMU/KVM virtual machines, or locally randomized bytes with the U/L bit flipped to 1) to ensure it doesn't clash with physical network cards.


* **Docker / Container Runtimes:**
* When Docker creates virtual Ethernet (`veth`) pairs for containers, it allocates MAC addresses sequentially or pseudo-randomly from a private range, ensuring uniqueness within that host's bridge network (e.g., the `docker0` bridge).


* **Hypervisors (VMware, Proxmox, KVM):**
* **Proxmox / KVM:** Generates virtual MAC addresses using the prefix `52:54:00:` followed by three randomly generated bytes (e.g., `52:54:00:12:34:56`). Because the space provides over 16 million combinations per prefix, the chance of a collision on a single host or local network is extremely low.
* **VMware ESXi:** Generates MAC addresses based on a combination of a VMware-assigned OUI prefix (like `00:0c:29` or `00:50:56`) and a hash of the virtual machine's UUID and vCenter identifier.



---

### 3. Manual Assignment

If you are managing your own Linux servers or network namespaces, you don't have to rely on automatic generation. You can explicitly assign a unique MAC address when creating the interface using tools like `iproute2`:

```bash
# Create a dummy interface and assign a custom MAC with the U/L bit set
sudo ip link add dummy0 type dummy
sudo ip link set dev dummy0 address 52:54:00:de:ad:be
sudo ip link set dev dummy0 up

```

### Summary

Virtual interfaces get unique MAC addresses through **pseudo-random generation using locally administered pools (LAAs)** managed by your hypervisor, container engine, or operating system kernel, explicitly flagged with the **U/L bit set to 1** to denote they are software-defined.


<br>

<br>

---

---

<br>

<br>


# The MAC Address Table Explained | How Ethernet Switches Work

**Source:** [The MAC Address Table Explained | How Ethernet Switches Work](http://www.youtube.com/watch?v=ikUv_IX8ZQc)
**Channel:** telecomTech

---

## 1. Core Purpose of the MAC Address Table

* **Definition:** A memory construct within a network switch that associates host MAC addresses with specific physical switch ports.
* **Function:** Enables switches to correctly forward frames out of the appropriate exit interface rather than broadcasting every packet.

---

## 2. Table Maintenance and Aging Timer

* **Learning Process:** Populated dynamically by reading the **source MAC address** of incoming frames and binding it to the ingress port.
* **Aging Timer (Default):** Set to **300 seconds (5 minutes)** on Cisco switches (values may vary slightly by vendor).
* **Why It Exists:** Switches have finite memory. The aging timer automatically flushes out entries for devices that have disconnected or stopped transmitting (crucial in high-churn environments like wireless APs connected to switches) to prevent table overflow and performance degradation.

---

## 3. Multi-Port Mappings and MAC Flapping

* **Many-to-One Mapping:** Multiple MAC addresses can be associated with a single port (e.g., when an access point, hub, or downstream switch connects multiple hosts to a single uplink port).
* **One-to-Many Restriction (Illegal):** A single MAC address *cannot* map to multiple switch ports.
* **MAC Flapping:** If a MAC address is suddenly learned on a new port, it is deleted from the old port and reassigned. If it continuously bounces between ports, it is called **MAC flapping**, which indicates a misconfiguration or loop and causes unpredictable behavior.

---

## 4. CAM (Content Addressable Memory) Hardware Lookup

* **Why CAM is Used:** Traditional software-based searches examine entries one by one (taking multiple CPU cycles, slowing down as tables grow).
* **How CAM Works:** A specialized hardware memory type that compares the search value (destination MAC address) against *all stored entries simultaneously in parallel*.
* **Line-Rate Performance:** Lookup time remains constant, taking only **one CPU cycle**, allowing switches to forward frames at line rate with extremely low latency.

---

## 5. Integration with VLANs

* **VLAN Column:** MAC address tables also track which VLAN each MAC address belongs to.
* **Scope & Isolation:** Because VLANs create separate layer 2 broadcast domains, lookups and unknown unicast flooding are strictly scoped within the matching VLAN, preventing data leaks across network segments.


<br>

<br>

---

---

<br>

<br>


