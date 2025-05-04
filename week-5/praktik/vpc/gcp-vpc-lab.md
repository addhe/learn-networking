# 🌐 Lab GCP: VPC dan Security Implementation

## 📋 Tujuan Pembelajaran
1. Membuat dan mengkonfigurasi VPC di GCP
2. Implementasi subnet dan IP addressing
3. Konfigurasi firewall rules
4. Setup routing dan network tags

## 🏗 Arsitektur Lab
```
                   Internet
                      |
                [Cloud NAT]
                      |
    +----------------[VPC]----------------+
    |                 |                  |
[Public Subnet]  [Private Subnet]    [Management Subnet]
   10.0.1.0/24    10.0.2.0/24         10.0.3.0/24
    |                |                     |
 [Web Server]    [App Server]         [Jump Host]
```

## 📝 Resource Planning
| Resource | Name | Spesifikasi |
|----------|------|-------------|
| VPC | prod-vpc | Auto mode: Disabled |
| Subnet Public | public-subnet | Region: asia-southeast1 |
| Subnet Private | private-subnet | Region: asia-southeast1 |
| Subnet Management | mgmt-subnet | Region: asia-southeast1 |
| Firewall Rules | allow-ssh | Allow SSH from management |
| Cloud NAT | prod-nat | Auto-allocation |

## 🛠 Implementasi dengan Terraform

### 1. Provider Configuration
```hcl
provider "google" {
  project = "your-project-id"
  region  = "asia-southeast1"
}

# VPC Configuration
resource "google_compute_network" "vpc" {
  name                    = "prod-vpc"
  auto_create_subnetworks = false
}

# Subnet Configuration
resource "google_compute_subnetwork" "public" {
  name          = "public-subnet"
  ip_cidr_range = "10.0.1.0/24"
  network       = google_compute_network.vpc.id
  region        = "asia-southeast1"
}
```

### 2. Firewall Rules
```hcl
resource "google_compute_firewall" "allow_ssh" {
  name    = "allow-ssh"
  network = google_compute_network.vpc.id

  allow {
    protocol = "tcp"
    ports    = ["22"]
  }

  source_ranges = ["10.0.3.0/24"]
  target_tags   = ["ssh-allowed"]
}
```

## 📋 Lab Tasks

### Task 1: VPC Setup
1. [ ] Create VPC network
2. [ ] Configure subnets
3. [ ] Verify network creation

### Task 2: Security Implementation
1. [ ] Configure firewall rules
2. [ ] Setup network tags
3. [ ] Test connectivity

### Task 3: Network Services
1. [ ] Configure Cloud NAT
2. [ ] Setup Cloud Router
3. [ ] Verify outbound connectivity

## 🔍 Verification Steps

### 1. Subnet Verification
```bash
gcloud compute networks subnets list --network=prod-vpc
```

### 2. Firewall Rules Check
```bash
gcloud compute firewall-rules list --filter="network=prod-vpc"
```

### 3. Connectivity Testing
```bash
# From Jump Host to App Server
ssh user@app-server-internal-ip

# Test outbound connectivity
curl -v https://www.google.com
```

## 💡 Best Practices
1. Gunakan network tags untuk firewall management
2. Implementasi principle of least privilege
3. Dokumentasikan setiap firewall rule
4. Gunakan meaningful naming conventions

## 🔐 Security Considerations
- Restrict IP ranges in firewall rules
- Use service accounts appropriately
- Enable VPC Flow Logs
- Implement proper IAM roles

## 📊 Monitoring Setup
1. Enable VPC Flow Logs
2. Configure Cloud Monitoring
3. Setup alerting policies
4. Monitor network usage

## 📝 Documentation Requirements
- Network diagram
- IP address allocation
- Firewall rules documentation
- Access procedures

## 🎯 Success Criteria
- [ ] VPC dan subnet terkonfigurasi
- [ ] Firewall rules berfungsi
- [ ] Cloud NAT operational
- [ ] Connectivity terverifikasi

## 🔍 Troubleshooting Guide
1. Check subnet ranges
2. Verify firewall rules
3. Test connectivity paths
4. Review Cloud NAT logs

## 📚 References
- [VPC Network Overview](https://cloud.google.com/vpc/docs/vpc)
- [Cloud NAT Overview](https://cloud.google.com/nat/docs/overview)
- [Firewall Rules](https://cloud.google.com/vpc/docs/firewalls)
- [Best Practices](https://cloud.google.com/vpc/docs/vpc-best-practices)