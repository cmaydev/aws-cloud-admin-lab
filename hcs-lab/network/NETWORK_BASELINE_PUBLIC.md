\# HCSL Network Baseline (Public / Sanitized)



\## Purpose

This document captures a \*\*known-good network baseline\*\* for the Hybrid Cloud Systems Lab (HCSL).  

It is designed for a public portfolio repository and intentionally uses \*\*sanitized addressing\*\*.



> Note: Exact IPs/MACs and sensitive identifiers are tracked privately in local ops notes.



---



\## Topology Overview

\- Single lab LAN segment (example: `10.0.0.0/24`)

\- One gateway/router (OpenWrt-based)

\- Temporary Layer-2 bridge device used as a \*\*port expander / unmanaged switch\*\*

\- Multiple Raspberry Pi hosts reachable from an operator workstation



---



\## Addressing (Sanitized Example)

\- Network: `10.0.0.0/24`

\- Gateway: `10.0.0.1`

\- Operator workstation: `10.0.0.10`

\- Hosts:

&nbsp; - `pi-core` → `10.0.0.21`

&nbsp; - `pi-util-01` → `10.0.0.22`

&nbsp; - `pi-parity` → `10.0.0.23`



---



\## Gateway

\- Platform: OpenWrt-based router (GL.iNet class device)

\- Role: L3 gateway for the lab LAN

\- SSH: enabled for LAN administration

\- Wi-Fi: previously had a lab SSID that was disabled and removed from baseline



---



\## Layer-2 Infrastructure

\### Temporary L2 Bridge (Disposable Infrastructure)

\- Device: Raspberry Pi (used as a temporary software switch)

\- Hostname (example): `hcsl-l2-bridge-temp`

\- Role: \*\*Pure Layer-2 bridge only\*\*

\- Bridge interface: `br0`

\- Key constraint: \*\*No IP assigned to the bridge (unmanaged switch behavior)\*\*



This device exists only to expand physical Ethernet ports and can be removed later without changing the logical lab topology.



---



\## Validation Checklist

\- From operator workstation:

&nbsp; - Hosts reachable (ICMP / SSH)

&nbsp; - Name resolution works as expected (or documented where it does not)

\- From any host behind the L2 bridge:

&nbsp; - Receives DHCP lease from the gateway

&nbsp; - Can reach gateway

&nbsp; - Can resolve DNS

&nbsp; - Can reach the internet (if enabled for the lab)



---



\## Change Control (Lightweight)

Any change to:

\- Subnet / DHCP scope

\- Gateway role or firewall posture

\- L2 bridge behavior

\- Host naming or addressing



…requires updating this baseline document and the associated diagram.



