# Phase 01: VLAN Configuration

## Objective

The objective of this phase is to implement VLAN-based segmentation within the network. Each department is placed into its own VLAN to improve organisation and prepare for controlled communication in later phases.

## VLAN Creation

VLANs were created on both switches to represent different departments within the network:

* VLAN 10   Management
* VLAN 20   Sales
* VLAN 30   IT
* VLAN 40   Guest

Creating VLANs on both switches ensures consistency across the network and allows VLAN traffic to traverse the trunk link between switches.

Relevant configuration can be found in:

* SW1: [configs/SW1.txt](configs/SW1.txt)
* SW2: [configs/SW2.txt](configs/SW2.txt)

## Port Assignment

Access ports were configured on each switch to assign end devices to their respective VLANs.

### SW1

* G0/0 -> VLAN 10 (PC-MGMT)
* G0/3 -> VLAN 20 (PC-SALES)

### SW2

* G0/2 -> VLAN 30 (PC-IT)
* G0/3 -> VLAN 40 (PC-GUEST)

This ensures that each device is logically grouped according to its department.

Relevant configuration can be found in:

* SW1: [configs/SW1.txt](configs/SW1.txt)
* SW2: [configs/SW2.txt](configs/SW2.txt)

## Trunk Configuration

A trunk link was configured between the two switches to allow traffic from multiple VLANs to pass between them.

* SW1 G0/2 <-> SW2 G0/1
* Encapsulation: 802.1Q
* Allowed VLANs: 10, 20, 30, 40

This allows VLANs configured on one switch to be extended across the network.

Relevant configuration can be found in:

* SW1: [configs/SW1.txt](configs/SW1.txt)
* SW2: [configs/SW2.txt](configs/SW2.txt)

## Verification

The following commands were used to verify the configuration:

* `show vlan brief`
* `show interfaces trunk`

These confirmed that:

* VLANs were successfully created
* Access ports were assigned correctly
* The trunk link was active and carrying the required VLANs

Screenshots of verification outputs are available in the [screenshots/](screenshots/) directory.

## Notes

At this stage, devices in different VLANs are unable to communicate with each other. This is expected behaviour, as inter-VLAN routing has not yet been configured.

This phase establishes the Layer 2 foundation required for implementing routing and additional services in later stages of the project.
