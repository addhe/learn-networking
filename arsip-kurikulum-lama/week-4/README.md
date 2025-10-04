# 📚 Minggu 4: Layanan Jaringan

## 📋 Materi Pembelajaran

### 1. Network Address Translation (NAT)
- `praktik/nat/` - Implementasi NAT
  - Static NAT
  - Dynamic NAT
  - PAT (Port Address Translation)
  - NAT troubleshooting

### 2. Dynamic Host Configuration Protocol (DHCP)
- `praktik/dhcp/` - Implementasi DHCP
  - DHCP Server configuration
  - DHCP Relay
  - DHCP options
  - IP Helper Address

### 3. Hot Standby Router Protocol (HSRP)
- `praktik/hsrp/` - Implementasi HSRP
  - HSRP basic configuration
  - HSRP authentication
  - Load balancing dengan multiple HSRP groups
  - HSRP tracking

## 🎯 Tugas Praktik
1. [ ] Konfigurasi NAT dengan multiple inside networks
2. [ ] Setup DHCP server dengan multiple scopes
3. [ ] Implementasi HSRP dengan tracking
4. [ ] Dokumentasi dan monitoring

## 📝 Panduan Lab
Setiap praktik harus mencakup:
- Topologi jaringan dengan IP addressing
- Konfigurasi step-by-step
- Verifikasi konfigurasi
- Skenario troubleshooting

## 💻 Lab Monitoring
- `monitoring/` - Tools dan scripts untuk monitoring
  - DHCP lease monitoring
  - NAT statistics
  - HSRP state changes
  - Syslog configuration

## 🔍 Sumber Pembelajaran
- [Cisco NAT Configuration Guide](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/13772-12.html)
- [DHCP Configuration Guide](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/15-mt/dhcp-15-mt-book.html)
- [HSRP Configuration Guide](https://www.cisco.com/c/en/us/support/docs/ip/hot-standby-router-protocol-hsrp/9234-hsrpguidetoc.html)

## 💡 Tips Praktik
- Mulai dengan konfigurasi dasar sebelum fitur lanjutan
- Gunakan debugging commands untuk troubleshooting
- Dokumentasikan setiap perubahan konfigurasi
- Buat backup konfigurasi sebelum melakukan perubahan besar