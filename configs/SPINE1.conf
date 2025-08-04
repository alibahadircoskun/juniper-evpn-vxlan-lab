## SPINE1 - Juniper Spine Router Configuration
## Junos version: 17.4R1.16
## Cleaned-up version with underlay interfaces and BGP config

set version 17.4R1.16

# Hostname
set system host-name SPINE1

# Interfaces - Underlay links and Loopback
set interfaces xe-0/0/3 unit 0 family inet address 172.16.13.0/31
set interfaces xe-0/0/4 unit 0 family inet address 172.16.14.0/31
set interfaces xe-0/0/5 unit 0 family inet address 172.16.15.0/31
set interfaces lo0 unit 0 family inet address 1.1.1.1/32

# Routing options
set routing-options router-id 1.1.1.1
set routing-options autonomous-system 65530
set routing-options forwarding-table export LB
set routing-options forwarding-table chained-composite-next-hop ingress evpn

# BGP Underlay - external peers with multipath and export policy
set protocols bgp group UNDERLAY type external
set protocols bgp group UNDERLAY export Export-Lo
set protocols bgp group UNDERLAY local-as 64512
set protocols bgp group UNDERLAY multipath multiple-as
set protocols bgp group UNDERLAY neighbor 172.16.13.1 peer-as 64514
set protocols bgp group UNDERLAY neighbor 172.16.14.1 peer-as 64515
set protocols bgp group UNDERLAY neighbor 172.16.15.1 peer-as 64516

# BGP Overlay - EVPN signaling with internal peers
set protocols bgp group OVERLAY type internal
set protocols bgp group OVERLAY local-address 1.1.1.1
set protocols bgp group OVERLAY family evpn signaling
set protocols bgp group OVERLAY cluster 1.1.1.1
set protocols bgp group OVERLAY local-as 65530
set protocols bgp group OVERLAY multipath
set protocols bgp group OVERLAY neighbor 2.2.2.2
set protocols bgp group OVERLAY neighbor 3.3.3.3
set protocols bgp group OVERLAY neighbor 4.4.4.4
set protocols bgp group OVERLAY neighbor 5.5.5.5

# Policy Statements
set policy-options policy-statement Export-Lo term 1 from protocol direct
set policy-options policy-statement Export-Lo term 1 from interface lo0.0
set policy-options policy-statement Export-Lo term 1 then accept
set policy-options policy-statement LB term 1 then load-balance per-packet
set policy-options policy-statement LB term 1 then accept
