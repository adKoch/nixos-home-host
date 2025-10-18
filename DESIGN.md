# NixOS Home Server Design

## Project Overview

Bootable NixOS configuration for a home miniPC serving as an always-on server running essential self-hosted services.

## Goals

- **Reliability**: Always-on operation with minimal maintenance
- **Reproducibility**: Declarative NixOS configuration for easy deployment/recovery
- **Simplicity**: Minimal service stack focused on core needs
- **Isolation**: Containerized services via Podman

## Services

### Audiobookshelf
- Self-hosted audiobook and podcast server
- Web interface for streaming and management
- Metadata management and library organization

### Joplin Server
- Note synchronization server for Joplin clients
- Enables cross-device note syncing
- Lightweight and efficient

## Architecture

### Container Strategy
- **Podman**: Rootless containers for security
- **systemd integration**: Native NixOS service management
- **Persistent storage**: Host-mounted volumes for data persistence

### NixOS Configuration
- **Flake-based**: Modern Nix flakes for reproducible builds
- **Minimal base**: Server-optimized NixOS installation
- **Declarative services**: All configuration in version control

## Implementation Approach

1. **Base System**: Minimal NixOS server configuration
2. **Container Runtime**: Podman with systemd quadlet integration
3. **Service Definitions**: NixOS modules for each service
4. **Storage Management**: Organized data directories with proper permissions
5. **Network Configuration**: Simple host networking with port mapping

## File Structure

```
nixos-home-host/
├── flake.nix              # Nix flake definition
├── configuration.nix      # Main NixOS configuration
├── services/
│   ├── audiobookshelf.nix # Audiobookshelf service config
│   └── joplin.nix         # Joplin server service config
└── hardware-configuration.nix
```