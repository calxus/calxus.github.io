---
layout: post
title: Hack the Box - Blue
date: 2020-03-13 16:04:22 +0100
description: Blue, while possibly the most simple machine on Hack The Box, demonstrates the severity of the EternalBlue exploit, which has been used in multiple large-scale ransomware and crypto-mining attacks since it was leaked publicly.
img: blue.png
fig-caption: Blue
tags: [Easy, Windows, Retired, CVE]
---
## Overview
Blue, while possibly the most simple machine on Hack The Box, demonstrates the severity of the EternalBlue exploit, which has been used in multiple large-scale ransomware and crypto-mining attacks since it was leaked publicly.
## Enumeration
```
┌──[10.10.14.27]-(calxus㉿calxus)-[~]
└─$ sudo nmap -p- -T4 -sV 10.129.112.220
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-13 18:53 GMT
Nmap scan report for 10.129.112.220
Host is up (0.094s latency).
Not shown: 65526 closed ports
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
49157/tcp open  msrpc        Microsoft Windows RPC
```
```
┌──[10.10.14.27]-(calxus㉿calxus)-[~]
└─$ sudo nmap -p139,445 --script vuln 10.129.112.225                                                                                                                                                                                   130 ⨯
Starting Nmap 7.91 ( https://nmap.org ) at 2021-03-13 19:36 GMT
Nmap scan report for 10.129.112.225
Host is up (0.016s latency).

PORT    STATE SERVICE
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Host script results:
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_OBJECT_NAME_NOT_FOUND
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
```
## Foothold
## Privilege Escalation