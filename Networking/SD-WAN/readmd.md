
# SD-WAN
- Software Defined Wide Area Network
- Branch offices to a Datacenter
- Remote sites to headquaters
- users to cloud services
- Traditional WANs were build using private circuits, especially MPLS.

---

# Cisco SD-WAN terms:
- vManage
- vSmart
- vBond
- WAN Edge routers
- OMP
- TLOCs
- Colors
- VPNs
- VRFs
- Centralized Policies


---


- SD-WAN creates a secure overlay network over one or more underlay transport network.
- `Underlay`: The `real` connectivity underneath, which includes MPLS, broadband internet, 5G, and other transport technologies.
- `Overlay`: The logical SD-WAN fabric build on top of these transports.
- SD-WAN Fabric: the virtual network formed by all SD-WAN devices, controllers, secure tunnels and policies that work together to connect sites and applications.
- SD-WAN allows us to think in terms of a managed WAN fabric.

---

- User traffic does not pass through the central controller
- The controller instructs SD-WAN infrastructure to apply policies
- `Control plane traffic`: signaling used to instruct SD-WAN infrastructure on how to behave and how to treat traffic.
- `NOTE`: User traffic still flows between edge devices.

- Question: How the policies get passed to these SD-WAN's different devices?

---
















# Ref Link:
[sd-wan-youtube-link](https://www.youtube.com/watch?v=vVXu5SWfwvE&list=PLZnlAkYyiRMk)
