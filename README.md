# Ansible Network Automation

A comprehensive Ansible automation framework for managing and configuring network infrastructure including routers, switches, and core network devices.

## Overview

This project provides automated configuration and management of enterprise network devices using Ansible playbooks. It includes three main modules for system configuration, interface management, and information gathering.

## Network Topology
<img width="1301" height="850" alt="Screenshot 2026-04-02 at 6 44 53 PM" src="https://github.com/user-attachments/assets/32445d5d-533a-4a6c-b2e8-b59714a8a63e" />


## Modules

### Basic System Config
Configures fundamental device settings:
- Device hostname configuration
- NTP time synchronization
- SNMP monitoring parameters
- Device banners and login messages

Run with:
```bash
cd basic_system_config
ansible-playbook -i inventory/inventory.yml basic_system_config.yml
```

### Interface Config
Manages network connectivity and VLAN configuration:
- VLAN definitions and assignments
- Layer 2 interface configuration
- Layer 3 interface configuration with IP addresses
- Switched Virtual Interfaces (SVIs)
- Interface enable/disable operations

Run with:
```bash
cd interface_config
ansible-playbook -i inventory/inventory.yml configure_interfaces.yml
```

### Show Commands
Gathers operational information from network devices:
- Device version and system information
- Current running configuration
- IP routing table
- Interface statistics and status
- VLAN membership information

Run playbooks individually:
```bash
cd show_commands
ansible-playbook -i inventory/inventory.yml show_version.yml
ansible-playbook -i inventory/inventory.yml show_running_config.yml
```

## Managed Devices

**Core Layer:**
- CORE-RTR-A, CORE-RTR-B (Routers)
- CORE-SW-A, CORE-SW-B (Switches)

**Access Layer:**
- ACCESS-SW1, ACCESS-SW2, ACCESS-SW3 (Switches)

**ISP Connectivity:**
- ISP-RTR-A, ISP-RTR-B (Routers)

## Project Structure

```
ansible_network_automation/
├── basic_system_config/          # System configuration module
│   ├── ansible.cfg
│   ├── basic_system_config.yml   # Main playbook
│   ├── group_vars/               # Group-level variables
│   ├── inventory/                # Device inventory
│   └── task/                     # Individual tasks
│
├── interface_config/             # Interface configuration module
│   ├── ansible.cfg
│   ├── configure_interfaces.yml  # Main playbook
│   ├── host_vars/                # Host-specific variables
│   ├── inventory/                # Device inventory
│   └── tasks/                    # Interface tasks
│
├── show_commands/                # Information gathering module
│   ├── ansible.cfg
│   ├── show_*.yml                # Individual show command playbooks
│   └── inventory/                # Device inventory
│
└── ansible-venv/                 # Python virtual environment
    └── bin/                      # Ansible and tools
```

## Quick Start

1. **Activate the virtual environment:**
   ```bash
   source ansible-venv/bin/activate
   ```

2. **Update inventory files** with your network device details:
   ```bash
   nano basic_system_config/inventory/inventory.yml
   nano interface_config/inventory/inventory.yml
   nano show_commands/inventory/inventory.yml
   ```

3. **Configure variables** for your environment:
   ```bash
   # Edit group variables
   nano basic_system_config/group_vars/all.yml
   
   # Edit device-specific variables
   nano interface_config/host_vars/CORE-RTR-A.yml
   ```

4. **Run a playbook:**
   ```bash
   cd basic_system_config
   ansible-playbook -i inventory/inventory.yml basic_system_config.yml
   ```

## Requirements

- Python 3.12+
- Ansible 2.20.3+
- Netmiko 4.6.0+
- SSH access to network devices
- Cisco IOS, IOS-XE, or compatible network devices

## Variable Management

- **Group Variables** (`group_vars/`) - Applied to device groups (all, routers, switches)
- **Host Variables** (`host_vars/`) - Applied to individual devices
- **Inventory** (`inventory/inventory.yml`) - Device definitions and grouping

## Usage Examples

Run playbook against specific group:
```bash
ansible-playbook -i inventory/inventory.yml basic_system_config.yml -l routers
```

Dry run (check mode):
```bash
ansible-playbook -i inventory/inventory.yml basic_system_config.yml --check
```

Test device connectivity:
```bash
ansible all -i inventory/inventory.yml -m ping
```

## License

MIT
