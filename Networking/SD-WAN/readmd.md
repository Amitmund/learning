
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

---

### Question: How the policies get passed to these SD-WAN's different devices?

In an SD-WAN architecture, policies are decoupled from individual devices and managed through a centralized framework. Instead of logging into routers one-by-one via CLI, network administrators define policies in a **Centralized Management Dashboard**, which then pushes them to edge devices using automated protocols and overlay control planes.

---

### **1. The Policy Distribution Workflow**

The pipeline of how a policy flows from an administrator's screen down to the physical or virtual edge devices typically follows these stages:

1. **Creation & Compilation (Management Plane):**
An administrator builds or modifies policies using a GUI wizard or API templates (such as application-aware routing rules, security firewalls, or QoS priorities). The management system compiles these high-level intents into structured data models (like JSON or XML payloads).
2. **Secure Transport (NETCONF / RESTCONF):**
The management system pushes these configuration payloads securely down to the target controllers or edge nodes over encrypted channels using standard, programmatic network management protocols like **NETCONF** (running over TLS/SSH) or **REST APIs**.
3. **Control Plane Distribution (OMP / BGP):**
For global routing and traffic-steering policies, the controller doesn't always touch every single edge node directly. Instead, it pushes the control policy to a centralized control cluster (e.g., vSmart in Cisco Viptela or Nuage VSC), which then dynamically advertises the updated routing paths, TLOCs (Transport Locators), and service chains to the edge devices using an overlay protocol like **OMP (Overlay Management Protocol)** or internal **BGP**.
4. **Local Enforcement (Data Plane):**
The Edge device receives the policy instructions, compiles them into its local forwarding tables, packet filters (`nftables`/`iptables`), or QoS queues, and enforces them directly on live traffic passing through the data plane.

---

### **2. Centralized vs. Localized Policy Distribution**

Depending on what the policy is trying to achieve, SD-WAN splits distribution into two categories:

* **Centralized Policies (Pushed from Controller/Orchestrator):**
* *What they control:* Inter-site routing, topology definitions, application-aware path selection across public/private transports, and global security rules.
* *How they pass:* Configured once on the manager, pushed to the controller via **NETCONF**, and distributed via the overlay routing protocol (**OMP/BGP**).


* **Localized Policies (Pushed via Device Templates or CLI):**
* *What they control:* Site-specific interface configurations, local branch NAT rules, local DHCP services, or local interface QoS queue weights.
* *How they pass:* Pushed as reusable **Device Templates** directly from the orchestrator to specific edge nodes using NETCONF, or applied locally.

---

### SD-WAN control plane's Application Aware Routing:

- Applicaiton
- user/role
- policy
- Time/Location
  
- Traditional Routing makes decisions based on prefixes, metrics, Administrated Distanced (ADs), next hops and routing protocols.
- SD-WAN can make routing decisions based on the type of application and the current quality of the available path.

- Applications and Destinations:
  - Voice (Low Latency)
  - SAAS (Business Apps)
  - File Transfer (Bulk / Non-Critical)
  - Guest Internet (Direct Internet)
  - Data Center (Private Resources)
  - Security Services (Secure Inspection)
 
- So, SD-WAN makes decisions based on what the application needs and how well each path is performing.
- SD-WAN allows organizaitons to use multiple WAN links more intelligently and effciently.

NOTE:

- SD-WAN does not make other network technologies obsolete.
- It doesn't make routing, IPsec, QoS and troubleshooting disappear.


---

### Cisco-Specific terms for SD-WAN:

- `vManage/SD-WAN manager` - used for management, configuration, monitoring and policy creation.
- `vSmart/SD-WAN controller` - part of the control plane which help distribute routing and policy information across the fabric.
- `vBond/SD-WAN validator` - helps with the initial orchestration and onboarding of devices into the fabric.
- `WAN Edge routes` - devices that sit at the network edge location, and forward traffic.
- `Overlay Management Protocol (OMP)` - Cisco control protocol used to exchange routing, transport and policy-related info.
- Transport Locators (TLOCs) - help identify the transport attachment points used by WAN edge routes to build the overlay.

  
---

### What we will learn on this:

- Why does SD-WAN exist? What problems does it solve?
- What is SD-WAN and how does it differ from traditional WANs?
- Underlay vs Overlay, what's the difference?
- SD-WAN architecture, including management and control planes.
- How do SD-WAN devices join the fabric?
- OMP, application-aware routing, centralized policies, and segmentation using `VRFs` and `VPNs`
- Direct internet access, SaaS optimization, security, SASE, QoS, troubleshooting, real-world design and the skills you need to learn.


---











# Ref Link:
[sd-wan-youtube-link](https://www.youtube.com/watch?v=vVXu5SWfwvE&list=PLZnlAkYyiRMk)
