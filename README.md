# Project NetCore: Multi-VLAN Network Design and Implementation

## Documentation

Additional design details are available in the [docs/](docs) directory.

## **Overview**

This project is a personal learning initiative focused on understanding how small business networks are structured and managed in practice.

Having developed a solid foundation in networking and data infrastructure concepts during my CCNA studies, I wanted to continue strengthening my understanding of how these ideas come together in a more realistic business setting.

In this project, I have used a simulated environment to model a small business office network and explore how it can be segmented, automated, and controlled using core networking principles. This work forms part of a hands-on lab project I have named *Project NetCore*.


## **Objectives**

The aim of this project is to:
* Explore how network segmentation is applied in practice
* Understand inter-VLAN communication within a structured network
* Implement dynamic IP address assignment using DHCP
* Introduce basic access control between network segments

## **Business Scenario**

A small business operating from a single office has grown to include multiple teams working on the same network.

Initially, all devices were connected without much structure. As the business expanded, it became harder to manage how devices were organised and how different parts of the network interacted.

This project explores how a simple redesign can introduce structure, improve organisation, and allow more controlled communication between departments.

## **Tools and Technologies Used**

### **EVE-NG Community**
Network simulation environment. While exploring different lab environments, I also considered [PNETLab](https://pnetlab.com/) as an alternative open-source platform. 

For this project, I chose to work with [EVE-NG Community](https://www.eve-ng.net/) but PNETLab appeared like an equalliy useable solution to study networking devices and a range of networking features. Other tools such as Cisco Packet Tracer, GNS3, and Cisco Modeling Labs (CML) were considered during the early stages of the project.

### **VMWare Worstation**
Used to host the EVE-NG lab environment. The EVE-NG Community lab environment is hosted within VMware Workstation, running on an Ubuntu 22.04 virtual machine. This layered setup allows network devices such as routers and switches to be emulated within a controlled environment, making it possible to build, modify, and test network configurations safely. It also mirrors how virtualised lab environments are commonly used to explore and validate network designs before deployment.

### **Cisco IOSv / Cisco IOSvL2**
Virtual routing and switching devices.

### **VPCS**
End-device simulation for testing.

### **MobaXterm Personal Edition**
Terminal access to devices.

### **draw.io**
Topology diagram creation.

### **Visual Studio Code**
Used to write and edit Markdown documentation.

### **GitHub**
Project documentation and version control.

## **High-Level Design**

The network is organised into separate logical groups representing different departments:

* Management
* Sales
* IT
* Guest

Each department is placed in its own VLAN to maintain separation, while a central router allows controlled communication between them.

Basic access control is introduced to limit unnecessary interaction between departments.

## **Low-Level Design Summary**

### VLAN & IP Scheme 

#### Design rationale
The addressing scheme was designed so that each VLAN matches a corresponding subnet (e.g. VLAN 10 -> 192.168.10.0/24). This makes the network easier to read, troubleshoot, and manage, as IP addresses can be quickly linked to their respective departments.

A /24 subnet was chosen for each VLAN to keep the design simple while still providing enough address space for a small business environment.

Private addressing (192.168.x.x) was used in line with common practice for internal networks, avoiding unnecessary complexity at this stage of the design.

#### VLAN & IP Allocation

| VLAN | Department | Subnet          | Gateway      |
| ---- | ---------- | --------------- | ------------ |
| 10   | Management | 192.168.10.0/24 | 192.168.10.1 |
| 20   | Sales      | 192.168.20.0/24 | 192.168.20.1 |
| 30   | IT         | 192.168.30.0/24 | 192.168.30.1 |
| 40   | Guest      | 192.168.40.0/24 | 192.168.40.1 |

Further design details can be found in:

- [High-Level Design](docs/high-level-design.md)
- [Low-Level Design](docs/low-level-design.md)

## **Topology**

A visual representation of the network:

<p align="center">
  <img src="topology/topology-layout.png" alt="Network Topology" width="300"/>
</p>

## **Implementation Approach**

The network is being built in stages for structure and to reflect the core tasks and activities:

1. VLAN creation and device assignment: this phase focuses on establishing logical segmentation by assigning devices to departiment-specific VLANS.
2. Trunk configuration between switches: The trunk links are configured to allow VLAN traffic to travel between switches and to and from the router.
3. Inter-VLAN routing (router-on-a-stick): To allow communication between departments in their logically separate VLANS
4. DHCP configuration: For dynamic assignment of IP addresses to automate IP addressing of hosts.
5. Security and management features: To provide network controls and hardening features including ACLs (inter-VLAN traffic control), secure remote management using SSH, and additional Layer 2 protections such as DHCP Snooping and Dynamic ARP Inspection.

## **Configurations**

Device configurations are stored in:

- [configs/](configs/)

## **Build Notes**

Additional notes for each stage of the build:

- [build-notes/](build-notes/)

## **Testing Summary**

The network will be tested to confirm functionality and testing will continue every time additional features are introduced:

* Devices receive IP addresses via DHCP
* Connectivity within and across VLANs
* Access restrictions behave as expected

Further testing will be performed to validate:

* Access restrictions implemented using ACLs
* Secure remote management via SSH
* Additional security controls introduced in later phases

Detailed validation results will be documented in the [tests/](tests/) directory.

## **Troubleshooting**

Issues encountered during the build and how they were resolved are documented in the [notes/](notes/) directory.

## **Reflection**
This project provides a practical way to explore how networking concepts translate into real-world scenarios.

Building the network step by step reinforces how structure, automation, and access control contribute to a more manageable environment.

It also highlights the role of underlying Layer 2 mechanisms. This lab has not explored Spanning Tree Protocol, which helps prevent switching loops and maintain stability in this simple network. However STP will become  relevant as the network design grows as redundancy gets introduced.

## **Future Improvements**

Possible enhancements are to be explored in this project:

* Adding a dedicated server VLAN to host internal services
* Implementing Network Address Translation (NAT) for simulated internet access
* Introducing centralised authentication using RADIUS or TACACS+ for device access control
* Exploring redundancy and failover concepts (e.g. HSRP, multiple links)
