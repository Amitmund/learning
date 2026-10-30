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
