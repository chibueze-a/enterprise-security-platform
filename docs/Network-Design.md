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
