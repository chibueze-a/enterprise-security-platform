# Network Design

## Objective

Design a segmented virtual enterprise network that separates
systems according to their function and trust level while allowing
only the communication required for business and security operations.

## Design Principles

- Network segmentation
- Least privilege
- Explicit trust boundaries
- Centralized security monitoring
- Controlled administrative access
- Observable network activity

## Planned Security Zones

### User Network
Employee workstations and other user endpoints.

### Server Network
Enterprise services such as Active Directory and Linux servers.

### Security Network
Security monitoring and management infrastructure such as
Splunk and Wazuh.

### Attack Network
Systems used to safely simulate adversary activity against
the lab environment.

## IP Addressing Plan

| Zone | Subnet | Gateway | Purpose |
|------|--------|---------|---------|
| User | 10.10.10.0/24 | 10.10.10.1 | Employee endpoints |
| Server | 10.10.20.0/24 | 10.10.20.1 | Enterprise servers and identity services |
| Security | 10.10.30.0/24 | 10.10.30.1 | Monitoring and security infrastructure |
| Attack | 10.10.40.0/24 | 10.10.40.1 | Controlled adversary simulation |

## Planned Systems

### User Network

Windows Workstation

IP: 10.10.10.10

### Server Network

Domain Controller

IP: 10.10.20.10

Linux Server

IP: 10.10.20.20

### Security Network

Wazuh Server

IP: 10.10.30.10

Splunk Server

IP: 10.10.30.20

### Attack Network

Kali Linux

IP: 10.10.40.10

## Routing

pfSense will operate as the default gateway for each internal
network and will control routing between security zones.

Inter-zone communication will be denied or permitted according
to explicit firewall policy rather than allowing unrestricted
communication between all systems.
