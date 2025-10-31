# Google Compute Engine (GCE)

## Overview

Google Compute Engine (GCE) is Google Cloud's Infrastructure-as-a-Service (IaaS) offering for provisioning and managing virtual machine (VM) instances on Google’s global infrastructure. It supports workloads from small dev/test to large-scale, production, high-performance, and GPU workflows.

## Access Methods

- Cloud Console (Web UI)
- REST APIs
- `gcloud` CLI (`gcloud compute ...`)
- Client libraries (Python, Go, Java, etc.)

## Why Use Compute Engine

- Pay-as-you-go pricing (no upfront commitment)
- High reliability & global footprint (multi-region, multi-zone)
- Flexible performance options (machine families, custom types, GPUs)
- Easy migration from on-prem (lift-and-shift with images / import tools)

## Core Features

- VM instances (general purpose, compute optimized, memory optimized)
- Machine families: N1/N2 (general), E2 (cost-efficient), C2/C2D (compute intensive), M2 (memory), plus custom machine types
- Specialized options: Preemptible/Spot VMs (discounted, interruptible), Confidential VMs (memory encryption), GPU & accelerator VMs
- Images: Public images (Google-maintained OS) & custom images
- Persistent disks (durable block storage) + snapshots & custom images
- Load balancing (global/regional HTTP(S), TCP/UDP) & autoscaling with instance groups
- Security: IAM roles, service accounts, VPC firewall rules, VPN/Cloud Interconnect
- Global availability across regions & zones
- Integrations: Cloud Storage, Cloud SQL, GKE, Cloud Logging & Monitoring

## Common Use Cases

- Web/app hosting
- Data processing & analytics (ETL, batch jobs)
- Machine learning training/inference (GPU-accelerated)
- Development & testing environments
- High Performance Computing (HPC) / scientific simulations
- Batch processing on Spot/Preemptible VMs
- Virtual desktops / remote workstations
- Hybrid cloud extension (on-prem connectivity)

## Spot / Preemptible VMs

Provisioning model: Standard vs Spot (preemptible). Spot provides steep discounts with possible termination (approx. 30s notice). Use for stateless, fault-tolerant, checkpointed workloads.

**Options:**

- Max run duration limit
- Graceful shutdown handling (trap signals / finalize work)

## Machine Types Summary

- General Purpose: N1, N2 (balanced CPU/memory, most workloads); E2 (cost-optimized)
- Compute Optimized: C2, C2D (high vCPU performance)
- Memory Optimized: M2 (large RAM for in-memory DB, analytics)
- Custom: User-defined vCPU/RAM combinations (fit unique workloads)
- Specialized: GPU (A2, others), Confidential VMs, Spot VMs

## Storage

- Persistent Disk (pd-standard, pd-balanced, pd-ssd, pd-extreme)
- Snapshots (incremental backups)
- Images (base or customized OS templates)
- Local SSD (ephemeral, very high IOPS/low latency)
- Regional disks (replicated across zones)

## Networking

- VPC networks & subnets (regional)
- External vs internal IP addresses
- Firewall rules (ingress/egress control)
- Load balancers (HTTP(S), TCP/UDP, internal/external)
- Cloud VPN / Cloud Interconnect for hybrid connectivity

## Security & Identity

- IAM roles: granular least privilege (e.g., `compute.instanceAdmin.v1`)
- Service accounts for VM identity & API access
- VPC firewall rule hardening (restrict ports, sources)
- Confidential VMs (memory encryption) & Shielded VM features (Secure Boot, vTPM)

## Cost & Optimization

- Right-size instances (avoid over-provisioning)
- Use Spot/Preemptible for interrupt-tolerant workloads
- Select appropriate disk type (throughput vs cost)
- Autoscaling managed instance groups
- Monitor utilization (CPU, memory, disk, network) & adjust
- Consider committed use discounts (CUDs) for steady usage

## Best Practices

- Use instance templates + managed instance groups for repeatability & scaling
- Implement health checks + autohealing
- Keep OS images patched; leverage OS Config
- Use startup scripts or configuration management (Ansible, Puppet, etc.)
- Separate data from boot disk; snapshot regularly
- Tag instances and apply firewall rules via network tags
- Apply least privilege IAM to users & service accounts
- Log & monitor via Cloud Logging / Monitoring dashboards & alerts

## Quick gcloud Examples

```bash
# List zones & machine types
gcloud compute zones list
gcloud compute machine-types list --zones=us-central1-a

# Create an instance (standard)
gcloud compute instances create my-vm \
    --zone=us-central1-a \
    --machine-type=e2-medium \
    --image-family=debian-12 \
    --image-project=debian-cloud \
    --tags=http-server \
    --metadata=startup-script='#!/bin/bash; apt-get update'

# Create a Spot (preemptible) instance
gcloud compute instances create spot-vm \
    --zone=us-central1-a \
    --machine-type=e2-medium \
    --image-family=debian-12 \
    --image-project=debian-cloud \
    --provisioning-model=SPOT \
    --instance-termination-action=STOP

# Disks & snapshots
gcloud compute disks create data-disk --size=100GB --type=pd-balanced --zone=us-central1-a
gcloud compute instances attach-disk my-vm --disk=data-disk --zone=us-central1-a
gcloud compute snapshots create data-disk-snap --source-disk=data-disk --zone=us-central1-a

# Firewall rule (allow HTTP)
gcloud compute firewall-rules create allow-http --allow=tcp:80 --target-tags=http-server

# SSH into a VM
gcloud compute ssh my-vm --zone=us-central1-a
```

## Decision Guide (When to Choose GCE)

- Need OS-level control or legacy app lift-and-shift → GCE
- Containerized, stateless microservices → Cloud Run or GKE
- Managed PaaS simplicity → App Engine
- High-performance compute / GPUs → GCE specialized families
- Cost-sensitive batch → Spot VMs on GCE or Spot pods in GKE

## Summary

Compute Engine delivers flexible, global, secure VM infrastructure with granular scaling, pricing models, storage/network options, and deep integration across GCP services—enabling optimized performance and cost for diverse workloads.

Revision date: 2025-10-31
