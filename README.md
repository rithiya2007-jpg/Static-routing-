# Static Routing Between Two LANs

A Cisco Packet Tracer lab illustrating how two routers can connect separate LANs using static routes. The supplied screenshot shows two router-connected LANs and ping tests from a PC.

## Project Overview

Two LANs use separate IP subnets and connect through two routers over a point-to-point network. Static routes allow devices on one LAN to reach devices on the other LAN.

> **Artifact limitation:** The original Cisco Packet Tracer `.pkt` file was not provided. This repository includes the supplied topology/test screenshot and documentation only. The configuration has not been independently tested.

## Features

- Two-router topology
- Two separate LANs
- Point-to-point router link
- Static-routing concept
- PC-to-PC ping verification

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS routing concepts
- IPv4 addressing and subnetting
- Static routes and ICMP ping

## Project Structure

```text
static-routing-two-lan/
├── README.md
└── screenshots/
    └── static-routing-topology-and-ping.png
```

## Network Topology Details

The screenshot labels these networks and interfaces:

| Segment | Addressing shown |
|---|---|
| Left LAN | `192.168.1.0/24` |
| Right LAN | `192.168.2.0/24` |
| Router-to-router link | `192.168.3.2` and `192.168.3.3` are shown on the link |

Visible endpoint examples include `192.168.1.2`, `192.168.1.3`, `192.168.2.2`, and `192.168.2.3`. The router LAN-side labels include `192.168.1.1` and `192.168.2.1`.

The exact subnet mask and complete interface configuration should be confirmed when rebuilding the topology.

## How to Recreate and Test

1. Add two Cisco ISR 4331 routers, two Catalyst 2960 switches, and two PCs per LAN.
2. Connect each LAN's PCs to its switch, and each switch to its local router.
3. Connect the routers using the interfaces supported by your selected Packet Tracer models.
4. Configure the LAN interfaces and router-to-router interfaces with non-overlapping IP addresses.
5. Configure each PC with an IP address, subnet mask, and default gateway for its LAN.
6. Add a static route on Router0 to the right LAN through Router1.
7. Add a return static route on Router1 to the left LAN through Router0.
8. Verify interfaces and routes, then ping between PCs on opposite LANs.

Example route patterns (replace next-hop addresses with the actual addresses used on your recreated link):

```text
! Router0: route to the remote LAN
ip route 192.168.2.0 255.255.255.0 <Router1-next-hop>

! Router1: return route to the left LAN
ip route 192.168.1.0 255.255.255.0 <Router0-next-hop>
```

## Useful Verification Commands

```text
show ip interface brief
show ip route
show running-config
ping 192.168.2.2
traceroute 192.168.2.2
```

Run the ping from a PC command prompt using the destination PC's IP address.

## Expected Results

- Router interfaces show `up/up` after correct addressing and cabling.
- `show ip route` includes the connected networks and configured static routes (marked with `S`).
- A PC on `192.168.1.0/24` can ping a PC on `192.168.2.0/24` when both directions are routed correctly.
- The first ping may time out while ARP resolution completes; repeat the test before diagnosing packet loss.

The screenshot displays successful replies after initial timeouts for the shown ping tests. This repository does not independently validate the original lab configuration.

## Important Notes

- The original `.pkt` file was not supplied.
- The next-hop placeholders must be replaced with the actual router-link addresses.
- Ensure each PC's default gateway points to its local router.
- Screenshots and labels are references, not a substitute for verifying the recreated configuration.
