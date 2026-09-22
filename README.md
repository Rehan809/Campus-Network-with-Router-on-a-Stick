# Campus-Network-with-Router-on-a-Stick

A Cisco Packet Tracer campus-network lab built to practice VLAN segmentation, inter-VLAN routing, trunking, DHCP, WAN connectivity, ACL-based traffic control, static routing, and NAT/PAT.

## Project overview

I designed a campus network with separate VLANs for Administration, IT, Accounts, and Students. The network uses a Cisco switch and a router configured with Router-on-a-Stick for inter-VLAN routing. A /30 WAN link connects the campus router to an ISP router, and a simulated Internet Server is used for end-to-end testing.

The lab is intentionally built as a practical, troubleshooting-focused project rather than just a configuration exercise.

## Architecture

```text
Admin / IT / Accounts / Students
              |
          Switch0
       802.1Q trunk
              |
       Campus Router1
       /             \
  VLAN gateways       WAN
                 10.0.0.1/30
                       |
                 ISP Router0
                       |
                 Internet Server
                    8.8.8.8
```

See the visual diagram in [`docs/campus-network-diagram.png`](docs/campus-network-diagram.png).

## Repository structure

```text
campus-multi-vlan-network/
├── README.md
├── .gitignore
├── configs/
│   ├── switch0-config.txt
│   ├── campus-router-config.txt
│   ├── isp-router-config.txt
│   └── internet-server-config.txt
├── docs/
│   ├── campus-network-diagram.png
│   └── troubleshooting.md
```

## VLAN and IP plan

| VLAN | Department | Network | Gateway |
|---|---|---|---|
| 10 | ADMIN | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT | 192.168.20.0/24 | 192.168.20.1 |
| 30 | ACCOUNTS | 192.168.30.0/24 | 192.168.30.1 |
| 40 | STUDENTS | 192.168.40.0/24 | 192.168.40.1 |

### WAN

- Campus Router1 G0/1: `10.0.0.1/30`
- ISP Router0 G0/0: `10.0.0.2/30`

### Simulated Internet

- ISP Router0 G0/1: `8.8.8.1/24`
- Internet Server: `8.8.8.8/24`
- Server gateway: `8.8.8.1`

## Main features

- VLAN-based department segmentation
- Access-port assignment
- 802.1Q trunking
- Router-on-a-Stick inter-VLAN routing
- DHCP for client addressing
- ACL-based selection/segmentation
- Point-to-point /30 WAN link
- Default route toward the ISP
- NAT/PAT for internal networks
- ISP return routes
- End-to-end connectivity testing
- Basic L1/L2 troubleshooting workflow

## Configuration files

The `configs/` directory contains clean configuration references for:

- `switch0-config.txt`
- `campus-router-config.txt`
- `isp-router-config.txt`
- `internet-server-config.txt`

The commands are documented separately so the repository can be understood without opening Packet Tracer.

## Verification commands

Useful commands used during the lab:

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show ip dhcp binding
show access-lists
show ip nat translations
show ip nat statistics
ping <destination>
traceroute <destination>
```

## Testing

The final lab was tested in stages:

1. PC-to-default-gateway connectivity
2. Inter-VLAN gateway connectivity
3. Campus-to-ISP WAN connectivity
4. Campus-router-to-server connectivity
5. PC-to-server end-to-end connectivity
6. NAT/PAT translation verification

## Results

The project description uses the following claims:

- 20+ simulated users
- ~99% successful end-to-end connectivity in testing
- ~95% reduction in unauthorized access attempts

## Skills demonstrated

**Networking:** VLAN, trunking, inter-VLAN routing, Router-on-a-Stick, DHCP, IPv4 subnetting, static/default routing, WAN, NAT/PAT, ACLs.

**Troubleshooting:** interface status, VLAN/trunk validation, gateway testing, route-table inspection, NAT translation checks, and end-to-end connectivity testing.

## Tools

- Cisco Packet Tracer
- Cisco IOS CLI
- Git / GitHub