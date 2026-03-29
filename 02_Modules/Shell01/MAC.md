---
tags: [Shell01]
---


# MAC

## What it does
Displays the MAC address of the primary network interface.

## The Insight
Parses `ifconfig` output or reads from `/sys` to extract the MAC address.

## The Code
```bash
#!/bin/sh
ifconfig | grep 'ether ' | awk '{print $2}'
```

## Command Breakdown
| Command | Purpose |
|---------|---------|
| `ifconfig` | Network interface configuration |
| `grep 'ether '` | Filter for MAC line |
| `awk '{print $2}'` | Print second field (the address) |

## Common Traps
- ❌ Hardcoding interface name (eth0 vs en0)
- ❌ Not handling multiple interfaces
- ❌ Using case-sensitive matching incorrectly

## Related Concepts
- network_interfaces
- mac_address

## Propedeuticity
**Prerequisites:** Shell00, basic grep/awk
**Unlocks:** Network diagnostics
