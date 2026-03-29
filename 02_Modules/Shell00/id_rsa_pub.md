---
tags: [Shell00]
---


# id_rsa_pub

## What it does
Creates and submits an SSH public key for authentication with remote servers.

## The Insight
SSH keys use asymmetric cryptography - the private key stays local, public key goes on servers. Never share your private key.

## Step-by-step Algorithm
1. Generate SSH key pair: `ssh-keygen -t rsa -b 4096 -C "email"`
2. Copy public key: `cp ~/.ssh/id_rsa.pub id_rsa_pub`
3. Submit the public key file

## The Code
```bash
# Generate SSH key pair
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Copy public key to submission location
cp ~/.ssh/id_rsa.pub id_rsa_pub
```

## SSH Key Security
| Key Type | Location | Shareable |
|----------|----------|-----------|
| Private (`id_rsa`) | `~/.ssh/` | ❌ NEVER |
| Public (`id_rsa.pub`) | `~/.ssh/` | ✅ Yes |

## Common Traps
- ❌ Sharing the private key instead of public
- ❌ Not using a strong passphrase
- ❌ Using weak encryption (less than 2048 bits)

## Related Concepts
- ssh_authentication
- asymmetric_crypto

## Propedeuticity
**Prerequisites:** None
**Unlocks:** Git clone with SSH, server access
