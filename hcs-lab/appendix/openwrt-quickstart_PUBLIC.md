\# OpenWrt Quick Start (Public / Sanitized)



\## What OpenWrt Is

OpenWrt is a Linux-based operating system for routers and embedded networking devices.  

It uses a declarative configuration system (UCI) and standard Linux networking tools.



---



\## Core mental model

\- \*\*Runtime state\*\*: what the system is doing right now (`ip`, `iw`, logs)

\- \*\*UCI config\*\*: what should persist across reboots (`/etc/config/\*` via `uci`)

\- \*\*Services\*\*: apply config to runtime (`network`, `firewall`, `wifi`, `dropbear`)



---



\## Where config lives

\- `/etc/config/network` — interfaces, bridges, VLANs

\- `/etc/config/wireless` — radios, SSIDs

\- `/etc/config/firewall` — zones and rules

\- `/etc/config/dhcp` — dnsmasq DHCP/DNS

\- `/etc/config/system` — hostname/time



---



\## High-signal operational commands



\### Identity / platform

\*\*Command:\*\* `ubus call system board`  

\*\*What it does:\*\* Shows platform + OpenWrt release metadata  

\*\*Why used:\*\* Confirms firmware target and environment before changes



\*\*Command:\*\* `cat /etc/openwrt\_release`  

\*\*What it does:\*\* Shows OpenWrt release info  

\*\*Why used:\*\* Quick proof of OS version/build



---



\### UCI workflow (config changes)

\*\*Command:\*\* `uci show <config>`  

\*\*What it does:\*\* Prints config (read-only)  

\*\*Why used:\*\* Inspect before touching anything



\*\*Command:\*\* `uci set <config>.<section>.<option>='<value>'`  

\*\*What it does:\*\* Updates config in memory  

\*\*Why used:\*\* Safe, scriptable change mechanism



\*\*Command:\*\* `uci commit <config>`  

\*\*What it does:\*\* Writes changes to disk  

\*\*Why used:\*\* Persistence across reboot



\*\*Command:\*\* `wifi reload`  

\*\*What it does:\*\* Applies wireless config  

\*\*Why used:\*\* Enable/disable SSIDs without reboot



Example pattern:

```sh

uci set wireless.<section>.disabled='1'

uci commit wireless

wifi reload





Wireless truth vs config

Command: iw dev
What it does: Shows what’s actively broadcasting
Why used: Ground truth for Wi-Fi state

Command: uci show wireless
What it does: Shows declared wireless config
Why used: Identify which config section maps to a live SSID

Network state

Command: ip addr
What it does: Interface addressing
Why used: Confirm LAN/WAN/VLAN interfaces

Command: ip route
What it does: Routing table
Why used: Confirm gateway behavior and reachability

Logs

Command: logread
What it does: Shows system logs
Why used: First stop for connectivity, DHCP, Wi-Fi issues