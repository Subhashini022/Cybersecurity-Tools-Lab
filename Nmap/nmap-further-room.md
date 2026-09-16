# Nmap – Further Nmap

## Overview

This document contains my hands-on learning and practice from the TryHackMe **Further Nmap** room.

Nmap (Network Mapper) is a network scanning tool used to discover hosts, identify open ports, detect services, and perform different types of network scans.

**Platform:** TryHackMe  
**Room:** Further Nmap  
**Focus:** Nmap scanning, port states, scan types, NSE scripts, and practical enumeration

---

## What I Learned

During this room, I learned:

- TCP Connect scans
- TCP SYN scans
- UDP scans
- NULL scans
- FIN scans
- Xmas scans
- Ping sweeps
- Port states
- Nmap timing and verbosity options
- NSE (Nmap Scripting Engine)
- NSE script categories
- Searching for installed NSE scripts
- Vulnerability scripts
- FTP anonymous login enumeration
- SMB NSE scripts
- Host discovery and firewall considerations
- Adding random data to packets using `--data-length`

---

## Basic Nmap Scan

A basic Nmap scan can be performed using:

My Lab Scan
nmap 10.49.190.20
Result

The scan identified these open TCP ports:

Port	State	Service
21/tcp	Open	FTP
22/tcp	Open	SSH
53/tcp	Open	DNS
80/tcp	Open	HTTP

Nmap also reported 996 closed TCP ports in the default scan.

Screenshot

TCP Connect Scan

A TCP Connect scan uses the operating system's TCP connection process.

nmap -sT <TARGET-IP>

The TCP connection follows the basic process:

SYN
 ↓
SYN/ACK
 ↓
ACK

A TCP Connect scan completes the TCP handshake.

TCP SYN Scan

A SYN scan is also known as:

Half-open scan
Stealth scan

Nmap command:

nmap -sS <TARGET-IP>

A SYN scan does not complete the full TCP connection.

UDP Scan

UDP scanning can be performed using:

nmap -sU <TARGET-IP>
My Lab Scan
nmap -sU -p 161 10.49.190.20
Result
161/udp  closed  snmp

Port 161 is commonly associated with SNMP.

Screenshot

NULL, FIN and Xmas Scans
NULL Scan
nmap -sN <TARGET-IP>

A NULL scan sends a TCP packet without any flags.

FIN Scan
nmap -sF <TARGET-IP>

A FIN scan sends a packet with the FIN flag.

Xmas Scan
nmap -sX <TARGET-IP>

An Xmas scan uses:

FIN
PSH
URG

These scan types can be useful for testing how a target or firewall responds to unusual TCP packets.

Ping Sweep

A ping sweep is used to discover live hosts in a network.

For a 172.16.x.x network with subnet mask 255.255.0.0, the CIDR notation is /16.

nmap -sn 172.16.0.0/16

-sn performs host discovery without performing a port scan.

Nmap Verbosity

Nmap supports different verbosity levels.

nmap -v <TARGET-IP>

Higher verbosity provides additional information during a scan.

For example:

nmap -vv <TARGET-IP>
Scanning All TCP Ports

To scan all 65,535 TCP ports:

nmap -p- <TARGET-IP>

The -p- option represents ports 1–65535.

Nmap Timing Templates

Nmap provides timing templates from -T0 to -T5.

Option	Timing
-T0	Paranoid
-T1	Sneaky
-T2	Polite
-T3	Normal
-T4	Aggressive
-T5	Insane
Saving Nmap Output
Normal format
nmap -oN scan.txt <TARGET-IP>
XML format
nmap -oX scan.xml <TARGET-IP>
Grepable format
nmap -oG scan.txt <TARGET-IP>
All major formats
nmap -oA scan <TARGET-IP>
Nmap Scripting Engine (NSE)

Nmap includes the Nmap Scripting Engine (NSE), which allows Nmap to use scripts for additional scanning and enumeration.

A specific script can be activated using:

nmap --script <script-name> <TARGET-IP>

Example:

nmap --script http-title <TARGET-IP>
Vulnerability Scripts

All scripts in the vuln category can be run using:

nmap --script vuln <TARGET-IP>

The intrusive category should be used carefully because these scripts can potentially affect or disrupt systems.

Finding NSE Scripts

Nmap stores NSE scripts on Linux in:

/usr/share/nmap/scripts/

Scripts can be searched using:

grep "ftp" /usr/share/nmap/scripts/script.db

Another method is:

ls -l /usr/share/nmap/scripts/*ftp*

SMB scripts can be searched using:

ls -l /usr/share/nmap/scripts/*smb*
SMB OS Discovery

The SMB script I identified was:

smb-os-discovery.nse

This script is used to gather information about the operating system and related details of an SMB server.

FTP Anonymous Login

The ftp-anon NSE script checks whether an FTP server allows anonymous access.

nmap -p 21 --script ftp-anon <TARGET-IP>

The script can also use the optional argument:

ftp-anon.maxlist

This controls the maximum number of files/directories that the script attempts to list.

In the practical task, Nmap was able to successfully log in to the FTP server using anonymous access.

Host Discovery and -Pn

Sometimes a host may not respond to normal host-discovery probes.

Nmap can skip host discovery using:

nmap -Pn <TARGET-IP>

This tells Nmap to treat the target as online and continue with the scan.

Adding Random Data to Packets

The Nmap option:

--data-length <number>

can be used to append random data to packets.

Example:

nmap --data-length 50 <TARGET-IP>
Key Learnings

This room helped me understand that Nmap is more than a basic port scanner.

I learned how to:

Identify open, closed and filtered ports.
Understand TCP connection behavior.
Perform TCP Connect and SYN scans.
Perform UDP scans.
Understand NULL, FIN and Xmas scans.
Perform network host discovery.
Use Nmap verbosity and timing options.
Scan all TCP ports.
Save scan results in different formats.
Use NSE scripts for additional enumeration.
Search for installed NSE scripts.
Use vulnerability-related scripts.
Enumerate FTP anonymous access.
Understand how firewalls can affect Nmap results.
Interpret Nmap output instead of simply running commands.
TryHackMe Completion

I completed the Further Nmap TryHackMe room.

Completed Tasks: 15
Points Earned: 328

Screenshot

Disclaimer

All scans documented here were performed in an authorized TryHackMe lab environment for educational purposes.

I do not scan systems without permission.

Tools Used
Nmap
Nmap Scripting Engine (NSE)
Linux terminal
TryHackMe

```bash
nmap <TARGET-IP>
