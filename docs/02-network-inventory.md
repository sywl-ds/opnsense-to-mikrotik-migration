# Network Inventory

## 1. Network Architecture Overview

Current network design uses a multi-router architecture:

ISP → Main Router → OPNsense (legacy) → Internal Network

After migration:

ISP → Main Router → MikroTik hEX → Internal Network

MikroTik does NOT connect directly to ISP.
It acts as a downstream gateway and security router.

## 2. Upstream Router (Main Router)

This router connects directly to ISP and provides upstream connectivity.

- Device Name : Router Utama
- Device Type : Router
- Managed By : Internal
- WAN Interface : eth1 & eth2
- WAN IP Type : Static
- LAN Interface : eth3, eth4 & eth5
- Downstream Subnet : 192.168.100.0/24

Notes:

- NAT is performed on this router
- Acts as default gateway to the internet

## 3. MikroTik Router (New Gateway)

- Device : MikroTik hEX
- RouterOS Version : v7.x
- Role : Internal Gateway & Firewall
- Position : Downstream from Main Router

### Interfaces

| Interface | Role   | IP Address       | Notes                     |
| --------- | ------ | ---------------- | ------------------------- |
| ether1    | Uplink | 192.168.100.0/24 | Connected to Main Router  |
| ether2    | LAN    | 192.168.10.0/24  | Office LAN                |
| ether3    | WIFI   | 192.168.1.0/24   | WIFI FOR LIVE TIKTO, etc. |

### Routing

- Default Gateway : IP of Main Router
- Internet Access: Via upstream router

## 4. Internal Network Segments

| Segment    | Purpose      |
| ---------- | ------------ |
| Office LAN | Office users |
| WIFI       | Live Sale    |

## 5. NAT & Routing Design

### Existing (OPNsense)

- NAT Type : Masquarade
- Default Route : Main Router
- Port Forward : No

### Planned (MikroTik)

- NAT : Yes
- Double NAT : Yes
- Default Route : Main Router IP

## 6. Network Services

### DHCP

- DHCP Server Location : Main Router
- DHCP Scope per VLAN : No

### DNS

- DNS Resolver : Mikrotik
- Forwarders : ISP

## 7. Security Zones

| Zone         | Description         | Access Policy |
| ------------ | ------------------- | ------------- |
| WAN-UPSTREAM | Main Router Network | Restricted    |
| LAN          | Internal users      | Full          |
| WIFI         | Wireless network    | Internet only |

## 8. Dependency & Risk Notes

- Internet availability depends on upstream router
- Firewall rules must consider upstream NAT
- Port forwarding requires configuration on:
  - Main Router
  - MikroTik
- Monitoring visibility limited if upstream router unmanaged
