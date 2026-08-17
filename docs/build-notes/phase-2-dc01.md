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

- [ ] Windows Server installed
- [ ] Server renamed to DC01
- [ ] Static IP configured
- [ ] Internet connectivity verified
- [ ] AD DS installed
- [ ] DNS installed
- [ ] Forest created
- [ ] Domain created

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
