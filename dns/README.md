# Proxmox: Creating a Template from Ubuntu Cloud Image

This guide outlines how to deploy a DNS server using CoreDNS and Docker.

## 🛠️ Steps

### 1. Install Docker Engine on Ubuntu
https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

### 2. Download the Ubuntu Cloud Image
```bash
wget https://cloud-images.ubuntu.com/releases/noble/release/ubuntu-24.04-server-cloudimg-amd64.img
```

### 3. Create a VM Definition
```bash
qm create 8000 --memory 4096 --name ubuntu-cloud --net0 virtio,bridge=vmbr0
```

### 4. Import the Cloud Image as a Virtual Disk
```bash
qm importdisk 8000 ubuntu-24.04-server-cloudimg-amd64.img local-lvm
```

### 5. Attach the Imported Disk to the VM
```bash
qm set 8000 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-8000-disk-0
```

### 6. Add a Cloud-Init Drive to the VM
```bash
qm set 8000 --ide2 local-lvm:cloudinit
```

### 7. Set the Boot Device to the Imported Disk
```bash
qm set 8000 --boot c --bootdisk scsi0
```

### 8. Enable Serial Console for Headless Access
```bash
qm set 8000 --serial0 socket --vga serial0
```

### 9. Configure Cloud-Init Parameters via the Proxmox GUI

In the Proxmox web interface:

1. Select the VM (ID 8000).
2. Go to the **Cloud-Init** tab.
3. Set the following parameters as needed:
   - **User** (e.g., `cloud`)
   - **Password** or **SSH Public Key**
   - **Hostname**
   - **IP Configuration** (DHCP or static)

These settings will be applied at first boot using the attached cloud-init drive.

### 10. Convert the VM to a Template

Once you've configured everything and **before starting the VM**, convert it into a reusable template:

1. In the Proxmox web interface, **right-click the VM**.
2. Select **"Convert to Template"**.

This allows you to clone new VMs from this template without redoing the setup each time.
