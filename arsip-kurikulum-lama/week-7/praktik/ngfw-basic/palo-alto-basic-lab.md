# 🔒 Lab Palo Alto: Implementasi NGFW Dasar

## 📋 Tujuan Pembelajaran
1. Konfigurasi dasar Palo Alto NGFW
2. Implementasi security zones dan policies
3. Setup App-ID dan User-ID
4. Monitoring dan logging

## 🏗 Topologi Lab
```
Internet Zone
     |
   [NGFW]
     |
 +---+---+
 |       |
DMZ    Internal
Zone    Zone
```

## 📝 Konfigurasi Dasar

### 1. Interface Configuration
```
# Network > Interfaces
ethernet1/1:
  - Zone: internet
  - Type: Layer3
  - IP: 203.0.113.1/24
  - Virtual Router: default

ethernet1/2:
  - Zone: dmz
  - Type: Layer3
  - IP: 172.16.1.1/24
  - Virtual Router: default

ethernet1/3:
  - Zone: internal
  - Type: Layer3
  - IP: 10.0.0.1/24
  - Virtual Router: default
```

### 2. Security Zones
```
# Network > Zones
- internet (Type: Layer3)
- dmz (Type: Layer3)
- internal (Type: Layer3)
```

### 3. Security Policies
```
# Policies > Security
Rule 1: Allow Outbound
  - Source Zone: internal
  - Destination Zone: internet
  - Source Address: any
  - Destination Address: any
  - Application: web-browsing, ssl
  - Service: application-default
  - Action: allow
  - Profile Settings: default-security-profiles

Rule 2: DMZ Access
  - Source Zone: internet
  - Destination Zone: dmz
  - Source Address: any
  - Destination Address: dmz-servers
  - Application: web-browsing, ssl
  - Service: application-default
  - Action: allow
  - Profile Settings: strict-security-profiles
```

## 🛠 Langkah-langkah Implementasi

### 1. Initial Setup
1. Login ke web interface
2. Verifikasi lisensi dan updates
3. Konfigurasi management interface

### 2. Network Configuration
1. Setup interfaces
2. Buat security zones
3. Konfigurasi virtual router
4. Setup NAT (jika diperlukan)

### 3. Security Policy Implementation
1. Buat address objects
2. Definisikan applications
3. Buat security rules
4. Implementasi profiles

### 4. Monitoring Setup
1. Enable logging
2. Konfigurasi syslog
3. Setup email alerts
4. Enable threat logging

## 📋 Verifikasi

### 1. Interface Status
```
> show interface all
```

### 2. Security Policy
```
> show security-policy-rule all
```

### 3. Traffic Monitoring
```
> show session all
> show counter global filter delta yes
```

## 🔍 Troubleshooting

### 1. Connectivity Issues
```
> ping host <ip>
> traceroute <ip>
```

### 2. Policy Testing
```
> test security-policy-match
```

### 3. Traffic Analysis
```
> show log traffic
> show log threat
```

## 💡 Best Practices
1. Implementasi zero-trust model
2. Gunakan App-ID untuk kontrol
3. Enable logging untuk semua rules
4. Regular backup configuration

## 📊 Success Criteria
- [ ] Interfaces up dan running
- [ ] Security zones terkonfigurasi
- [ ] Policies berfungsi sesuai requirement
- [ ] Logging dan monitoring aktif

## 🎯 Latihan Praktik

### Lab 1: Basic Setup
1. Konfigurasi interfaces
2. Buat security zones
3. Test basic connectivity

### Lab 2: Security Policies
1. Implementasi security rules
2. Test policy enforcement
3. Verify logging

### Lab 3: Advanced Features
1. Setup App-ID
2. Konfigurasi User-ID
3. Implement security profiles

## 📚 Resources
- [Palo Alto Networks Documentation](https://docs.paloaltonetworks.com)
- [Security Best Practices Guide](https://www.paloaltonetworks.com/documentation/best-practices)
- [PAN-OS Administrator's Guide](https://docs.paloaltonetworks.com/pan-os)

## 📝 Notes
- Backup konfigurasi sebelum perubahan
- Test di lab environment dulu
- Dokumentasikan semua perubahan
- Monitor security logs