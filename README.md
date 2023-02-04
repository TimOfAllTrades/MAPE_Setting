# MAPE_Setting

A blog on getting MAP-E to work on OpenWRT
MAP-E support for Japanese Internet Service Providers

A detailed method for installing MAP-E support on OpenWRT routers is explained.  Credit goes to https://github.com/fakemanhk/openwrt-jp-ipoe

Background

Japanese ISPs, primarily fiberoptic providers, uses PPPoE authentication for their slower and older internet communication.  As the number of users increased, the somewhat less efficient PPPoE protocol and the aging hardware infrustructure supporting it was unable to keep up with demand resulting in significantly slow speeds particularly in crowded areas at crowded times of the day.  The solution was to use new protocols IPoE and IPv6 in an effort to provide faster speeds while alleviating the ip address exhaustion issue that existed with IPv4.

The transition to IPv6 has not been a smooth one due to the incompatibility with IPv4 and to this day, IPv6 internet coexists separately from IPv4, leaving ISPs and other “internet brokers” to provide the link between the two.  Since the vast majority of the internet is still IPv4, ISPs use Virtual Network Enablers (VNE) to encapsulate IPv4 internet data and send it to users via IPv6.  This is commonly referred to as IPv4 over IPv6.

How ISPs implement their IPv4 over IPv6 methods has no universally accepted standard and each provider has resorted to their own ways to do so.  

A side effect of this is that many Japanese routers (usually of low quality) are specifically configured to work on certain ISPs and the methods are not disclosed or transparent to the user.  This has made higher end or gaming routers incompatible with the IPv4 over IPv6 communication of Japanese ISPs, significantly limiting the users ability to customize or enhance their own home networks or add additional tools, such as VPN or webservers.

OpenWRT is an open source operating system that many high end routers use or can be installed with.  By enabling Japanese IPv4 over IPv6 communication methods on OpenWRT, this enables any router running OpenWRT to fully take advantage of the faster IPv4 and IPv6 communications in Japan, no longer limiting such features to Japanese specific routers.

Types of Virtual network enablers VNEs

There are many names for IPv4 over IPv6 VNEs that providers use, but they can all be more or less aggregated into two categories MAP-E and DS-Lite.  Both cases combine multiple subscribers into a single IPV4 address using ports to differentiate each users’ communication.  DS-lite is set so that port assignment is provided on the fly by the provider, whereas MAP-E allocates a certain range of ports for each particular user.  

In my opinion, the MAP-E implementation is better since the port range for your internet is constant, which allows for a static IP and port in which external communication can always be reached at.  This is important if you hope to host game or file servers or if you want to set up a vpn server.  In contrast, DS Lite doesn’t have static ports so an IP address and port that your application is listening on could be assigned to someone else later on by the ISP. 

Examples of MAP-E providers are OCN, So-net Purara and so on.  A detailed list can be found here.  https://www.kahemicafe.com/ipv4-over-ipv6-provider

I personally use Docomo Hikari with OCN as my provider which is a MAP-E type IPv4 over IPv6 configuration

OpenWRT compatible routers

OpenWRT is an open source operating system for routers, like Linux is to personal computers.  OpenWRT provides a platform for many custom software and options for routers to allow users to configure their home networks to their own liking.  OpenWRT also runs on many high end hardware routers and thus users are not forced to use slower Japanese routers for the sake of IPv4 to IPv6 connectivity.

Compatible hardware can be found on OpenWRT’s table of hardware page https://openwrt.org/toh/start.


To install OpenWRT on a router (the image above is for a TP-link Archer A6 v3), you need to download the file provided in the Firmware OpenWRT Install URL link.  It is probably best to first find a router you like on OpenWRT before purchasing as not all routers are compatible.  Furthermore, particularly for first timers, you should ensure that the file name has the word squashfs in it as this is a linux binary compatible with the GUI upgrade option inside router web Uis.  If the link or openwrt firmware file contains the text “initramfs,” it will be significantly harder to upgrade.

I tested this on a TP link Archer A6 version 3 router.  Simply navigate to the upgrade firmware section and select the bin file downloaded from the openwrt site to begin the flashing process.

OpenWRT settings
