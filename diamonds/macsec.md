# MACsec

MACsec works at link layer (L2) providing:

* confidentiality
* authentication 
* eavesdropping pevention (aka MIM attacks), because it detects any alteration or replay of frames. 

IPSec works at network/transport layer (L2/L3) setting up end-to-end session based encryption.

MACsec is a cyber security complement to IPSec, not an alternative.



## Use cases

MACsec is agnostic to the Ethernet traffic type and can be easily added to systems to provide an additional layer of protection to a network.

* Enterprise customers can adopt MACsec to provide protection behind their firewall.  System administrators can authorise ports to communicate in a secure fashion, and can detect misuse such as attempted Denial of Service (DOS).
* Data Center and Cloud-based systems can benefit from the confidentiality and data source authentication offered by MACsec.

MACsec typically works in conjunction with IEEE 801.1X-2010 which provides the secure key distribution around the network.  

![MACsec example][images/macsec-example.jpg]

But what happens when you want to protect your traffic using MACsec and that traffic has to go over a service provider’s network? Your devices will not be directly connected hence the intermediary devices will tamper with MACsec requirements.

You can overcome this problem by using Ethernet over MPLS circuits or LAN service emulation (E-LAN VPLS, E-LINE VPWS).



# References

* [Algotronix](http://www.eetimes.com/document.asp?doc_id=1317153)
* [MACsec over L2 circuit](http://nextheader.net/2016/10/07/macsec-over-l2circuit/)
