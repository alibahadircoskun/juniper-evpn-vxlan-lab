# Spine-Leaf Overview

This note provides a quick overview of the Spine-Leaf architecture used in my Juniper EVPN-VXLAN lab.

## What is Spine-Leaf?

Spine-Leaf is a modern Layer 3 data center topology that delivers predictable latency and high bandwidth.  
It consists of two layers:

- **Spines**: Core switches that interconnect all leaf switches.
- **Leaves**: Access switches that connect to the spines and endpoints (servers etc.).

Every leaf is connected to every spine there are no direct leaf-to-leaf or spine-to-spine links.

## Lab Topology

- **Spines**: SPINE1, SPINE2  
- **Leaves**: LEAF3, LEAF4, LEAF5

Each leaf is dual-homed to both spines to ensure redundancy and ECMP.

## Benefits

- **Scalability**: Easy to add more leaves without touching the spine layer.  
- **Predictable Performance**: Fixed two-hop path between any two endpoints.  
- **Redundancy & Load Balancing**: Equal-Cost Multi-Path (ECMP) across uplinks.

## Architecture Notes

- **Underlay**: IP fabric using eBGP between leafs and spines.  
- **Overlay**: EVPN as the control plane over VXLAN.  
- **Routing**: IRB interfaces on leafs provide L3 gateways for VLANs.  
- **Loopbacks**: Each device has a loopback interface used for VTEP sourcing and BGP peering.

