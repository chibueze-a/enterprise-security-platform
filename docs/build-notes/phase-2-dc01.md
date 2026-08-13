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
