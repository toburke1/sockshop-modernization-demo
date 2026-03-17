# sockshop-modernization-demo
Nutanix Sock Shop Modernization Demo
Overview

This repository provides a hands-on modernization demo that partners can deploy in their own datacenter to demonstrate how Nutanix supports both virtual machines and containerized applications on the same platform.

The demo walks through a common modernization scenario:

Start with a monolithic retail application running on an Ubuntu VM

Extract the product catalog into a containerized microservice

Deploy the microservice on Nutanix Kubernetes Platform (NKP)

Demonstrate independent scaling, resilience, and service separation

This mirrors how many enterprises modernize legacy applications incrementally.

Architecture
Before Modernization
User Browser
      │
      ▼
Monolithic Application
(Ubuntu VM on AHV)
 ├ UI
 ├ Product Catalog
 ├ Cart
 └ Orders
After Modernization
User Browser
      │
      ▼
Monolithic Application (VM)
 ├ UI
 ├ Cart
 └ Orders
      │
      ▼
NKP Kubernetes Cluster
 └ Catalog Microservice
      ├ Pod
      ├ Pod
      └ Pod

This demonstrates how Nutanix can run VMs and Kubernetes workloads side-by-side.

Demo Highlights

This demo allows partners to show:

VM workloads on AHV

Containerized services on NKP

Incremental application modernization

Independent service scaling

Kubernetes load balancing

Infrastructure consolidation on Nutanix

What This Demo Deploys
Component	Platform	Description
Sock Shop Monolith	AHV VM	Retail web app running Flask
Catalog Microservice	NKP	Containerized product catalog
Kubernetes Service	NKP	Exposes the catalog API
Bastion Host	Linux	Runs kubectl for cluster operations
Repository Structure
sockshop-modernization-demo
│
├── README.md
│
├── docs
│   ├── 01-overview.md
│   ├── 02-prerequisites.md
│   ├── 03-ahv-vm-build.md
│   ├── 04-monolith-install.md
│   ├── 05-catalog-container-build.md
│   ├── 06-nkp-deploy.md
│   ├── 07-demo-walkthrough.md
│   └── 08-troubleshooting.md
│
├── monolith-vm
│   ├── app.py
│   ├── requirements.txt
│   ├── templates
│   ├── static
│   └── scripts
│
├── catalog-service
│   ├── app.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── scripts
│
├── nkp
│   ├── catalog-service.yaml
│   └── scripts
│
└── demo
    ├── demo-talk-track.md
    ├── demo-checklist.md
    └── cleanup.sh
Prerequisites

Partners will need the following environment:

Nutanix Infrastructure

Nutanix cluster with AHV

Nutanix Kubernetes Platform (NKP) installed

Access to Prism Central

Bastion host with kubectl configured

Software

Ubuntu Server ISO

Docker installed on the VM

Access to a container registry

Docker Hub

or private registry

Network

VM must reach NKP service IP

Bastion host must reach Kubernetes API

Deployment Workflow

The demo is deployed in five phases.

1. Build the Ubuntu VM

Create a VM in AHV and install Ubuntu.

Documentation:

docs/03-ahv-vm-build.md
2. Install the Monolithic Application

Install Python dependencies and run the Sock Shop monolith.

Documentation:

docs/04-monolith-install.md

Validate the application loads:

http://<vm-ip>:5000
3. Build the Catalog Microservice Container

Build the container image and push it to your registry.

Documentation:

docs/05-catalog-container-build.md
4. Deploy the Catalog Service to NKP

Deploy the Kubernetes workload from the bastion host.

Documentation:

docs/06-nkp-deploy.md

Validate:

kubectl get deployment,rs,pods -n <namespace>
5. Update the Monolith Routing

Update the monolith so /products routes to the Kubernetes service.

Restart the application and validate.

Demo Walkthrough

A complete 10-minute partner demo script is provided here:

demo/demo-talk-track.md

Typical demo flow:

Show the monolithic application running on AHV.

Explain why catalog is a good modernization candidate.

Deploy or show the containerized catalog on NKP.

Scale the catalog service.

Demonstrate load balancing across pods.

Scaling Example

Scale the catalog service to 3 pods:

kubectl scale deployment catalog-service \
--replicas=3 \
-n <namespace>

Verify:

kubectl get pods -n <namespace>
Troubleshooting

Common issues are documented here:

docs/08-troubleshooting.md

Examples include:

ImagePullBackOff

Wrong namespace

Service not reachable

Dashboard not showing workloads

Cleanup

Remove all deployed resources:

demo/cleanup.sh
Why This Demo Matters

Many customers want to modernize applications but cannot rewrite everything at once.

This demo shows how Nutanix enables:

Incremental modernization

VM and container consolidation

Unified infrastructure operations

All within the Nutanix platform.

Contributing

Partners and SEs are encouraged to:

fork this repository

submit improvements

add additional modernization scenarios

License

This project is intended for partner enablement and technical demonstrations.
