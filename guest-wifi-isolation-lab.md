# Guest Wi-Fi Isolation Lab

## Objective

Configure a wireless router so that a guest device can connect to Wi-Fi while being prevented from accessing devices on the trusted home LAN.

## Topology

- Home Router
- OWNER PC
- GUEST PC
- Main wireless network
- Guest wireless network

## Configuration

The OWNER PC was connected to the normal home Wi-Fi.

The GUEST PC was connected to the router's dedicated Guest Network.

The guest network was configured with WPA-PSK security and guest access to the local network was disabled.

## Testing

The OWNER PC had the following IPv4 configuration:

IPv4 Address: 192.168.0.102  
Subnet Mask: 255.255.255.0  
Default Gateway: 192.168.0.1

From the GUEST PC, I tested connectivity to the OWNER PC using:

ping 192.168.0.102

Before guest isolation was configured correctly, the ping succeeded:

Reply from 192.168.0.102

This showed that the guest device could still communicate with devices on the trusted LAN.

After enabling the router's dedicated Guest Network and disabling guest access to the local network, the same ping failed:

Request timed out.

## Result

Guest network isolation was successfully configured.

OWNER PC  
↓  
Main Wi-Fi  
↓  
HOME ROUTER  
↓  
Guest Wi-Fi  
↓  
GUEST PC  

GUEST PC → OWNER PC = BLOCKED

The guest device could use the guest wireless network but could not access the OWNER PC on the trusted LAN.

## Troubleshooting

Initially, I renamed one of the router's normal wireless networks to "guest".

This changed the SSID but did not create true guest isolation.

The GUEST PC was still able to ping the OWNER PC.

The issue was resolved by using the router's dedicated Guest Network feature and disabling access to the local network.

A different SSID does not automatically mean a separate or isolated network.

## Same-LAN Communication

Devices on the same LAN can normally communicate directly.

Example:

OWNER: 192.168.0.102  
GUEST: 192.168.0.103  
Subnet Mask: 255.255.255.0

Both addresses belong to the 192.168.0.0/24 network.

Because both devices are on the same subnet, the sending device does not normally need to send local traffic to the default gateway first.

Instead, it uses ARP to discover the MAC address of the destination device.

GUEST asks: "Who has 192.168.0.102?"

OWNER responds with its MAC address.

The GUEST PC can then send Ethernet frames directly to the OWNER PC.

This is why guest isolation is important. Without isolation, an untrusted guest device may be able to communicate with trusted devices on the LAN.

## What I Learned

A different SSID does not automatically provide network isolation.

Guest networks are used to separate untrusted devices from trusted LAN devices.

WPA-PSK provides wireless authentication and encryption but does not itself isolate devices.

Ping can be used to test whether hosts can communicate.

Devices on the same IPv4 subnet can normally communicate directly.

ARP is used to map an IPv4 address to a MAC address on the local network.

Guest isolation can block access to trusted LAN devices while still allowing network or internet access.

## Networking Concepts Practised

Wireless networking  
SSIDs  
WPA-PSK  
IPv4 addressing  
Subnet masks  
Default gateways  
ICMP  
Ping  
ARP  
MAC addressing  
Layer 2 communication  
LAN communication  
Network segmentation  
Guest network isolation  
Basic network security
