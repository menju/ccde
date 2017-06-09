# IS-IS overload bit

Overload bit is used to alert all the devices in a certain area by setting a particular bit in LSPs (link state packets):

* A router runs out of system resources
* It can't store LSDB
* It can't run SPF

When this situation is detected by other routers, they **won't use this router for transit traffic**, but they will use it for packets destined to the overloaded router's directly connected networks and IP prefixes.



## Design use cases

The overload bit has some aditional or expanded uses in design to avoid the creation of **black holes** of traffic and to **limit the amount of information that routers advertise** in their own LSPs.

* On start-up for a limited amount of time to ensure that the router does not receive transit traffic while the routing protocol is still converging, avoiding _black holes_.
* To suppress some prefixes from being advertised in the router own LSPs.
    * L1 into L2 or L2 into L1: avoid being a transit node
    * External routing information: avoid being an ASBR



# References

[Uses of the Overload Bit with IS-IS](http://www.cisco.com/c/en/us/support/docs/ip/integrated-intermediate-system-to-intermediate-system-is-is/24509-set-overload-bit.html)
