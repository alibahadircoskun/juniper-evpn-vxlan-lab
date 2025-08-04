# VLAN and IRB Configuration in the Lab

This note explains how VLANs and IRB interfaces are used in my EVPN-VXLAN Spine-Leaf lab to provide L2 segmentation and routing.

## VLANs and VXLAN VNIs

- VLANs are defined per tenant or service (e.g., Data1, Data2).
- Each VLAN is mapped to a VXLAN VNI for overlay segmentation.
- VLAN to VNI mapping enables VXLAN encapsulation and traffic isolation across the fabric.

## IRB Interfaces as Gateway

- IRB interfaces act as the default gateway for hosts in each VLAN.
- Virtual Gateway Address and Virtual MAC provide seamless gateway redundancy across leaves.
- The IRB interface is tied to the VLAN via `l3-interface` and configured with the VLAN subnet.

## Lab-Specific Highlights

- VLANs `Data1` and `Data2` correspond to VNIs 20512 and 20513 respectively.
- IRB virtual-gateway MAC addresses are manually configured for consistency.
- Proxy ARP and virtual gateway acceptance are enabled on IRB interfaces to support host failover.

### Partial Configuration Example from Leaf3

```set vlans Data1 vlan-id 512
set vlans Data1 vxlan vni 20512
set vlans Data1 l3-interface irb.512

set interfaces irb unit 512 proxy-macip-advertisement
set interfaces irb unit 512 virtual-gateway-accept-data
set interfaces irb unit 512 family inet address 10.99.55.200/24 virtual-gateway-address 10.99.55.1
set interfaces irb unit 512 virtual-gateway-v4-mac 00:aa:11:bb:22:cc
