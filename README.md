<div align="center">

<img src="https://kubernetes.io/images/wheel.svg" align="center" width="144px" height="144px"/>

# Home Ops
[![sponsor me](https://img.shields.io/badge/sponsor-30363D?style=for-the-badge&logo=GitHub-Sponsors&logoColor=#white)](https://github.com/sponsors/simbleau)
[![buy me a coffee](https://img.shields.io/badge/Buy_Me_A_Coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/simbleau)
[![pre-commit](https://img.shields.io/badge/pre--commit-disabled-red?logo=pre-commit&logoColor=white&style=for-the-badge)](https://github.com/pre-commit/pre-commit)
[![renovate](https://img.shields.io/github/workflow/status/simbleau/home-ops/Schedule%20-%20Renovate?label=renovate&logo=renovatebot&style=for-the-badge)](https://github.com/onedr0p/home-ops/actions/workflows/)

[![internet](https://img.shields.io/uptimerobot/status/m791626909-5410cf23ca18cabcf74e32fa?color=lightgray&label=my%20home%20internet&style=flat-square&logo=opnSense&logoColor=white)](https://uptimerobot.com)
[![website](https://img.shields.io/uptimerobot/status/m791626907-5129386a08c0539012946152?logo=googlechrome&logoColor=white&color=lightgray&label=my%20website&style=flat-square)](https://spencer.imbleau.com)
[![home assistant](https://img.shields.io/uptimerobot/status/m791626943-e78c1a531a0ebfe443491da8?logo=homeassistant&logoColor=white&color=lightgray&label=my%20home%20assistant&style=flat-square)](https://www.home-assistant.io/)

</div>

---

## 📖 Overview

This is a mono repository for my home infrastructure and Kubernetes cluster. I try to adhere to Infrastructure as Code (IaC) and GitOps practices using the tools like [__Ansible__](https://www.ansible.com/), [__Terraform__](https://www.terraform.io/), [__Kubernetes__](https://kubernetes.io/), [__Flux__](https://github.com/fluxcd/flux2), [__Renovate__](https://github.com/renovatebot/renovate) and [__GitHub Actions__](https://github.com/features/actions). All tools chosen are completely free and at no cost to myself.

---

## ⛵ Kubernetes
[![K3S](https://img.shields.io/badge/k3s-v1.23-brightgreen?style=for-the-badge&logo=kubernetes&logoColor=white)](https://k3s.io/)

I run a fully conformant [__Kubernetes__](https://kubernetes.io/) cluster at home with [__K3S__](https://k3s.io/), provisioned overtop bare-metal Ubuntu 22.04 using [__Ansible__](https://www.ansible.com/). This is a semi hyperconverged cluster (HCI), with workloads and block storage sharing the same available resources from a centralized hardware RAID 5 enclosure.

### 🛠️ Core Components

- [__projectcalico/calico__](https://github.com/projectcalico/calico): Internal Kubernetes networking plugin.
- [__rook/rook__](https://github.com/projectcalico/calico): Distributed block storage for peristent storage.
- [__mozilla/sops__](https://toolkit.fluxcd.io/guides/mozilla-sops/): Manages secrets for Kubernetes, Ansible and Terraform.
- [__kubernetes-sigs/external-dns__](https://github.com/kubernetes-sigs/external-dns): Automatically manages DNS records from my cluster in a cloud DNS provider.
- [__jetstack/cert-manager__](https://cert-manager.io/docs/): Creates SSL certificates for services in my Kubernetes cluster.
- [__kubernetes/ingress-nginx__](https://github.com/kubernetes/ingress-nginx/): Ingress controller to expose HTTP traffic to pods over DNS.

### 📦 Deployment
[![ArtifactHub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/simbleau&style=for-the-badge)](https://artifacthub.io/packages/search?user=simbleau)
[![Helm](https://img.shields.io/badge/Helm-https%3A%2F%2Fsimbleau.github.io%2Fhome--ops%2Fhelm-0f1689?style=for-the-badge&logo=helm&logoColor=white)](https://simbleau.github.io/home-ops/helm)

Applications I serve from my home, including [__my website__](https://spencer.imbleau.com), are stored in a [__Helm__](https://helm.sh) registry, `https://simbleau.github.io/home-ops/helm`, deployed with [__GitHub Pages__](https://pages.github.com/). The registry is verified and traversible through [__ArtifactHub__](https://artifacthub.io/packages/search?user=simbleau).

### 🤖 GitOps

- [__Flux__](https://fluxcd.io/) watches my [__cluster__](./k8scluster/) folder and makes the changes to my cluster automatically, based on the YAML manifests.
- [__Renovate__](https://renovatebot.com/) watches my entire repository looking for dependency updates, and automatically generates PRs for them. If there are no conflicts, auto-merging is allowed.
- [__GitHub Actions__](https://github.com/features/actions) validates commits and PRs generated by checking for conflicts.

---

## 🏁 Provisioning

📙 _[__Click here__](./provision/) to see my Ansible playbooks and roles for provisioning my home infrastructure._

- [__k8s__](./provision/k8s/): Provision my kubernetes cluster.
- [__ubuntu-workstation__](./provision/k8s/): Provision my Ubuntu Workstation.

---

## 🔧 Hardware

| Device                      | Amt | OS Disk | Data Disk    | RAM   | OS           | Purpose             |
| --------------------------- | --- | ------- | ------------ | ----- | ------------ | ------------------- |
| ARRIS Surfboard SB6183      | 1   | N/A     | N/A          | 256MB | N/A          | Modem               |
| ASUS RT-AC68U               | 1   | N/A     | N/A          | 16GB  | ASUSWRT      | Router, oVPN, SMB   |
| Raspberry Pi 4B 2GB         | 1   | 32GB SD | N/A          | 2GB   | Ubuntu 22.04 | Kubernetes Master   |
| Raspberry Pi 4B 2GB         | 3   | 32GB SD | N/A          | 2GB   | Ubuntu 22.04 | Kubernetes Worker   |
| Raspberry Pi 3 Model B+     | 1   | 32GB SD | N/A          | 1GB   | Ubuntu 22.04 | Kubernetes Worker   |
| AC Infinity CLOUDPLATE T1-N | 1   | N/A     | N/A          | 64GB  | Ubuntu 22.04 | Air Cooling         |
| Kingston SATA 3 2.5" SSD    | 4   | N/A     | 240 GB       | N/A   | N/A          | SATA 3 Internal SSD |
| QNAP TR-004 4 Bay DAS       | 1   | N/A     | 720 GB RAID5 | N/A   | N/A          | RAID 5 DAS          |
| ADJ Products PC-100A PDU    | 1   | N/A     | N/A          | N/A   | N/A          | PDU                 |

---

## 🔏 License
This project is dual-licensed under both [Apache 2.0](LICENSE-APACHE) and [MIT](LICENSE-MIT) licenses.