# 🔢 Latihan Perhitungan Subnetting

## 📋 Latihan 1: Subnetting Dasar

### Soal 1
Diberikan network address: 192.168.1.0/24
Buatlah 4 subnet yang sama besar.

#### Jawab:
1. Tentukan jumlah bit yang diperlukan: 2 bit (untuk 4 subnet)
2. Subnet mask baru: /26 (24 + 2)
3. Subnet yang terbentuk:
   - Subnet 1: 192.168.1.0/26 (0-63)
   - Subnet 2: 192.168.1.64/26 (64-127)
   - Subnet 3: 192.168.1.128/26 (128-191)
   - Subnet 4: 192.168.1.192/26 (192-255)

## 📋 Latihan 2: VLSM (Variable Length Subnet Mask)

### Soal 2
Network address: 172.16.0.0/16
Kebutuhan:
- Subnet A: 1000 host
- Subnet B: 500 host
- Subnet C: 250 host
- Subnet D: 100 host

#### Jawab:
1. Urutkan kebutuhan host dari terbesar:
   - Subnet A: 1000 host → /22
   - Subnet B: 500 host → /23
   - Subnet C: 250 host → /24
   - Subnet D: 100 host → /25

2. Alokasi subnet:
   - Subnet A: 172.16.0.0/22
   - Subnet B: 172.16.4.0/23
   - Subnet C: 172.16.6.0/24
   - Subnet D: 172.16.7.0/25

## 📋 Latihan 3: Praktik Real-World

### Soal 3
Desain jaringan untuk sebuah kantor dengan:
- Departemen IT: 100 host
- Departemen Finance: 50 host
- Departemen HR: 30 host
- Departemen Marketing: 60 host

Network address yang tersedia: 192.168.0.0/24

#### Jawab:
[Tempat untuk mengisi jawaban]

## 💡 Tips Subnetting
1. Selalu mulai dengan menghitung kebutuhan host
2. Gunakan VLSM untuk efisiensi alamat IP
3. Dokumentasikan setiap perhitungan
4. Verifikasi range IP setiap subnet
5. Pastikan tidak ada overlap

## ✅ Verifikasi
Untuk setiap subnet, tentukan:
1. Network address
2. Broadcast address
3. Range IP yang bisa digunakan
4. Subnet mask dalam format:
   - Decimal (255.255.255.0)
   - CIDR (/24)
   - Binary