# 🏠 Homelab Overview

## 🔧 Purpose & Use Cases

- Run and manage Proxmox VE and Kubernetes workloads.
- Host DNS services and self-developed projects (e.g., portfolio site).
- Practice infrastructure automation using Ansible and IaC principles.
- Train for cybersecurity and pentesting in an isolated environment.
- Continuously improve practical skills in virtualization, Kubernetes, and automation workflows.

## 🧱 Architecture Summary

The environment includes:
- 1 modem → 1 router → 1 managed switch.
- 5 physical servers:
  - 2 Proxmox VE hosts (clustered).
  - 2 Kubernetes worker nodes.
  - 1 "tiebreaker" node for Proxmox used also as etcd/master for Kubernetes.

---

# 🌐 Network Topology

## 📶 Internet & Routing



## 🔄 Switch & VLANs



## 💻 Server Overview

- `pve1`: Primary Proxmox VE host running all production VMs.
- `pve2`: Secondary Proxmox node used for maintenance, live-migration, and as a backup host. Restore is enabled for critical VMs. May be extended with Ceph in the future for shared storage.
- `k8s-worker1` & `k8s-worker2`: Kubernetes worker nodes running containerized workloads.
- `tiebreaker`: Lightweight control plane node for Kubernetes and serves as a Proxmox quorum/tiebreaker node to prevent split-brain in the cluster.


---

# 🖥️ Hardware Inventory

## 📦 Server Hardware

| Hostname       | CPU        | RAM   | Storage        | Role                                              |
|----------------|------------|--------|----------------|---------------------------------------------------|
| pve1           | i5-6500    | 16 GB | 256GB SSD      | Primary Proxmox VE host for VMs                   |
| pve2           | i5-6500    | 16 GB | 256GB SSD      | Secondary Proxmox node for maintenance/HA         |
| k8s-worker1    | i5-6500    | 16 GB | 256GB SSD      | Kubernetes worker node                            |
| k8s-worker2    | i5-6500    | 16 GB | 256GB SSD      | Kubernetes worker node                            |
| tiebreaker     | i5-6500    | 16 GB | 256GB SSD      | Kubernetes control plane + Proxmox quorum node    |


## 📡 Networking Equipment

| Device               | Model                 | Role                                     |
|----------------------|-----------------------|------------------------------------------|
| Modem                | Swisscom Internet-Box | ISP gateway in bridge mode               |
| Router               | TP-Link TL-R605       | Main router/firewall (Omada SDN)         |
| Managed Switch       | TP-Link TL-SG108PE    | 8-port managed switch with VLAN support  |


## 🔌 Power & UPS

- None

---

# 🧠 Virtualization & Containers

## 🧊 Proxmox VE (PVE) Nodes

Two Proxmox VE nodes (`pve1` and `pve2`) form a cluster with high availability. Storage is currently local (ZFS-backed) with plans to possibly add Ceph for shared storage in the future.

### 🔹 Hosted VMs:
- **Windows VM** – for testing software under development.
- **Linux VM** – for testing and staging Linux-based applications.
- **Backup VM** - TBD: maybe Proxmox Backup, Borg or Restic
- Additional VMs may be added as needed for experimentation and project work.

## ☸️ Kubernetes Cluster

A lightweight K3s-based Kubernetes cluster runs on `k8s-worker1`, `k8s-worker2`, and `tiebreaker` (as the control plane node).

### 🔹 Deployed Apps:
- **DNS** – internal DNS resolver (planned via CoreDNS or Pi-hole).
- **Apache** – for basic HTTP serving and testing.
- Future workloads will include more internal tools, dev services, and observability stacks.

---

# ⚙️ Services & Tools

## 🧰 Core Services (DNS, DHCP, etc.)

- **BIND** for authoritative and internal DNS resolution.
- **Pi-hole** on Docker for DNS-level ad blocking.

## 📊 Monitoring & Logging

- TBD: Searching for a lightweight Zabbix alternative

---

# 🛠️ Automation & Configuration

## 🤖 Ansible Structure



## 🗃️ IaC Repositories



## 🔁 Update & Patch Strategy

- Weekly `apt` updates via Ansible cron tasks.
- Monthly full upgrades and snapshots before major changes.

---

# 🧾 Backup Strategy

## 🎯 Backup Targets

- VMs
- Kubernetes volumes.

## 🔁 Frequency & Tools


---

# 📈 Roadmap & Lessons Learned

## 🔮 Planned Upgrades


## 📚 Key Learnings


