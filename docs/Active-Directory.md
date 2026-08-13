# Active Directory Design

## Business

Apex Trading Group

Industry

Algorithmic Trading

Employees

Approximately 50

Location

New York

## Active Directory Goals

Provide centralized authentication.

Implement least privilege.

Support enterprise security monitoring.

Provide identity infrastructure for future attack simulations.

Support Group Policy.

Support enterprise logging.

## Domain Name

corp.apextrading.com

## Domain Controller

DC01

IP

10.10.20.10

Operating System

Windows Server 2025

## Planned Organizational Units

Corporate

Trading

Engineering

Cybersecurity

IT

Finance

Human Resources

Servers

Workstations

Service Accounts

## Planned Security Groups

IT Administrators

Cybersecurity Team

Trading Users

Engineering Users

Finance Users

HR Users

## Domain Controller Design

### Hostname

DC01

### Virtual Machine

ESP-DC01

### Purpose

Primary Domain Controller

DNS Server

Kerberos Authentication

LDAP Directory

Group Policy

### Network

Server Network

### Static Address

IP Address:
10.10.20.10

Subnet Mask:
255.255.255.0

Gateway:
10.10.20.1

Preferred DNS:
10.10.20.10

### Security Considerations

The Domain Controller is the trust anchor for the Active Directory forest.
It will be hardened and monitored because compromise of this server could
lead to complete domain compromise.
