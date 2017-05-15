# AToM vs L2TPv3

The next table summarizes the major differences between two L2 VPN VPLS solutions: AToM and L2TPv3.

![l2vpn-tree][logo]

[logo]:images/atom-vs-l2tpv3-map.png


| | AToM | L2TPv3 |
| - | - | - |
| Underlying infrastructure requirements | MPLS | IP |
| Supported L2 protocols | Ethernet, PPP, HDLC, FR, ATM | Ethernet, PPP, HDLC, FR, ATM |
| Signaling protocol | Targeted LDP, out of band | L2TP, in band |
| Transport protocol | MPLS | IPv4 (protocol #115) UDP (port #1701) |
| Tunnel Type | 2 unidirectional LSPs (data) | 1 bidirectional (for control and data)|
| Tunnel Overhead | Short, 2 labels = 8 octets | Large (IPv4 and UDP) |
| Control Message Authentication | TCP MD5 for LDP sessions | Shared secret message digest |
| Encryption | Can’t be directly encrypted with IPSec | Easy IPSec integration |
| Inter-AS | Hard. Inter-AS interconnection | Easy because the SP are already interconnected |
| Data path verification | MPLS ping, MPLS traceroute | IP ping, IP traceroute |
| Scalability (Customer) | High | Medium |
| Opex & Capex (Customer) | Low | Medium |
| MTU | Need to match at both sides | Path MTU discovery |
| QoS | MPLS-TE | IP DiffServ |
| Cost | High | Low |
| Deployment Time | High (if not automated) | Low |
| Resiliency | Very High, FRR | Medium |




## Underlying infrastructure requirements

AToM architecture requires an underlay MPLS network to transport traffic between customer endpoints. If the customer is attached to a service provider with an MPLS enabled core providing L2 VPN services AToM may be an option to consider.

L2TP only requires IP connectivity to provide L2 VPN services and for this reason is a good option when there is not an MPLS enabled network available or that option don’t want to be used again for other reasons, such as economic associated costs.


## Supported L2 protocols

Both options support Ethernet, PPP, HDLC, FR and ATM technologies.

Nowadays, the most commonly AToM and L2TP transport Ethernet frames over MPLS or IP. There are two types of Ethernet support over AToM and L2TP:

* Untagged Ethernet frames
* Tagged Ethernet frames (802.1Q frames)

The untagged transport of Ethernet frames is also known as port mode whereas the Tagged mode is known as VLAN mode.

Depending on the selected mode, PE (or LCCE) routers classify Ethernet frames received from the CE customer device into one or different pseudowires.


## Signaling protocol

AToM uses LDP to distribute labels. It uses targeted LDP sessions between PE routers to exchange the labels needed to set up the pseudowires. LDP works out of band

L2TPv3 uses L2TP in band protocol to set up the pseudowire.



## Transport protocol

AToM transports the L2 payload over MPLS using label based forwarding.

L2TPv3 specification defines two available methods, tunnel the L2 frames over IP or over UDP. The tunneling mechanism inserts a L2TP header between the IP or UDP header and the L2 payload.

L2TP control packets are transmitted in band with data packets. This may not be the case in AToM where LSP may not follow the LDP (the later will follow the IGP).

The UDP transport mode is more suitable when using IPSec or when traversing NAT and firewalls.


# Tunnel Type

AToM emulates a pseudowire as 2 MPLS LSPs. The MPLS LSPs are unidirectional by design, so to enable bidirectional communication, AToM needs two of them in opposite directions.

L2TPv3 sessions are bidirectional. The L2TPv3 session identifies the corresponding pseudowire for that session. The L2TPv3 session ID is equivalent to the AToM pseudowire label. Each pseudowire has associated two session IDs (one for each customer site).


## Tunnel Overhead

AToM uses at least 2 MPLS label stack entries to transport the frames between customer sites. Each MPLS label stack entry is 4 octets.

L2TPv3 can use IP or UDP as a transport protocol. In any case, the overhead introduced is higher than the introduced by AToM. The size of an IPv4 header varies between 20 and 60 octets. The size of an UDP header is 8 octets.


## Control message authentication

In AToM, the targeted LDP sessions between the PE routers may be authenticated by using MD5 TCP header authentication.

L2TP can use message digest with shared secret authentication (HMAC-MD5, HMAC-SHA-1).


## Encryption (payload)

L2TPv3 can use UDP and IP as transport protocols for L2 frames. Because of that, the integration with IPSec is much easier that in the AToM case.


## Inter-AS

As IP connectivity to the public Internet is available at most of the locations worldwide, L2TPv3 is easy to manage and deploy quickly in the case of dispersed sites. IP connectivity is usually cheaper than the L2VPN alternative.

AToM service may not be available at every location when each location depends on different service providers. This service providers may not have in their portfolio L2VPN services or an interconnection may be needed between them to exchange frames from different sites of the same VPN.


## Data path verification

AToM needs MPLS ping and traceroute to verify the data plane. This is because the path the MPLS labeled packets follow may not be the same of the regular IP packets.


## MTU

L2TPv3 can use path MTU discovery to adjust the MTU along the path from source to destination.

AToM does not use IP as a transport, so the MTU must be carefully matched at both sides of the interconnection.


## Resiliency & QoS

AToM L2VPNs could make use of all the mechanisms enabled in the service provider core to increase the resiliency of the network.

L2TPv3 is often deployed over public Internet connections, so the QoS and resiliency of the interconnection solution is very limited.
