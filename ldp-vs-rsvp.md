I want to share some brief notes about two protocols used for setting up the LSP in MPLS enabled core networks: LDP and RSVP. Both protocols have some important differences that should be understood to dig deeper into protection and restoration mechanisms as well as DiffServ-aware TE.

# LDP and RSVP

There are three protocols commonly used for the distribution of label bindings in MPLS networks:
* LDP
* RSVP
* BGP

Exists multiple extensions to IGPs that enable that protocols to distribute labels as an addition to perform classical routing functions on the network. That extensions are not commonly used in real deployments, so are not going to be covered here.

## LDP

Of the three, LDP is the youngest one. Was created explicitly to distribute labels and it’s not an extension or added functionality to a relatively old protocol like in the RSVP or BGP case.

LDP is designed to be highly extensible, using TLV triplets to be able to transport multiple additional fields in the future and warrantee the compatibility with previous versions via ignoring the unknown new fields.

LDP is highly flexible, as supports local and remote neighbors (using targeted LDP sessions). This flexibility allows an LSR to exchange label information with local and remote peers which enables it to support the engineering of multiple services and functionalities like LDP session protection.

LDP is a reliable protocol, because it uses TCP as transport. Only the neighbor discovery and maintenance is performed using UDP. The incremental updates functionality is a point in favor of its scalability.

If LDP is so reliable, extensible, functional and scalable, why do we even think about using an alternative to it in the MPLS core to do the job of setting up the labeled switched paths? Well, it follows the leader blindly and that may, under some circumstances, be a problem like may be in real life.

LDP follows the IGP in the decisions the later takes. The price to pay for that decision is loss of stability of the LSPs that LDP set up.

* Instability: if the IGP changes, the LDP will change with it, but late. LDP could set up instable LSPs in the network.

* Convergence: the convergence events that happens on every network are inherited by LDP and that could lead to data loss or looping conditions. The convergence time of the IGP will set a lower convergence time limit to LDP and to the LSPs (not considering LDP FRR capabilities yet).

* Race conditions: race conditions may always appear when two protocols interact in an unsynchronized way, and that may leads to data loss.


## RSVP

Please, I need you to complete this section with a similar approach :) so that we can compare yours with mine.
