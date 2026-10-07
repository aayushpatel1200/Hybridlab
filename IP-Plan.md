## How addressing works here
Every VLAN is a /24 (254 usable hosts). Within each VLAN the last
number (the "host" part) follows the same convention, so any address
is self-describing:

| Range      | Meaning                          | Example        |
|------------|----------------------------------|----------------|
| .1         | Firewall = default gateway       | 10.10.20.1     |
| .2 - .3    | Reserved for a 2nd firewall (HA) | --             |
| .10 - .49  | Manually assigned servers        | 10.10.20.10    |
| .100 - .199| DHCP pool (auto, temporary VMs)  | 10.10.30.100   |

## Server addresses (manually assigned)
| Host     | Role                        | VLAN | IP address  |
|----------|-----------------------------|------|-------------|
| PBS01    | Backup server               | 10   | 10.10.10.10 |
| MON01    | Monitoring (Grafana)        | 10   | 10.10.10.11 |
| SIEM01   | Security monitoring (Wazuh) | 10   | 10.10.10.12 |
| DC01     | Domain controller / DNS     | 20   | 10.10.20.10 |
| SYNC01   | Entra identity sync         | 20   | 10.10.20.11 |
| DOCKER01 | App host / reverse proxy    | 40   | 10.10.40.10 |

## Point-to-point links between routers
Each link is a /30 (only 2 usable addresses, one per router).

| Link                   | Subnet         | Addresses                    |
|------------------------|----------------|------------------------------|
| Firewall <-> Branch    | 10.255.0.0/30  | Firewall .1, Branch .2       |
| Firewall <-> AWS (VPN) | 10.255.1.0/30  | Firewall .1, AWS router .2   |
| Remote admin VPN       | 10.255.10.0/24 | VPN clients                  |

## Router IDs (unique label per router for OSPF/BGP)
| Router        | Router ID     |
|---------------|---------------|
| FW01          | 10.255.255.1  |
| BR-RTR01      | 10.255.255.2  |
| CLOUD-RTR01   | 10.255.255.3  |

## BGP autonomous system numbers (private range)
| Network | ASN   |
|---------|-------|
| Lab     | 65010 |
| AWS     | 65050 |