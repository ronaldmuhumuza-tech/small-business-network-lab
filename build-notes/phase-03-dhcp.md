# Phase 03 – DHCP Configuration

## Objective

The objective of this phase is to automate IP address assignment within the network by configuring the router as a DHCP server.

This removes the need for manual IP configuration on end devices and reflects how most real-world networks operate.

---

## DHCP Configuration Overview

Dynamic Host Configuration Protocol (DHCP) was implemented on R1 to dynamically assign IP addresses to hosts within each VLAN.

Separate DHCP pools were created for each VLAN to ensure proper segmentation and address management.

---

## DHCP Pools

A DHCP pool was configured for each VLAN using the following structure:

* Network address
* Default gateway (router subinterface)
* Address range (excluding reserved addresses)

### VLAN 10 – Management

* Network: 192.168.10.0/24
* Default Gateway: 192.168.10.1

### VLAN 20 – Sales

* Network: 192.168.20.0/24
* Default Gateway: 192.168.20.1

### VLAN 30 – IT

* Network: 192.168.30.0/24
* Default Gateway: 192.168.30.1

### VLAN 40 – Guest

* Network: 192.168.40.0/24
* Default Gateway: 192.168.40.1

To prevent conflicts, gateway addresses were excluded from DHCP allocation.

Relevant configuration can be found in:

* R1: `configs/R1.txt`

---

## Host Configuration

All VPCS devices were reconfigured to obtain IP addresses dynamically using DHCP.

This replaced the static IP configuration used in Phase 2.

---

## Verification

The following checks were performed to verify DHCP functionality:

* `show ip dhcp binding` (R1)
* `show ip dhcp pool` (R1)
* `show ip` (VPCS)

Additionally, connectivity tests were performed to confirm that:

* Hosts received correct IP addresses
* Default gateways were assigned correctly
* Inter-VLAN communication remained functional

Screenshots of verification outputs are available in the `/screenshots` directory.

---

## Notes

DHCP simplifies network management by automating IP address allocation and reducing the risk of configuration errors.

At this stage, all VLANs can communicate freely, and address assignment is fully dynamic. Security controls will be introduced in the next phase using ACLs.
