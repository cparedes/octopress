--- 
layout: post
title: Network Deployment and Planning
comments: true
post_id: "215"
categories:
- Computers
- Consulting
- Networks
- Wifi
---
I'm doing a bit of consulting on the side for a small business in Seattle, and I'm tasked with coming up with a proposal for improving the reliability of their wifi network (which could mean anything between the internet and the user's laptop, including the network gateway, wifi AP capacity, etc.), and ultimately implementing all of the hardware and software.  As I have probably said before, I'm mostly on the technical side of IT rather than the business side, so this will expose me more to the business side of things.

On the technical side, the plan is to make sure that the network has close to 100% uptime during business hours.  Between the gateway and the internet, we can look at whether the routes to the typical services are reliable; this means looking at the next hop (at the very least), the ISP provided DNS servers, etc.  I typically change the DNS servers over to 4.2.2.1, 4.2.2.2, and 4.2.2.3, which are all provided by Level 3 (this is of course dependent on the circumstances, we might have to setup a local DNS server for any name resolutions for in-house servers.)  Between the gateway and any other device, we will want to make sure that the connection between the gateway and whatever other device physically exists right after the gateway does not get saturated.  If it does, we would probably have to look either at any switches in between the gateway and any other device, install more routers in order to limit the data that hits the gateway, or install a firewall and simply block certain packets from going through.  Since this particular deployment will most likely not saturate a 1 Gbps connection on the gateway, we will only put a switch right after the gateway and turn on basic QoS just in case.

Next, since this is a wifi deployment, we will have to worry about wifi capacity on each access point, not to mention any possibility of crosstalk between APs.  Without getting into details of doing a site survey and identifying any blind spots or whatever, we would have to know the real world capacity of each AP, and deploy accordingly.  We expect maybe 30-40 clients on the entire network at any given time, spread out between two different floors and separated by concrete.  So at the very least, we need two or three APs to cover both floors.  From what I've seen, there's at least fifteen laptops open at any given time on the first floor, with the first floor separated by brick between two rooms.  Therefore, we will need two AP's at the very least in the first floor, with maybe a third AP in order to make sure we cover every corner of both rooms.  Let's say that there are ten people in one room that are all connected on 802.11g.  Realistically, we can expect a throughput of 35 Mbps per client; therefore, we can expect the throughput to be around 300-350 Mbps total on one AP; if the AP has a 1 Gbps interface, then this is quite good, though I might be missing a few details.

However, if we are to consider a 802.11n deployment, then we will be be expecting about 70-150 Mbps throughput in the best conditions, with a theoretical maximum of 300 Mbps.  This will hit the 1 Gbps interface at around 700 Mbps-1500 Mbps of throughput, which might become a problem; this is also all assuming that we will be deploying AP's without much centralized control.  This would pose a problem in this particular case if there is a lot of peer to peer activity within the network, yet if we are assuming that about half of the users will simply use the internet, then this will soften the load considerably.

On the business side, there will have to be an SLA in place between me and the business, as well as a clear outline of what is to be provided, how it will be deployed, and deadlines on the various phases of the deployment.  Further, I will have to audit their current network and ensure that the deployment will have a noticeable increase in reliability and speed.  Again, I don't know whether I am missing anything; I need to work on the business side a bit more.

Anyway, hopefully this sheds a bit of light on my own line of thinking, and I hope that it falls somewhat the standards of network deployment.
