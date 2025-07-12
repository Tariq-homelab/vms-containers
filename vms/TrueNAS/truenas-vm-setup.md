# Project NAS – Part 1: Setup & Storage

This phase of the project focuses on setting up a resilient, LAN-accessible NAS using Proxmox and TrueNAS SCALE in a virtualized homelab.

## Skills Gained

By completing this phase, I gained practical experience in the following areas:

- **Virtualization & Hypervisor Management**  
  Creating and configuring a TrueNAS VM in Proxmox with optimal performance settings.

- **ZFS Storage & Pool Management**  
  Creating a ZFS pool with compression and encryption, understanding VDEVs and datasets.

- **File Sharing (SMB/CIFS)**  
  Setting up user-authenticated SMB shares for reliable file access across the LAN.

- **User Access & Windows Integration**  
  Mapping network drives from Windows to TrueNAS shares with persistent authentication.

---

## Step-by-Step Setup

### 1. Enable IOMMU in BIOS and Proxmox
Ensure that virtualization and IOMMU (SVM/VT-d) are enabled in BIOS. Then, enable IOMMU on the Proxmox host to allow PCI passthrough.  
*(see Pic 1)*

### 2. Add USB Device to Proxmox VM
Attach the external hard drive to the NAS VM by passing through the USB device in Proxmox hardware settings.  
*(see Pic 2)*

### 3. Fix Boot Order if Needed
If TrueNAS fails to boot or stalls, try removing the IDE disk and re-adding it as a SATA disk in Proxmox.  
*(see Pic 3)*

### 4. Boot Into TrueNAS Installer
Launch the TrueNAS SCALE installer from the VM. Select the correct target disk and complete the installation.  
*(see Pic 4)*

### 5. Verify Disks and Select Boot Disk
Once installed, open the TrueNAS dashboard and verify that the boot disk and USB disk are both recognized.  
*(see Pic 5)*

### 5.5 Access TrueNAS Web UI and Configure Network
After reboot, log into the TrueNAS Web UI using the IP shown in the console. Configure static IP, DNS, and hostname to match your LAN plan.  
*(see Pic 6)*

### 6. Create a ZFS Pool
Create a new pool using the USB disk. Choose settings like compression (lz4) and encryption if desired.  
*(see Pic 7)*

### 7. Create a Dataset
Under the pool, create a new dataset to store files. This allows finer-grained control over permissions and sharing.  
*(see Pic 8)*

### 8. Create Local User
Create a local user that will authenticate when connecting to the SMB share from Windows.  
*(see Pic 9)*

### 9. Set Dataset Permissions
Assign the dataset's access rights to the newly created user. Set ownership and access flags properly.  
*(see Pic 10)*

### 10. Map Network Drive in Windows
On a Windows client, use File Explorer to map the network drive. Enter the TrueNAS IP and shared folder path, and authenticate using the local user.  
*(see Pic 11)*

---

## Troubleshooting: Boot Failures with OVMF

During initial setup, the TrueNAS VM failed to boot when using:

- **BIOS:** OVMF (UEFI)  
- **Machine Type:** i440fx (default)

Several attempts with these configurations led to blank screens or failure to reach the installer.

### ✅ Working Configuration (after testing)
- **BIOS:** SeaBIOS  
- **Machine Type:** q35

After switching to SeaBIOS and q35, the VM successfully reached the GRUB screen and booted into the TrueNAS installer. This configuration was used for all subsequent steps in the project.

📌 Notes:
- SeaBIOS provided better compatibility with older bootloaders.
- q35 exposes more modern PCI devices than i440fx and resolved passthrough issues.

---

## Screenshots

**Pic 1 – IOMMU Check Enabled**  
![Pic 1 – IOMMU Check Enabled](vms/TrueNAS/images/iommu-check-enabled.png)

**Pic 2 – Added USB Device**  
![Pic 2 – Added USB Device](vms/TrueNAS/images/added-usb-device.png)

**Pic 3 – Boot Troubleshoot: Remove IDE, Add SATA**  
![Pic 3 – Boot Troubleshoot Remove IDE Add SATA](vms/TrueNAS/images/boot-troubleshoot-remove-ide-add-sata.png)

**Pic 4 – GRUB Menu**  
![Pic 4 – GRUB](vms/TrueNAS/images/grub.png)

**Pic 5 – Disk Setup in TrueNAS**  
![Pic 5 – Disk Setup](vms/TrueNAS/images/disk-setup.png)

**Pic 6 – IP Config in Web UI**  
![Pic 6 – IP Config](vms/TrueNAS/images/ip-config.png)

**Pic 7 – Create ZFS Pool**  
![Pic 7 – Create Pool](vms/TrueNAS/images/create-pool.png)

**Pic 8 – Dataset Configuration**  
![Pic 8 – Datasets Config](vms/TrueNAS/images/datasets-config.png)

**Pic 9 – Local User Creation**  
![Pic 9 – Local User Create](vms/TrueNAS/images/local-user-create.png)

**Pic 10 – Set Dataset Permissions**  
![Pic 10 – Directory Permissions](vms/TrueNAS/images/directory-permissiosn.png)

**Pic 11 – Windows Mapped Network Drive**  
![Pic 11 – Map Network Drive](vms/TrueNAS/images/map-network-drive.png)
