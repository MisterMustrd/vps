# vps
Infrastructure documentation for my personal Ubuntu VPS, this includes networking, security, Docker, and self-hosted services.

## Project Goals
- This was created to build hands-on experience with Linux system administration, networking, Docker, and self-hosting. 
- The VPS serves as the core of my personal infrastructure and provides secure access / shared services for my homelab.
- Learn Docker and Docker Compose by deploying and managing services.
- Improve networking knowledge through DNS, VPN, and firewall configuration.
- Practice securing a server using SSH, Tailscale, and firewall rules.

## Environment
- Ubuntu Server 24.04 LTS
- Docker & Docker Compose
- Hosted on an Cloud Provider VPS

## Core Services

The VPS hosts several containerized services that provide networking, monitoring, secure remote access, and self-hosted applications.

### Bare Metal
- Pi-hole: Network-wide DNS
- Unbound: Recursive DNS resolver 
- Cloudflared: DNS-over-HTTPS fallback resolver.
- Tailscale: Mesh VPN


### Docker
- Netdata: Monitoring of system performance, resource usage, and running services.
- Watchtower: Automatic Docker container updates.
- SMB Share: To provide access to shared files.
- FileStash: Browser-based file management.
- Gluetun: VPN gateway

- Invidious: Privacy-focused YouTube frontend.
- Redlib: Privacy-focused Reddit frontend.


## Network

The VPS serves as the central networking hub for my self-hosted environment. 
It provides private remote access, DNS resolution, and containerized services while minimizing public exposure.

Key components:
- Tailscale for secure connection to other devices on network  
- Pi-hole for network DNS filtering and ad blocking.
- Unbound as a local DNS resolver for improved privacy and reliability.
- Cloudflared as a fallback DNS.
- Docker for running and isolating services on dedicated networks.
- Gluetun to isolate selected Docker containers through a VPN.
- iptables firewall rules to restrict access to services and limit exposure to the public internet.


### DNS Flow
Client >> Pi-hole >> Unbound >> DNS Root Servers
                  >> (fallback) >> Cloudflared >> Cloudflare DNS



## Security

I avoid exposing services directly to the internet, so I use multiple layers of protection to reduce unnecessary access.

Key Components:
- SSH key-based authentication for remote administration.
- iptables firewall rules including restricting access to devices connected to my private Tailscale network. 
- Docker network isolation where appropriate.
- Gluetun to route selected containers through a VPN.
- Regular system and container updates to keep software current.



## Docker Infrastructure

Apart from my DNS Chain, Docker is used to host and manage the services running on the VPS. 
Each application runs in its own container with persistent storage to preserve data across updates and restarts.

My Docker environment includes:

- Docker Compose to define and manage multi-container applications.
- User-defined Docker networks to isolate services and control communication.
- Configuration files organized into separate directories for easier maintenance and deployment.


## Storage

The VPS uses local storage for the operating system, Docker volumes, and application data. 
Docker volumes are used to ensure data is retained across container updates and restarts.

Additional storage is provided through a network-mounted share from my homelab to keep major storage centralized.

