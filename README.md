guiand888.ssh_hardening
===

# Purpose
Comprehensive SSH security hardening role with two modes of operation:
- Basic SSH Security  
- Strict SSH Security Compliance (NIST SP 800-53, ANSSI recommendations)  

# Features
## Basic Hardening
- Disable root login  
- Disable password authentication  
- Prevent empty passwords  

## Strict Hardening
- Restrict SSH to administrative networks  
- Disable root login  
- Enforce key-based authentication  
- Prevent empty passwords  
- Implement group-based SSH access control  
- Enforce SSH protocol 2  
- Configure strong encryption algorithms (AES)  
- Set strict MAC algorithms (SHA2)  
- Implement session timeouts and logging  
- Disable TCP and X11 forwarding  
- Enable last log display  
- Implement brute-force protection with fail2ban  
- Enforce strict file permission checking  
- Enable privilege separation and sandboxing  

# Instructions
## Required Variables
### Basic Hardening Mode
- No explicit variables required  

### Strict Hardening Mode
- `ssh_allowed_group`: SSH access restricted to this group (default: not set)  
- `ssh_idle_timeout`: SSH session idle timeout (default: 300)  
- `ssh_idle_disconnect_threshold`: Disconnection after idle checks (default: 3)  

### Optional Variables for Fail2Ban Configuration
- `fail2ban_package_state`: Package state (default: 'present')  
- `fail2ban_service_enabled`: Enable fail2ban service (default: true)  
- `fail2ban_service_state`: Fail2ban service state (default: 'started')  
- `fail2ban_ssh_enabled`: Enable SSH jail (default: true)  
- `fail2ban_ssh_port`: SSH port to protect (default: 'ssh')  
- `fail2ban_ssh_filter`: Fail2ban filter (default: 'sshd')  
- `fail2ban_ssh_max_retry`: Maximum login attempts (default: 5)  
- `fail2ban_ssh_ban_time`: Ban duration in seconds (default: 3600)  
- `fail2ban_ssh_find_time`: Time window for retry attempts (default: 600)  

## Example Configuration
```yaml
# Strict SSH Hardening Configuration
ssh_allowed_group: ssh_admins
ssh_idle_timeout: 600
ssh_idle_disconnect_threshold: 5
```

## Example Playbook
```yaml
- hosts: servers
  roles:
    - guiand888.ssh_hardening
  vars:
    ssh_allowed_group: ssh_admins
```

## Execution
Run with tags to select hardening mode:  
- Basic: default  
- Strict: `ansible-playbook playbook.yml -t ssh_hardening_strict`  

You can select the hardening mode by setting the `ssh_hardening_mode` variable in your inventory or `group_vars`:  
- `basic`: Default, minimal security improvements  
- `strict`: Comprehensive security hardening  

For example:  
```yaml
# In inventory or group_vars
ssh_hardening_mode: strict
```

# Compatibility
- RedHat/CentOS  
- Debian/Ubuntu  

# Compliance
- NIST SP 800-53  
- ANSSI SSH Secure Use Recommendations  

# License
- GPLv3  

# Maintainers
Guillaume A.  
  - Contact: [mail@guillaumea.fr](mailto:mail@guillaumea.fr)  
  - Blog: https://blog.guillaumea.fr  
