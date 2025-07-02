# Constella Ansible Playbook Collection

A comprehensive collection of Ansible playbooks for network infrastructure management and Windows system administration.

## 📁 Repository Structure

```
constella-ansible-playbooks/
├── windows/                    # Windows management playbooks
├── dell-switches/             # Dell switch management playbooks  
├── inventory-templates/       # Inventory configuration templates
└── README.md                 # This file
```

## 🖥️ Windows Management Playbooks

### `get-windows-resources.yml`
Monitors Windows system resources (RAM and Storage) with specific output format.

**Output Format:**
```
-RAM part
Current RAM usage: X.XX GB
Max RAM: X.XX GB
Percentage usage: XX.XX%

-Storage part
Current Storage usage: XX.XX GB
Max Storage: XX.XX GB
Percentage usage: XX.XX%
```

**Usage:**
```bash
ansible-playbook -i inventory.ini windows/get-windows-resources.yml
```

### `get-running-services.yml`
Retrieves detailed information about running Windows services with JSON output.

**Features:**
- Lists only running services
- JSON formatted output for parsing
- Service start types and status
- Top 10 services summary

### `get-windows-services.yml`
Comprehensive Windows service information (running and stopped services).

## 🔌 Dell Switch Management Playbooks

### Core Playbooks

#### `dell_switch_vlans_final_10.0.0.5.yml`
**Primary VLAN management playbook** - Gets comprehensive VLAN information.

#### `dell_switch_interfaces_10.0.0.5.yml`
**Interface discovery playbook** - Retrieves all interface status and descriptions.

### Specialized Playbooks

#### VLAN Management:
- `dell_switch_vlans_check_10.0.0.5.yml` - Basic VLAN checking
- `dell_switch_vlans_simple_10.0.0.5.yml` - Simplified VLAN retrieval
- `dell_switch_vlans_expect_10.0.0.5.yml` - Uses expect for interaction

#### Interface Management:
- `dell_switch_basic_10.0.0.5.yml` - Basic switch information
- `dell_switch_comprehensive_10.0.0.5.yml` - Comprehensive switch data

#### Connectivity Testing:
- `dell_switch_vlans_ssh_10.0.0.5.yml` - SSH-based VLAN checking

## 📋 Inventory Templates

### `inventory_dell_10.0.0.5.ini`
Dell switch inventory configuration.

### `inventory_dell_ssh_10.0.0.5.ini`
SSH-based Dell switch configuration.

### `inventory-template.ini`
Generic inventory template for Windows systems.

## 🔧 Prerequisites

### For Windows Management:
```bash
# Ubuntu/Debian
sudo apt install python3-winrm python3-requests python3-requests-ntlm

# Windows VM Setup (Run as Administrator)
Enable-PSRemoting -Force
winrm quickconfig -force
winrm set winrm/config/service/auth '@{Basic="true"}'
winrm set winrm/config/service '@{AllowUnencrypted="true"}'
```

### For Dell Switch Management:
```bash
# Install pexpect for expect module
pip install pexpect
```

## 🚀 Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/nadzzdan/Constella.git
   cd Constella/constella-ansible-playbooks
   ```

2. **Configure inventory:**
   ```bash
   cp inventory-templates/inventory-template.ini inventory.ini
   # Edit inventory.ini with your systems
   ```

3. **Test connectivity:**
   ```bash
   # Windows systems
   ansible windows -i inventory.ini -m win_ping
   
   # Dell switches  
   ansible dell_switches -i inventory.ini -m ping
   ```

4. **Run playbooks:**
   ```bash
   # Windows resource monitoring
   ansible-playbook -i inventory.ini windows/get-windows-resources.yml
   
   # Dell switch VLAN information
   ansible-playbook -i inventory.ini dell-switches/dell_switch_vlans_final_10.0.0.5.yml
   
   # Dell switch interface information
   ansible-playbook -i inventory.ini dell-switches/dell_switch_interfaces_10.0.0.5.yml
   ```

## 📊 Tested Environment

### Target Systems:
- **Windows**: Windows Server 2019 Standard (NOC-LAB-CORE-02)
- **Dell Switch**: Dell EMC N3024ET-ON (10.0.0.5)
- **Ansible Controller**: Ubuntu 24.04.2 LTS

### Network Details:
- **Switch Model**: Dell EMC Networking N3024ET-ON
- **VLANs Configured**: 12 VLANs (Default, HR, TEST-AI_WARP, etc.)
- **Active Interfaces**: 24 Gigabit + 2 TenGig ports
- **Authentication**: SSH with username/password

## 🔒 Security Notes

- Use Ansible Vault for sensitive credentials in production
- Consider certificate-based authentication for WinRM
- Regularly rotate service account passwords
- Review firewall rules for WinRM (5985/5986) and SSH (22)

## 📈 Output Examples

### Windows Resources:
```
-RAM part
Current RAM usage: 2.53 GB
Max RAM: 4 GB
Percentage usage: 63.15%

-Storage part
Current Storage usage: 18.95 GB
Max Storage: 49.4 GB
Percentage usage: 38.35%
```

### Dell Switch VLANs:
```
VLAN   Name                    Ports          Type
-----  ---------------         -------------  --------------
1      default                 Po1-128,       Default
400    HR                      Gi1/0/2-5      Static
700    TEST-AI_WARP           Gi1/0/6-8      Static
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Test your playbooks thoroughly
4. Submit a pull request

## 📜 License

This project is open source and available under the MIT License.

## 🏷️ Tags

`ansible` `network-automation` `windows-management` `dell-switches` `infrastructure` `devops` `automation`
