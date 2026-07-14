Microsoft Azure Cloud Security Workshop Notes

SSN College of Engineering

Workshop Account

Azure Account:

ssnteam3@ksivvagmail.onmicrosoft.com
What is a Virtual Machine (VM)?

A Virtual Machine (VM) is a software-based computer running in Microsoft's cloud.

It behaves like a real computer with:

CPU
RAM
Storage
Operating System
Network

Example:

Your Laptop
      ↓

Azure Data Center

      ↓

Virtual Machine
Ports

A port is a communication endpoint used by applications and services.

A computer has 65,535 TCP/UDP ports.

Different applications listen on different ports.

Examples:

Port	Service	Purpose
22	SSH	Remote login to Linux VM
80	HTTP	Website (without SSL)
443	HTTPS	Secure website
3389	RDP	Remote Desktop for Windows
27017	MongoDB	MongoDB database server
3306	MySQL	MySQL database
1433	SQL Server	Microsoft SQL Server
Port 3389
3389 = Remote Desktop Protocol (RDP)

Purpose:

Used to remotely access a Windows Virtual Machine.

Laptop

↓

Internet

↓

Azure VM

↓

Windows Desktop
Port 22
22 = SSH

Purpose:

Remote login into Linux machines.

Example

ssh azureuser@Public-IP
Port 443
443 = HTTPS

Purpose

Secure websites.

Example

https://google.com

Uses SSL/TLS encryption.

MongoDB

Default Port

27017

Purpose

Allows applications to connect to MongoDB.

Corporate Firewall

Many organizations block ports like:

22
3389

Reason:

Hackers often attack these ports.

Example:

During the workshop

SSN Wi-Fi blocked RDP (3389).

Using Mobile Hotspot worked.

Azure Storage

A Virtual Machine contains disks.

Two major disks:

Virtual Machine

├── OS Disk
└── Data Disk
OS Disk

Contains

Windows/Linux
Installed software
System files
Boot files

Example

C:
Data Disk

Stores

Database
User files
Documents
Images
Videos
Application data

Usually

D:
Why separate OS Disk and Data Disk?

Imagine

Single Disk

Windows
Database
Documents

If Windows crashes

Format disk

↓

Everything lost

With separate disks

OS Disk

Windows

↓

Corrupted

Delete OS Disk

↓

Create New OS Disk

↓

Attach Existing Data Disk

↓

Database survives

This is why production servers keep application data on a separate disk.

HDD vs SSD
HDD

Hard Disk Drive

Advantages

Cheap
Large storage

Disadvantages

Slow
Mechanical
SSD

Solid State Drive

Advantages

Very Fast
Better performance
Faster boot
Faster database

Disadvantages

More expensive

Azure workshop used

Premium SSD
Disk Encryption

Azure encrypts all managed disks.

Encryption protects data if someone physically steals the storage hardware.

Key Management

Encryption always requires a key.

There are two major types.

Platform Managed Key (PMK)

Azure manages the encryption key.

Customer

↓

Azure

↓

Encryption Key

Advantages

Easy
Default
No management required
Customer Managed Key (CMK)

Customer owns the encryption key.

Usually stored inside

Azure Key Vault

Advantages

Customer controls keys
Can rotate keys
Meets compliance requirements
Example

Healthcare

HIPAA

Banks

Government

Military

These organizations often require Customer Managed Keys (CMK) because they do not want the cloud provider to control encryption keys.

Note: You mentioned "HEPPA"; the correct compliance standard is HIPAA (Health Insurance Portability and Accountability Act).

Encryption

The encryption algorithm may be the same (for example, AES-256).

The difference is who manages the encryption key, not the algorithm itself.

Load Balancer

Purpose

Distribute incoming traffic across multiple servers.

Example

Without Load Balancer

1000 Users

↓

One Server

↓

Server crashes

With Load Balancer

1000 Users

↓

Load Balancer

↓

Server 1

Server 2

Server 3

Benefits

Better performance
High availability
Fault tolerance
Scalability
CIA Triad

The three pillars of Information Security.

Confidentiality

Only authorized users can access data.

Examples

Passwords
Encryption
Access Control
Integrity

Data should not be modified without authorization.

Examples

Hashing
Digital Signatures
Checksums
Availability

Data and services should always be available to legitimate users.

Examples

Backups
Load Balancers
Redundant Servers
Auto Scaling
Auto Shutdown

Azure can automatically shut down a VM at a specified time.

Benefits

Saves money
Prevents unnecessary resource usage

Example

Working Hours

↓

VM Running

↓

8 PM

↓

VM Automatically Stops
Azure Resources Created During the Lab

When you created your VM, Azure automatically provisioned several resources:

Resource Group (Team3ssn)
│
├── Virtual Machine (vm3)
├── OS Disk (Premium SSD)
├── Virtual Network (vm3-vnet)
├── Subnet
├── Network Interface (NIC)
├── Public IP Address (vm3-ip)
├── Network Security Group (vm3-nsg)
└── Auto Shutdown Schedule
Key Takeaways
A Virtual Machine is a cloud-hosted computer.
Ports identify services (e.g., 22 for SSH, 3389 for RDP, 443 for HTTPS, 27017 for MongoDB).
Organizations often block RDP/SSH on corporate networks for security.
Keep OS disks and data disks separate to simplify recovery and protect data.
Premium SSDs provide better performance than HDDs.
Azure encrypts managed disks by default.
Platform Managed Keys are convenient; Customer Managed Keys are used when organizations require full control over encryption keys.
Load Balancers distribute traffic and improve availability.
The CIA Triad—Confidentiality, Integrity, and Availability—is a fundamental security model.
Auto Shutdown helps reduce cloud costs by stopping VMs when they are not in use.
