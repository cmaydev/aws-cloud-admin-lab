# Temporary L2 Bridge — Raspberry Pi (Public / Sanitized)

## Purpose
This document describes a **temporary Layer-2 Ethernet bridge** implemented using a Raspberry Pi.

The device exists solely to:
- Extend available Ethernet ports
- Behave like an **unmanaged switch**
- Be safely removed later with **no impact** to the lab

This is **infrastructure glue**, not a permanent node or service.

---

## Hardware
- Raspberry Pi (used in this build: Pi 2–class device)
- Multiple USB-to-Ethernet adapters

---

## Operating System
- Ubuntu Server 22.04 LTS (ARM)

---

## Network Role (Explicit)
**Layer-2 bridge only**

The bridge:
- Forwards Ethernet frames
- Does NOT participate in Layer-3

Explicitly excluded:
- No NAT
- No DHCP
- No routing
- No firewall rules
- No services beyond what is required for bridging

This configuration intentionally mimics the behavior of a **dumb/unmanaged Ethernet switch**.

---

## Configuration Summary (High Level)
- A Linux bridge interface (`br0`) is created
- Physical Ethernet interfaces are attached to `br0`
- The bridge interface has **no IPv4 address**
- Downstream hosts obtain addressing directly from the gateway

All addressing examples are sanitized for public documentation.

---

## Validation
Bridge functionality is validated indirectly:
- Downstream hosts receive DHCP leases
- Hosts can reach the gateway
- DNS resolution works
- Internet access functions when permitted

The bridge device itself is **not expected to respond to ping or SSH**.

---

## Removal Plan
Once a physical Ethernet switch is available:
1. Power down the temporary bridge device
2. Move downstream Ethernet cables to the switch
3. Verify host connectivity
4. Remove the bridge device from the lab

No configuration changes should be required elsewhere.

---

## Notes / Deviations
- A management IP may be temporarily assigned for maintenance during build/debug
- Any such IP must be removed after validation to preserve Layer-2-only behavior
