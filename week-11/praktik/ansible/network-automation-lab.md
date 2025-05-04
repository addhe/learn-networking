# 🤖 Lab Network Automation dengan Ansible

## 📋 Tujuan Pembelajaran
1. Implementasi network automation dengan Ansible
2. Membuat playbooks untuk konfigurasi perangkat
3. Mengelola network inventory
4. Automated backup dan deployment

## 🏗 Lab Environment
```
[Ansible Control Node]
         |
    Management Network
         |
+--------+--------+--------+
|        |        |        |
[Router1] [Router2] [Switch1]
```

## 📝 Directory Structure
```
network-automation/
├── inventory/
│   ├── hosts
│   └── group_vars/
│       └── all.yml
├── playbooks/
│   ├── backup.yml
│   ├── configure_interfaces.yml
│   └── deploy_config.yml
├── templates/
│   ├── interface_config.j2
│   └── routing_config.j2
└── ansible.cfg
```

## 🛠 Basic Setup

### 1. Ansible Configuration (ansible.cfg)
```ini
[defaults]
inventory = ./inventory/hosts
host_key_checking = False
timeout = 30
```

### 2. Inventory Setup (hosts)
```ini
[cisco_routers]
router1 ansible_host=192.168.1.10
router2 ansible_host=192.168.1.11

[cisco_switches]
switch1 ansible_host=192.168.1.20

[cisco:children]
cisco_routers
cisco_switches

[cisco:vars]
ansible_network_os=ios
ansible_connection=network_cli
ansible_user=admin
ansible_ssh_pass=cisco123
```

### 3. Group Variables (group_vars/all.yml)
```yaml
---
backup_path: "./backups"
ntp_servers:
  - 10.0.0.1
  - 10.0.0.2
dns_servers:
  - 8.8.8.8
  - 8.8.4.4
```

## 📚 Playbook Examples

### 1. Backup Configuration
```yaml
---
- name: Backup Network Devices
  hosts: cisco
  gather_facts: no
  
  tasks:
    - name: Get current date
      set_fact:
        backup_time: "{{ lookup('pipe', 'date +%Y%m%d_%H%M%S') }}"
      run_once: true

    - name: Backup running config
      ios_config:
        backup: yes
        backup_options:
          filename: "{{ inventory_hostname }}_{{ backup_time }}.cfg"
          dir_path: "{{ backup_path }}"
```

### 2. Configure Interfaces
```yaml
---
- name: Configure Device Interfaces
  hosts: cisco_routers
  gather_facts: no

  tasks:
    - name: Configure interfaces
      ios_interfaces:
        config:
          - name: GigabitEthernet0/0
            description: "WAN Interface"
            enabled: true
          - name: GigabitEthernet0/1
            description: "LAN Interface"
            enabled: true
      notify: save config

  handlers:
    - name: save config
      ios_command:
        commands: write memory
```

## 🔧 Praktik Lab

### Lab 1: Basic Setup
1. [ ] Install Ansible
2. [ ] Setup inventory
3. [ ] Test connectivity
```bash
ansible all -m ping
```

### Lab 2: Configuration Management
1. [ ] Create backup playbook
2. [ ] Implement configuration templates
3. [ ] Test deployment
```bash
ansible-playbook playbooks/deploy_config.yml --check
```

### Lab 3: Automation Tasks
1. [ ] Create interface configuration playbook
2. [ ] Implement VLAN automation
3. [ ] Setup routing automation

## 🔍 Validation & Testing

### 1. Syntax Check
```bash
ansible-playbook playbook.yml --syntax-check
```

### 2. Dry Run
```bash
ansible-playbook playbook.yml --check
```

### 3. Verbose Output
```bash
ansible-playbook playbook.yml -vvv
```

## 💡 Best Practices
1. Use version control for playbooks
2. Implement idempotency
3. Use templates for configurations
4. Regular testing and validation
5. Proper error handling

## 🔐 Security Considerations
- Encrypt sensitive data dengan Ansible Vault
- Gunakan SSH keys untuk authentication
- Regular rotation dari credentials
- Limit access ke control node

## 📊 Monitoring & Logging
1. Enable Ansible logging
2. Monitor playbook execution
3. Track configuration changes
4. Setup notifications

## 📝 Documentation Requirements
- Network topology
- Inventory documentation
- Playbook descriptions
- Variable definitions
- Testing procedures

## 🎯 Success Criteria
- [ ] All playbooks successfully executed
- [ ] Configurations properly deployed
- [ ] Backup system working
- [ ] Documentation complete

## 📚 References
- [Ansible Network Documentation](https://docs.ansible.com/ansible/latest/network/index.html)
- [Cisco Ansible Modules](https://docs.ansible.com/ansible/latest/collections/cisco/ios/index.html)
- [Ansible Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)