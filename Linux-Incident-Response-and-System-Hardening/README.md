# Linux Incident Response and System Hardening Project

## Project Overview

This project demonstrates practical Linux security and incident response skills through a simulated network breach scenario.

The objective was to prepare a secure workspace for handling potentially malicious files, protect sensitive evidence through appropriate permissions, and configure firewall rules to restrict unauthorized network traffic.

The project was completed in a controlled Kali Linux virtual machine environment.

## Scenario

I acted as the primary responder to a suspected network breach.

Before analyzing potentially malicious files, I needed to:

- Create an organized and isolated workspace
- Secure sensitive investigation data
- Configure appropriate file permissions
- Restrict unauthorized network traffic
- Allow required secure traffic for threat intelligence feeds
- Verify the security configuration

## Objectives

## Objective 1: File System Navigation & Creation

The first objective focused on creating and organizing a secure investigation workspace.

A main directory named "quarantine_zone" was created in the home directory.

Inside "quarantine_zone", three directories were created:

- "pcap_logs"
- "malware_samples"
- "threat_intel"

An empty file named "suspect_ips.txt" was then created inside the "threat_intel" directory and copied into the "pcap_logs" directory.

Directory Structure

quarantine_zone/
├── pcap_logs/
│   └── suspect_ips.txt
├── malware_samples/
└── threat_intel/
    └── suspect_ips.txt

## Commands Used

cd ~
mkdir quarantine_zone
cd quarantine_zone
mkdir pcap_logs malware_samples threat_intel
touch threat_intel/suspect_ips.txt
cp threat_intel/suspect_ips.txt pcap_logs/

## Objective 2: Securing Evidence

The second objective focused on protecting sensitive attacker data using Linux file permissions.

The required permission configuration for "suspect_ips.txt" was:

- Owner: read and write
- Group: read only
- Others: no access

Permission Command

chmod 640 threat_intel/suspect_ips.txt

The expected permission format is:

-rw-r-----

This configuration ensures that the file owner can read and modify the evidence, members of the assigned group can read it, and all other users are denied access.

Group Ownership

The command required to change the group ownership of the "quarantine_zone" directory to "soc_analysts" is:

sudo chgrp soc_analysts ~/quarantine_zone

## Objective 3: Network Isolation & Firewall Configuration

The third objective focused on using UFW (Uncomplicated Firewall) to control incoming network traffic.

The simulated attacker's IP address was:

198.51.100.22

Check Firewall Status

sudo ufw status

Deny Traffic from the Attacker

sudo ufw deny from 198.51.100.22

Allow Secure Threat Intelligence Traffic

Port 443 was allowed for incoming HTTPS traffic required to securely retrieve threat intelligence feeds.

sudo ufw allow 443/tcp

Enable the Firewall

sudo ufw enable

Verify Firewall Rules

sudo ufw status

The final firewall status and active rules were verified after configuration.

## Evidence

Screenshots documenting the practical work are included with the project.

The evidence covers:

## Objective 1 Evidence

- Navigation to the home directory
- Creation of "quarantine_zone"
- Creation of the three required subdirectories
- Creation of "suspect_ips.txt"
- Copying "suspect_ips.txt" into "pcap_logs"

## Objective 2 Evidence

- Permission modification using "chmod"
- Final "ls -l" output showing the required permissions
- Group ownership command for "soc_analysts"

## Objective 3 Evidence

- Firewall status command
- Firewall rule denying "198.51.100.22"
- Firewall rule allowing TCP port 443
- Firewall activation
- Final active firewall rules

## Security Concepts Demonstrated

This project demonstrates practical understanding of:

- Linux file system navigation
- Directory and file creation
- Evidence handling
- Linux file permissions
- Access control
- Group ownership
- Least privilege
- Firewall configuration
- Network isolation
- Attack-surface reduction
- Security verification

## Key Security Principles

Least Privilege

File permissions were configured so that users only receive the level of access required to perform their role.

Evidence Protection

Restricting access to "suspect_ips.txt" helps prevent unauthorized users from modifying or accessing sensitive attacker-related information.

Network Isolation

The firewall configuration demonstrates how incoming network traffic can be restricted while allowing necessary secure communications.

## Tools Used

- Kali Linux
- Linux Terminal
- Bash
- UFW Firewall
- VirtualBox

## Lessons Learned

This project provided practical experience with Linux file system management, permissions, group ownership, and firewall configuration.

It also demonstrated how basic Linux security controls can be used during the preparation stage of an incident response investigation.

## Conclusion

A properly secured investigation environment helps protect evidence and reduce the risk of further unauthorized access during an incident.

Through this project, I practiced applying Linux security controls to a simulated network breach scenario, including evidence organization, permission management, and firewall-based network isolation.

## Disclaimer

This project was completed in a controlled lab environment for educational and cybersecurity training purposes.
