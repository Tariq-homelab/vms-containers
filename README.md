# Homelab – VMs and Containers

This repository tracks the base installation and configuration of all VMs and containers used in my homelab.

Each entry includes:
- Purpose of the VM or container
- OS used and basic specs
- One or two screenshots (boot screen, terminal, desktop)
- A link to the full project repository (if applicable)

This repo serves as a visual and technical index of all infrastructure components.

## Installed Systems

| Name               | Type      | OS/Platform     | Purpose                | Linked Project                                      |
|--------------------|-----------|------------------|-------------------------|-----------------------------------------------------|
| Debian VPN VM       | VM        | Debian 12         | WireGuard VPN server     | [debian-wireguard](./debian-wireguard/README.md)   |
| Windows Server 2022 | VM        | Windows Server    | Active Directory test    | [winserver2022](./winserver2022/README.md)         |
| Ubuntu Monitor VM   | VM        | Ubuntu Server     | Monitoring & Logging     | [project-monitoring](https://github.com/Tariq-homelab/project-monitoring) |
| TrueNAS VM          | VM        | TrueNAS SCALE     | ZFS file server          | [truenas](https://github.com/Tariq-homelab/vms-containers/tree/master/truenas)                     |

