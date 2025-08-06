# Ansible Monitoring Repository

This repository contains Ansible playbooks for monitoring and managing Linux VMs.

## 🚀 Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/ansible-monitoring.git
   cd ansible-monitoring
   ```

2. **Update inventory:**
   Edit `inventory/hosts.yml` with your VM details.

3. **Install dependencies:**
   ```bash
   ansible-galaxy install -r requirements.yml
   ```

4. **Test connectivity:**
   ```bash
   ansible all -m ping
   ```

5. **Run monitoring:**
   ```bash
   ansible-playbook playbooks/system-monitoring.yml
   ```

## 📁 Structure

- `inventory/` - Host definitions and variables
- `playbooks/` - Main playbook files
- `roles/` - Reusable Ansible roles
- `ansible.cfg` - Ansible configuration

## 🔧 Configuration

Update the following files for your environment:
- `inventory/hosts.yml` - VM IPs and credentials
- `inventory/group_vars/all.yml` - Global settings
- `roles/*/defaults/main.yml` - Role-specific defaults

## �� Monitoring

The system monitors:
- CPU, Memory, and Disk usage
- System load and uptime
- Security updates
- Service status

## 🚨 Alerts

Alerts are triggered when:
- CPU usage > 80%
- Memory usage > 85%
- Disk usage > 90%

## 📝 License

MIT License
