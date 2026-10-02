# Phase 2: Domain Controller (DC01)

## Objective

Build the first Domain Controller for Apex Trading Group.

## Planned Configuration

Virtual Machine Name:
ESP-DC01

Hostname:
DC01

Operating System:
Windows Server 2025 Standard Evaluation

Network:
VMnet3 (Server Network)

Static IP:
10.10.20.10

Subnet Mask:
255.255.255.0

Gateway:
10.10.20.1

Preferred DNS:
10.10.20.10

Roles to Install:

- Active Directory Domain Services
- DNS Server

Validation Checklist

[x] Windows Server 2025 installed
[x] VMware Tools installed
[x] Hostname DC01
[x] Static IP 10.10.20.10/24
[x] Gateway 10.10.20.1
[x] pfSense SERVER policy configured
[x] Gateway connectivity
[x] Internet IP connectivity
[x] Pre-AD recovery snapshot
[ ] DNS Server
[ ] AD DS
[ ] corp.apextrading.com forest

### SERVER Gateway Connectivity

After configuring DC01 with the static address 10.10.20.10/24,
the server could not ping its pfSense gateway at 10.10.20.1.

#### Investigation

1. Verified DC01 had the intended static IPv4 configuration.
2. Verified DC01 was connected to VMware VMnet3.
3. Verified pfSense OPT1/em2 was configured as 10.10.20.1/24.
4. Checked the ARP table on DC01 after attempting to reach the
   gateway.
5. DC01 successfully resolved 10.10.20.1 to a MAC address,
   demonstrating Layer 2 connectivity between DC01 and pfSense.
6. Investigated pfSense policy rather than changing the VMware
   network or Windows configuration.
7. Configured explicit SERVER interface firewall policy.
8. Retested connectivity.

#### Result

DC01 successfully reached:

- 10.10.20.1 (pfSense SERVER gateway)
- 1.1.1.1 (external Internet address)

Both tests completed with 0% packet loss.

#### Lesson Learned

Successful ARP resolution does not imply that higher-layer traffic
such as ICMP will be permitted. Layer 2 connectivity was functioning,
while pfSense's firewall policy controlled the IPv4 traffic.

Troubleshooting was performed progressively rather than disabling
security controls or making unrelated configuration changes.


## Active Directory Deployment

### Forest

corp.apextrading.com

### Forest Root Domain

corp.apextrading.com

### Domain Controller

DC01

### Domain Controller Roles

- Active Directory Domain Services
- DNS Server
- Global Catalog

### Directory Services

LDAP:
Enabled through AD DS

Kerberos:
Domain authentication protocol

DNS:
AD-integrated DNS

SYSVOL:
Created during Domain Controller promotion

### Validation

-  AD DS role installed
-  DNS Server role installed
-  DC01 promoted successfully
-  corp.apextrading.com created
-  Domain Administrator login successful
-  Forward lookup zone exists
-  _msdcs zone exists
-  DC01 DNS record resolves
-  LDAP SRV records resolve
-  Kerberos SRV records resolve
-  SYSVOL share exists
-  NETLOGON share exists
-  dcdiag completed
-  External DNS resolution tested

Why we took these steps
Installing AD DS and promoting a server are separate operations because installing the role merely provides the software; promotion gives the server responsibility for a particular directory domain.
We installed DNS alongside AD because Active Directory relies heavily on DNS for service discovery. Clients don't need hard-coded knowledge of which machine is a Domain Controller—they can discover services through DNS records.
We validated LDAP and Kerberos SRV records because merely seeing "DNS Server running" doesn't prove that Active Directory service discovery is functioning.
We also kept DC01 pointed at its AD DNS infrastructure rather than switching it to a public DNS resolver. Later, external queries can be forwarded appropriately while internal AD queries remain authoritative.
And we ran dcdiag because good infrastructure engineering means validating the service, not merely trusting that an installation wizard reached 100%.
