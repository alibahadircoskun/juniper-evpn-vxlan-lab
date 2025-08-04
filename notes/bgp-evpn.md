# BGP and EVPN

This note covers how BGP and EVPN are used in the lab to build the control plane for VXLAN-based Layer 2 and Layer 3 services.

## BGP Overview

BGP is used in two roles:

- **eBGP for Underlay**  
  Leaf switches form eBGP sessions with spine switches using directly connected interfaces.  
  Loopbacks are advertised to provide stable endpoint addressing.

- **iBGP for Overlay**  
  All leaf switches form iBGP sessions with each other (full mesh).  
  These sessions use loopback addresses and carry EVPN routes.

## EVPN Overview

EVPN (Ethernet VPN) is an extension to BGP that enables MAC and IP address learning through control-plane signaling.

### Key EVPN Route Types Used

- **Type 2 (MAC/IP Advertisement)**  
  Advertises MAC and IP information for hosts connected to the fabric

- **Type 3 (Inclusive Multicast)**  
  Used for VXLAN flood groups and broadcast traffic replication

- **Type 5 (IP Prefix Route)**  
  Advertises IP prefixes for inter-subnet routing (optional but supported)

## Why Use BGP with EVPN?

- Scales better than flood-and-learn VXLAN  
- Centralized route control using standard BGP  
- Supports integrated L2 and L3 services

## Summary

- eBGP builds the underlay  
- iBGP with EVPN builds the overlay  
- EVPN advertises MAC and IP reachability for hosts over VXLAN tunnels

