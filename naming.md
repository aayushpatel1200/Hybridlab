# Naming Convention

## Hostnames
Each machine is named: its ROLE, then a 2-digit number.
- Uppercase, 15 characters max (a Windows limit on computer names).
- The number lets you have more than one of the same role.

Examples:
- FW01   = Firewall #01
- DC01   = Domain Controller #01
- PBS01  = Proxmox Backup Server #01
- WIN11-01 = Windows 11 client #01

## VM / Container ID numbers
Proxmox gives every VM an ID number. We pick the number so it
tells you which network (VLAN) the machine lives on.

| ID range | Lives on     |
|----------|--------------|
| 100      | FW01 (firewall) |
| 101      | BR-RTR01 (branch) |
| 110-119  | MGMT network |
| 120-129  | SERVERS network |
| 130-139  | CLIENTS network |
| 140-149  | DMZ network |
| 980-989  | TARGETS network |
| 990-999  | ATTACK network |
| 9000+    | Templates    |