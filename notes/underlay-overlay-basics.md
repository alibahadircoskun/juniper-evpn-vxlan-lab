# Underlay and Overlay Basics

This note explains the separation of underlay and overlay in the EVPN-VXLAN lab, a fundamental concept in modern data center networks.

## What is the Underlay?

The underlay is the physical IP network that carries all traffic.  
It provides basic IP connectivity between all spine and leaf switches using point-to-point routed links.

### Underlay Features in This Lab

- Leaf-to-Spine links run Layer 3 with /31 subnets
- Routing uses eBGP between leaves and spines
- Loopback interfaces are advertised via BGP
- ECMP allows load balancing across uplinks

## What is the Overlay?

The overlay is a virtual network that runs on top of the underlay.  
It enables L2 and L3 services between endpoints without requiring direct L2 connectivity.

### Overlay Features in This Lab

- VXLAN provides Layer 2 tunneling across the IP fabric
- EVPN is used as the control plane for MAC and IP route advertisement
- iBGP is used between all leaf nodes to exchange EVPN routes
- Loopback addresses are used as VTEP source and BGP peer IPs

## Summary

- Underlay = physical IP connectivity  
- Overlay = virtual L2/L3 services using VXLAN and EVPN  
- They are independent but work together to deliver scalable, resilient networks

