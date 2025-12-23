# Migration TODO List

## Phase 0 - Preparation

- [ ] Backup OPNsense configuration
- [ ] Collect network inventory
- [ ] Export firewall rules
- [ ] Identify VPN usage

## Phase 1 - Design

- [ ] Create physical topology diagram
- [ ] Create logical topology diagram
- [ ] Map OPNsense rules to MikroTik

## Phase 2 - MikroTik Base Setup

- [ ] Update RouterOS
- [ ] Configure WAN
- [ ] Configure LAN & VLAN
- [ ] Internet connectivity test

## Phase 3 - Firewall Migration

- [ ] Create address-list
- [ ] Implement input chain rules
- [ ] Implement forward chain rules
- [ ] Logging & monitoring

## Phase 4 - NAT & Services

- [ ] Outbound NAT
- [ ] Port forwarding
- [ ] DNS & DHCP

## Phase 5 - VPN

- [ ] VPN selection
- [ ] Configure VPN
- [ ] Routing & firewall

## Phase 6 - Testing

- [ ] Internet access
- [ ] Internal communication
- [ ] VPN test
- [ ] Failover (if any)

## Phase 7 - Cut Over

- [ ] Switch gateway to MikroTik
- [ ] Monitor traffic
- [ ] Performance tuning
- [ ] Rollback validation
