# 🌐 Lab OSPF: Multi-Area Configuration

## 📋 Tujuan Pembelajaran
1. Mengimplementasikan OSPF multi-area
2. Memahami konsep area backbone dan area reguler
3. Konfigurasi OSPF authentication
4. Implementasi route summarization

## 🔧 Topologi
```
                  Area 0 (Backbone)
[R1] -----------------[R2]----------------- [R3]
 |                                           |
 |                                           |
 |                                           |
[R4] -----------------[R5]----------------- [R6]
         Area 1                    Area 2
```

## 📝 Addressing Plan
| Router | Interface | IP Address     | Area    |
|--------|-----------|---------------|---------|
| R1     | Fa0/0    | 10.0.12.1/24  | Area 0  |
| R1     | Fa0/1    | 10.1.14.1/24  | Area 1  |
| R2     | Fa0/0    | 10.0.12.2/24  | Area 0  |
| R2     | Fa0/1    | 10.0.23.2/24  | Area 0  |
| R3     | Fa0/0    | 10.0.23.3/24  | Area 0  |
| R3     | Fa0/1    | 10.2.36.3/24  | Area 2  |
| R4     | Fa0/0    | 10.1.14.4/24  | Area 1  |
| R4     | Fa0/1    | 10.1.45.4/24  | Area 1  |
| R5     | Fa0/0    | 10.1.45.5/24  | Area 1  |
| R5     | Fa0/1    | 10.2.56.5/24  | Area 2  |
| R6     | Fa0/0    | 10.2.36.6/24  | Area 2  |
| R6     | Fa0/1    | 10.2.56.6/24  | Area 2  |

## 🛠 Langkah Konfigurasi

### 1. Konfigurasi Dasar Router
```cisco
! Konfigurasi untuk R1
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# interface FastEthernet0/0
R1(config-if)# ip address 10.0.12.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface FastEthernet0/1
R1(config-if)# ip address 10.1.14.1 255.255.255.0
R1(config-if)# no shutdown
```

### 2. Konfigurasi OSPF Multi-Area
```cisco
! Konfigurasi OSPF R1
R1(config)# router ospf 1
R1(config-router)# network 10.0.12.0 0.0.0.255 area 0
R1(config-router)# network 10.1.14.0 0.0.0.255 area 1
```

### 3. OSPF Authentication
```cisco
! Konfigurasi MD5 Authentication
R1(config)# interface FastEthernet0/0
R1(config-if)# ip ospf message-digest-key 1 md5 mypassword
R1(config-if)# ip ospf authentication message-digest
```

### 4. Route Summarization
```cisco
! Konfigurasi di ABR (R1)
R1(config)# router ospf 1
R1(config-router)# area 1 range 10.1.0.0 255.255.0.0
```

## 📋 Verifikasi

### 1. Periksa OSPF Neighbors
```cisco
show ip ospf neighbor
show ip ospf interface brief
```

### 2. Periksa OSPF Database
```cisco
show ip ospf database
show ip route ospf
```

### 3. Periksa Authentication
```cisco
show ip ospf interface FastEthernet0/0
```

## 🔍 Troubleshooting
1. Verifikasi status interface
2. Periksa OSPF neighbor relationships
3. Periksa area assignments
4. Verifikasi authentication settings

## 📚 Latihan Praktik

### Latihan 1: Basic OSPF
1. Konfigurasi basic OSPF di semua router
2. Verifikasi full connectivity
3. Analisis routing table

### Latihan 2: Authentication
1. Implementasi MD5 authentication
2. Test neighbor relationships
3. Verifikasi security settings

### Latihan 3: Route Optimization
1. Implementasi route summarization
2. Analisis efek pada routing table
3. Optimasi network performance

## 💡 Tips
1. Mulai dengan konfigurasi Area 0
2. Verifikasi connectivity sebelum authentication
3. Dokumentasikan setiap perubahan
4. Monitor OSPF database changes

## 📊 Evaluasi
- [ ] Full connectivity antar semua router
- [ ] OSPF neighbors established
- [ ] Authentication berfungsi
- [ ] Route summarization efektif

## 📖 Referensi
- [Cisco OSPF Configuration Guide](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/7039-1.html)
- [OSPF Design Guide](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/7039-1.html)
- [OSPF Authentication Guide](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13697-25.html)