<title>A design for secure networking</title>
<center><br/><br/><br/>

A design for secure networking
==============================

<p style="width: 60%; text-align: justify;">The main security goal of
this design is to remove the need to trust the hardware vendors of
your network interfaces. This is necessary, as there is no practical
way to inspect and verify the actual functionality of the networking
hardware and firmware that is going to be used for a connected system.</p>

<p style="width: 60%; text-align: justify;">For example, your Internet
firewall or router should not have to trust the network interface
hardware vendors. To achieve this, all network traffic needs to be
securely wrapped before it reaches the network interface of the
firewall or router of the internal network, while also insulating the
link from direct unwrapped traffic.</p>

by Leonard Norrg&aring;rd &lt;<vinsci@refactor.fi>&gt;

December 24th, 2012
</center>


It turns out that the solution to the networking hardware vendor trust
problem is quite simple and can be implemented using purpose-built but
cheap networking devices, where each device handles one physical
network connection.

The purpose-built networking devices are virtual private network (VPN)
tunnel endpoint devices, but with an additional internal link. This
internal link is the key to providing networking security.

Each VPN tunnel endpoint device in this design has two independent and
symmetrical parts (A and B), containing the same hardware and with a
standard *high-speed inter-chip data link* between the two parts. The
symmetrical parts have different firmware, to enable the B part to
implement a VPN authenticated tunnel:

<pre>
                         +------------------+
                         |                  |
    To the Internet or   |  +---+    +---+  |
    connected device ----|--| A |____| B |==|==== To router/firewall
                         |  +---+    +---+  |
                         |    !        !    |
                         +------------------+
                              !        !
                            Firmware programming interfaces

    Key:
        ---- Normal data link.
        ==== VPN tunnel data link, encrypted and authenticated.
        ____ Device internal high-speed chip to chip communications link.

        !    Firmware programming interface, one for each symmetrical part,
             used to upload the firmware for each part and in the part B case
             also encryption keys and authentication certificates.
</pre>

Each of the two symmetrical parts A and B has a suitable CPU or
microcontroller and a physical networking interface. In addition the
design requires a standard inter-chip data link for the two
independent parts to communicate. Each suitable CPU or microcontroller
typically implements at least one such high-speed link.

The firmware of the B part includes encryption keys and authentication
certificates. These must be unique to all VPN tunnel endpoint devices,
in order to avoid security breaches resulting from any mistakes done
when connecting the network cables to each device as well as provide
basic protection against unauthorized replacement of the device with
an insecure device.


Why is this secure?
-------------------

The VPN tunnel data link between the VPN tunnel device B part and the
router/firewall is encrypted and authenticated with both ends only
processing packets that were properly encrypted and authenticated. The
router/firewall processes the network traffic entirely in software,
after checking that it is authentic. The communications link between A
and B is entirely controlled by the firmware in each of the two parts
of the VPN tunnel endpoint device. This leaves no attack surface for
the physical hardware interfaces on either of the B part or the
router/firewall. Any successful attacks on the A part network
interface does not matter.


No physical protection
----------------------

Obviously, this design on its own doesn't address physical attacks on
the devices themselves, nor physical attacks on the router/firewall
itself.


A complete network router/firewall system
-----------------------------------------

The VPN endpoint devices described above can be used to build a secure
firewall and/or router using a standard PC where each network
connection is over a link equipped with one of the VPN endpoints. No
network link to the router/firewall is without a VPN endpoint
device. To protect internal computers or internal *groups of computers*
on the network from each other, they shouldn't share network
connections to the router/firewall.

Thus, the firewall/router only ever receives network traffic via the
VPN tunnel endpoint devices.


Implementation
--------------

No implementation exists yet.

<center>&#10086; &#10086; &#10086;</center>
