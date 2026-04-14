# High-Level Design

This network is designed to simulate a small business environment where different departments are logically separated while still allowing controlled communication.

The network is divided into the following segments:

- Management  
- Sales  
- IT  
- Guest  

Each segment is assigned its own VLAN to maintain separation and improve organisation.

Inter-VLAN communication is handled centrally to ensure that traffic between departments can be controlled and monitored.