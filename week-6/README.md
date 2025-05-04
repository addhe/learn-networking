# 📚 Minggu 6: GCP Cloud Networking Lanjutan

## 📋 Materi Pembelajaran

### 1. Cloud Interconnect
- `praktik/interconnect/` - Implementasi Cloud Interconnect
  - Dedicated Interconnect
  - Partner Interconnect
  - VLAN attachments
  - BGP configuration

### 2. Shared VPC
- `praktik/shared-vpc/` - Implementasi Shared VPC
  - Host project setup
  - Service project attachment
  - IAM dan permissions
  - Network resources sharing

### 3. VPC Peering
- `praktik/vpc-peering/` - Implementasi VPC Peering
  - VPC Network Peering setup
  - Route management
  - Firewall considerations
  - Cross-project peering

### 4. Infrastructure as Code
- `terraform/` - Otomatisasi dengan Terraform
  - VPC deployment
  - Subnet creation
  - Firewall rules
  - Network peering

## 🎯 Tugas Praktik
1. [ ] Setup Shared VPC environment
2. [ ] Implementasi VPC Peering antara dua VPC
3. [ ] Konfigurasi basic Cloud Interconnect
4. [ ] Membuat Terraform script untuk network deployment

## 📝 Lab GCP
- `lab-gcp/` - Praktik dengan Google Cloud Console
  - Shared VPC configuration
  - VPC Peering setup
  - Interconnect simulation
  - IAM role assignment

## 🔍 Sumber Pembelajaran
- [Cloud Interconnect Documentation](https://cloud.google.com/network-connectivity/docs/interconnect)
- [Shared VPC Overview](https://cloud.google.com/vpc/docs/shared-vpc)
- [VPC Network Peering](https://cloud.google.com/vpc/docs/vpc-peering)
- [Terraform GCP Provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs)

## 💡 Tips Praktik
- Mulai dengan environment test/development
- Perhatikan quota dan billing
- Gunakan service account yang sesuai
- Dokumentasikan setiap konfigurasi
- Selalu backup Terraform state

## 🔧 Alat yang Dibutuhkan
1. Google Cloud SDK
2. Terraform
3. Git untuk version control
4. Text editor (VS Code recommended)
5. Draw.io untuk dokumentasi arsitektur

## 📊 Evaluasi
- Pemahaman konsep Shared VPC
- Kemampuan troubleshooting VPC Peering
- Implementasi Infrastructure as Code
- Dokumentasi yang jelas dan terstruktur