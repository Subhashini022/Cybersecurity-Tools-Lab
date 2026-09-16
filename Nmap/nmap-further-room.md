# Nmap - Further Nmap

## Overview

I completed the TryHackMe **Further Nmap** room to learn practical Nmap scanning and enumeration.

**Platform:** TryHackMe  
**Room:** Further Nmap

## What I Learned

- TCP Connect scans
- TCP SYN scans
- UDP scans
- NULL scans
- FIN scans
- Xmas scans
- Ping sweeps
- Port states
- Nmap timing options
- Nmap verbosity
- NSE scripts
- NSE script categories
- FTP anonymous enumeration
- SMB enumeration
- Host discovery
- Firewall considerations

## Basic Nmap Scan

I performed a basic Nmap scan against the authorized TryHackMe lab target.

Results
Port	State	Service
21/tcp	Open	FTP
22/tcp	Open	SSH
53/tcp	Open	DNS
80/tcp	Open	HTTP

Nmap also reported 996 closed TCP ports.

UDP Scan

I performed a UDP scan against port 161.

nmap -sU -p 161 10.49.190.20

Result:

161/udp  closed  snmp

Port 161 is commonly associated with SNMP.

TCP SYN Scan

A SYN scan can be performed using:

nmap -sS <TARGET-IP>

A SYN scan is also called a half-open scan or stealth scan.

TCP Connect Scan

A TCP Connect scan can be performed using:

nmap -sT <TARGET-IP>

It completes the TCP three-way handshake.

SYN
 ↓
SYN/ACK
 ↓
ACK
UDP Scan

UDP scanning can be performed using:

nmap -sU <TARGET-IP>
NULL, FIN and Xmas Scans

NULL scan:

nmap -sN <TARGET-IP>

FIN scan:

nmap -sF <TARGET-IP>

Xmas scan:

nmap -sX <TARGET-IP>

The Xmas scan uses the FIN, PSH and URG flags.

Ping Sweep

A ping sweep can be performed using:

nmap -sn 172.16.0.0/16

The -sn option performs host discovery without a port scan.

Nmap Options
Verbosity
nmap -vv <TARGET-IP>
Scan all TCP ports
nmap -p- <TARGET-IP>
Skip host discovery
nmap -Pn <TARGET-IP>
Save output in all major formats
nmap -oA scan <TARGET-IP>
Nmap Scripting Engine

Nmap includes the Nmap Scripting Engine (NSE) for additional enumeration and security checks.

Run a specific script:

nmap --script <script-name> <TARGET-IP>

Run scripts from the vulnerability category:

nmap --script vuln <TARGET-IP>

The intrusive category should be used carefully because some scripts may affect the target.

Finding NSE Scripts

Nmap stores NSE scripts on Linux in:

/usr/share/nmap/scripts/

Scripts can be searched using:

grep "ftp" /usr/share/nmap/scripts/script.db

or:

ls -l /usr/share/nmap/scripts/*ftp*
SMB OS Discovery

The SMB script I identified was:

smb-os-discovery.nse

It is used to gather operating system and related information from an SMB server.

FTP Anonymous Login

The ftp-anon script checks whether an FTP server allows anonymous access.

nmap -p 21 --script ftp-anon <TARGET-IP>

The optional argument is:

ftp-anon.maxlist
Key Learnings

This room helped me understand how Nmap can be used for:

Network reconnaissance
Port scanning
Service discovery
Host discovery
UDP scanning
TCP scanning
NSE-based enumeration
Basic vulnerability scanning

Most importantly, I learned how to interpret Nmap results instead of only running commands.

TryHackMe Completion

I completed the Further Nmap TryHackMe room.

Completed Tasks: 15
Points Earned: 328

Screenshots

Screenshots from my authorized TryHackMe lab practice are included in this folder.

Tools Used
Nmap
Nmap Scripting Engine (NSE)
Linux
TryHackMe
Disclaimer

All scans documented here were performed against an authorized TryHackMe lab environment for educational purposes.

```bash
nmap 10.49.190.20
