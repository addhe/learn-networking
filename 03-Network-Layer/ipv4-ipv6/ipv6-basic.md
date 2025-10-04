# 🌐 Praktik Dasar IPv6

## 📋 Tujuan Pembelajaran
1. Memahami format alamat IPv6
2. Implementasi IPv6 pada router
3. Konfigurasi dual-stack (IPv4 & IPv6)
4. Verifikasi konektivitas IPv6

## 🔧 Topologi Dasar
```
[PC1-IPv6] --- [R1-DualStack] --- [PC2-IPv6]
```

## 📝 Addressing Plan
| Device | Interface | IPv6 Address          | Prefix Length |
|--------|-----------|----------------------|---------------|
| R1     | Fa0/0    | 2001:db8:acad:1::1   | /64          |
| R1     | Fa0/1    | 2001:db8:acad:2::1   | /64          |
| PC1    | NIC      | 2001:db8:acad:1::10  | /64          |
| PC2    | NIC      | 2001:db8:acad:2::10  | /64          |

## 🛠 Konfigurasi Router

### 1. Aktivasi IPv6 Routing
```cisco
R1> enable
R1# configure terminal
R1(config)# ipv6 unicast-routing
```

### 2. Konfigurasi Interface
```cisco
R1(config)# interface FastEthernet0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit

R1(config)# interface FastEthernet0/1
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# no shutdown
```

## 📋 Verifikasi Konfigurasi

### 1. Perintah Router
```cisco
show ipv6 interface brief
show ipv6 route
show ipv6 neighbors
```

### 2. Perintah PC
```bash
# Windows
ipconfig /all
ping -6 2001:db8:acad:1::1

# Linux
ip -6 addr show
ping6 2001:db8:acad:1::1
```

## 🔍 Troubleshooting
1. Verifikasi status interface
2. Cek IPv6 addressing
3. Periksa IPv6 routing
4. Test konektivitas ICMPv6

## 💡 Tips IPv6
1. Gunakan shorthand notation
2. Aktifkan IPv6 routing
3. Verifikasi Neighbor Discovery
4. Monitor ICMPv6 traffic

## 📚 Latihan Praktik

### Latihan 1: Basic Configuration
1. Konfigurasikan IPv6 pada router
2. Setup IPv6 pada PC client
3. Test konektivitas

### Latihan 2: Dual Stack
1. Tambahkan IPv4 addressing
2. Verifikasi dual-stack operation
3. Test konektivitas kedua protokol

### Latihan 3: Security Basic
1. Implementasi ACL IPv6
2. Konfigurasi basic security
3. Monitor traffic

## 📖 Referensi
- [Cisco IPv6 Configuration Guide](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipv6/configuration/15-mt/ipv6-15-mt-book.html)
- [IPv6 Addressing Architecture](https://tools.ietf.org/html/rfc4291)
- [IPv6 Subnetting](https://www.ripe.net/support/training/material/IPv6-for-LIRs-Training-Course/IPv6-Address-Planning.pdf)