# ADR-002: Use VMware Workstation Pro as the Lab Hypervisor

## Status

Accepted

## Context

The project requires a desktop hypervisor capable of running
Windows, Linux, pfSense, and security monitoring systems while
supporting multiple isolated virtual networks.

The original implementation plan considered VirtualBox. VMware
Workstation Pro is already selected for the host system and
provides the networking and snapshot capabilities required by
the design.

## Decision

VMware Workstation Pro will be used as the virtualization platform.

Custom VMnet networks will represent the User, Server, Security,
and Attack zones. The default VMware NAT network will provide the
pfSense WAN connection.

## Advantages

- Supports multiple custom isolated virtual networks
- Supports VM snapshots and cloning
- Provides a graphical Virtual Network Editor
- Supports Windows, Linux, and pfSense guests
- Familiar enterprise virtualization concepts
- Already selected for the host environment

## Tradeoffs

- VMware-specific configuration reduces portability
- Virtual networking adds a layer of troubleshooting complexity
- Host resource limits restrict how many VMs can run simultaneously
- Some steps differ from equivalent VirtualBox implementations

## Alternatives Considered

### Oracle VirtualBox

Meets the general project requirements and is free, but was not
selected because VMware Workstation Pro will be used on the host.

### Microsoft Hyper-V

Integrated with Windows but introduces different virtual-switch
management and may create compatibility considerations with other
desktop hypervisors.

## Outcome

The logical architecture remains independent of the hypervisor.
VMware Workstation Pro is the implementation mechanism, while
network segmentation, routing, and least privilege remain the
underlying design principles.
