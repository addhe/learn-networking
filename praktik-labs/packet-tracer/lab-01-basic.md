# 🔧 Lab 01: Konfigurasi Dasar Jaringan

## Tujuan Lab
1. Memahami konfigurasi dasar router dan switch
2. Implementasi IP addressing
3. Verifikasi konektivitas jaringan

## Topologi
```
[PC1] --- [SW1] --- [R1] --- [SW2] --- [PC2]
```

## Kebutuhan Perangkat
- 2 Router Cisco
- 2 Switch Cisco
- 2 PC Client
- Kabel console
- Kabel ethernet

## IP Addressing
| Device | Interface | IP Address | Subnet Mask |
|--------|-----------|------------|-------------|
| R1     | Fa0/0    | 192.168.1.1| 255.255.255.0|
| R1     | Fa0/1    | 192.168.2.1| 255.255.255.0|
| PC1    | NIC      | 192.168.1.10| 255.255.255.0|
| PC2    | NIC      | 192.168.2.10| 255.255.255.0|

## Langkah Konfigurasi

### 1. Konfigurasi Router
```cisco
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# interface FastEthernet0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface FastEthernet0/1
R1(config-if)# ip address 192.168.2.1 255.255.255.0
R1(config-if)# no shutdown
```

### 2. Konfigurasi PC
- PC1:
  - IP: 192.168.1.10
  - Subnet: 255.255.255.0
  - Gateway: 192.168.1.1

- PC2:
  - IP: 192.168.2.10
  - Subnet: 255.255.255.0
  - Gateway: 192.168.2.1

## Verifikasi
1. Dari PC1:
   ```
   ping 192.168.1.1
   ping 192.168.2.10
   ```

2. Dari Router:
   ```
   show ip interface brief
   show running-config
   ```

## Troubleshooting
1. Verifikasi status interface
2. Cek IP addressing
3. Verifikasi kabel connections
4. Cek routing table

## Pertanyaan Lab
1. Apa fungsi perintah 'no shutdown'?
2. Bagaimana cara verifikasi konektivitas antar PC?
3. Apa yang terjadi jika subnet mask tidak sesuai?

## Tugas Tambahan
1. Tambahkan VLAN di switch
2. Implementasi basic security
3. Dokumentasikan konfigurasi