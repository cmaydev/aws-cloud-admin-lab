

---



\### E) `hcs-lab\\appendix\\windows-linux-recon-cheatsheet\_PUBLIC.md`



```markdown

\# Windows ↔ Linux Recon Cheat Sheet (Public / Sanitized)



This cheat sheet maps common Linux networking recon/triage tools to Windows/PowerShell equivalents.



> Addresses shown are examples (e.g., 10.0.0.0/24).



---



\## Neighbor / ARP table

\*\*Use case:\*\* IP↔MAC discovery on the local LAN.



Linux:

\- Command: `ip neigh`

\- Common options:

&nbsp; - `ip neigh show nud reachable`

&nbsp; - `ip neigh flush all`



Windows (PowerShell):

\- Command: `Get-NetNeighbor`

\- Common options:

&nbsp; - `-AddressFamily IPv4`

&nbsp; - `-InterfaceAlias "Ethernet"`



Legacy:

\- Command: `arp -a`



---



\## Ping sweep (populate neighbor table)

\*\*Use case:\*\* lightweight host discovery without port scanning.



Linux:

\- Command:

&nbsp; ```bash

&nbsp; for i in $(seq 1 254); do ping -c1 -W1 10.0.0.$i >/dev/null; done





Windows (PowerShell):



Command:



1..254 | ForEach-Object { Test-Connection 10.0.0.$\_ -Count 1 -Quiet } | Out-Null



Port reachability test



Use case: “Is SSH/HTTP reachable?”



Linux:



Command: nc -zv 10.0.0.1 22



Windows (PowerShell):



Command: Test-NetConnection 10.0.0.1 -Port 22



Common option: -InformationLevel Detailed



DNS resolution



Use case: differentiate DNS failure from network failure.



Linux:



Command: dig example.com



Lightweight: getent hosts example.com



Windows (PowerShell):



Command: Resolve-DnsName example.com



Legacy: nslookup example.com



Interfaces + IPs



Linux:



Command: ip addr



IPv4 only: ip -4 addr



Windows:



Command: Get-NetIPAddress



IPv4 only: Get-NetIPAddress -AddressFamily IPv4

