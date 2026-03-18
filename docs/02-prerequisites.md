Prerequisites

Before starting the Sock Shop modernization demo, ensure the following infrastructure and software requirements are available.

This demo assumes a Nutanix environment with AHV and NKP already installed.

Environment Overview

The demo requires three systems:

System	Purpose
Ubuntu VM	Runs the Sock Shop monolithic application
NKP Kubernetes Cluster	Hosts the containerized catalog service
Bastion Host	Runs kubectl and deploys Kubernetes resources

Architecture example:
User Browser
      │
      ▼
Sock Shop Monolith
(Ubuntu VM on AHV)
      │
      ▼
NKP Kubernetes Cluster
Catalog Microservice Pods

Infrastructure Requirements
Nutanix Cluster

The Nutanix environment must include:

Nutanix AHV

Prism Central

Nutanix Kubernetes Platform (NKP) installed

Bastion host with kubectl access

Kubernetes Cluster

NKP cluster must already exist.

Verify access:
kubectl get nodes

Expected output:
NAME           STATUS   ROLES           AGE
node1          Ready    control-plane
node2          Ready    worker
node3          Ready    worker

Virtual Machine Requirements

Create an Ubuntu VM that will run the monolithic application.

Recommended VM Size:
OS: Ubuntu 25.10
CPU: 4 vCPU
RAM: 8 GB
Disk: 40 GB
Download Ubuntu ISO:

https://ubuntu.com/download/server

Install Ubuntu normally.

VM Network Requirements

The VM must be able to reach:

Kubernetes service IPs

container registry

internet for package installs

Verify connectivity:
ping <nkp-node-ip>

Bastion Host Requirements

The bastion host must have:

kubectl installed

access to the NKP cluster

network connectivity to the VM

Verify:
kubectl get nodes

Check current context:
kubectl config current-context

Example:
nkp-admin@nkp
Required Software
On Ubuntu VM

The following packages must be installable:

Software	Purpose
Python3	Run monolithic application
pip	Python package manager
venv	Virtual environment
Docker	Build catalog container image

Verify Python:

python3 --version

Verify Docker:

docker --version
Container Registry

The catalog service image must be pushed to a container registry.

Supported options:

Docker Hub

Harbor

Private enterprise registry

Example image path:

docker.io/<username>/catalog-service:v1

Verify login:

docker login
NKP Namespace

A Kubernetes namespace will be used for the demo.

Example:

sockshop-demo

Create if needed:

kubectl create namespace sockshop-demo

Verify:

kubectl get ns
Service Exposure

The catalog service must be reachable from the VM.

Two common options:

Option 1 — MetalLB (Recommended)

MetalLB assigns a service IP to the Kubernetes service.

Example:

10.38.239.80
Option 2 — NodePort

Alternatively, use NodePort.

Example access:

http://<node-ip>:<node-port>
Verify Environment Readiness

Run the following checks before starting the deployment.

Verify Kubernetes Access
kubectl get nodes
Verify Namespace Access
kubectl get ns
Verify Docker

On the VM:

docker run hello-world
Verify Network Connectivity

From the VM:

curl http://<node-ip>
Estimated Deployment Time
Phase	Time
VM creation	10 minutes
Monolith install	10 minutes
Container build	5 minutes
NKP deployment	5 minutes
Demo walkthrough	10 minutes

Total setup time:

~30 minutes
