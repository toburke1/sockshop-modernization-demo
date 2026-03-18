Build the Ubuntu VM on AHV

This section walks through creating the Ubuntu VM that will host the Sock Shop monolithic application.

The VM will run the retail web application before we extract the catalog into Kubernetes.

Architecture Context

The VM represents the legacy monolithic application.
User Browser
      │
      ▼
Sock Shop Monolith
(Ubuntu VM on AHV)
      │
      ▼
NKP Kubernetes Cluster
Catalog Microservice

Step 1 — Download Ubuntu ISO

Download the Ubuntu Server ISO.

Recommended version:

Ubuntu Server 25.10 

Download from:

https://ubuntu.com/download/server

Step 2 — Upload ISO to Prism Central

Log into Prism Central

Navigate to:

Compute & Storage
→ Images

Click:

Upload Image

Configure:

Field	Value
Name	ubuntu-server
Type	ISO
Upload Method	From Local File

Upload the Ubuntu ISO.

Wait for the upload to complete.

Step 3 — Create the Virtual Machine

Navigate to:

Compute & Storage
→ VMs

Click:

Create VM
Step 4 — Configure VM Settings
General
Setting	Value
Name	sockshop-monolith
Description	Sock Shop monolithic application
Compute
Resource	Value
vCPU	4
Memory	8 GB
Disks

Add one disk.

Setting	Value
Type	Disk
Bus	SCSI
Size	40 GB
CD-ROM

Add a CD-ROM device and attach the Ubuntu ISO.

Setting	Value
Device	CD-ROM
Image	ubuntu-server
Network

Attach the VM to your network.

Setting	Value
NIC	Default subnet or lab network
Step 5 — Create and Power On VM

Click:

Save

Then power on the VM.

Open the console.

Step 6 — Install Ubuntu

Follow the Ubuntu installer.

Recommended options

Language:

English

Keyboard:

English (US)
Network

Allow DHCP to assign an IP address.

You can configure static networking later if required.

Storage

Choose:

Use Entire Disk
User Account

Create a user.

Example:

Field	Value
Name	socks
Username	socks
Password	password
SSH

Enable:

Install OpenSSH server

This allows remote access.

Step 7 — Complete Installation

Once the installation completes:

Remove the ISO from the VM.

Reboot the VM.

Step 8 — Verify SSH Access

From your bastion host:

ssh socks@<vm-ip>

Example:

ssh socks@10.38.239.44

If successful you should see:

socks@sockshop-monolith:~$
Step 9 — Update the VM

Run the following commands:

sudo apt update
sudo apt upgrade -y
Step 10 — Verify Internet Connectivity

Test internet access.

ping google.com

Test package installation.

sudo apt install curl -y
Step 11 — Confirm Environment

Verify the VM is ready.

Check OS version:

lsb_release -a

Check disk space:

df -h

Check memory:

free -m
Expected Result

You should now have a VM with:

Component	Status
Ubuntu installed	✓
SSH enabled	✓
Internet connectivity	✓
System updated	✓
