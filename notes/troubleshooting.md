# Troubleshooting Story: Virtual Gateway Not Reachable and VXLAN Tunnel Issues

While working on my Juniper EVPN-VXLAN lab, I encountered a frustrating problem that took quite some time to resolve.

## The Problem

- I could successfully ping the physical gateway IP address on the IRB interface.
- However, the **virtual gateway IP** configured for VXLAN did not respond to pings.
- As a result, hosts connected on different leaf switches could not communicate.
- Additionally, VXLAN tunnels between the leaf switches were not forming properly, breaking the overlay connectivity.

## What I Checked

- **Underlay connectivity:** All spine-leaf BGP sessions were established and stable.
- **Interface configurations:** IRB interfaces had correct IP addresses and VLAN membership.
- **BGP EVPN peers:** Overlay BGP sessions were established, but overlay routing did not work as expected.
- **EVPN protocols:** Checked for missing settings related to virtual gateway behavior.

## Root Cause

I discovered that the EVPN virtual gateway requires an explicit setting to accept data traffic destined for the virtual gateway IP. Without enabling this, the virtual gateway does not respond, causing hosts to be unreachable and VXLAN tunnels to malfunction.

## The Fix

Entering EVPN protocol configuration mode and adding:

```bash
edit protocols evpn
set virtual-gateway-accept-data
commit
