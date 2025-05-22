> [!info] This machine was using Ubuntu 24 and ext4, with also a LVM (Logical Volume Manager) and your root (`/`) filesystem on a logical volume (`ubuntu--vg-ubuntu-lv` inside `/dev/sda3`)

## Step 1: Increase Disk Size in Proxmox (VM Level)

1. **Open Proxmox Web UI**.
2. Go to `Datacenter > node > VM > Hardware`.
3. Select the **disk** you want to resize (e.g., `scsi0`, `virtio0`, etc.).
4. Click **"Resize disk"** (top menu).
5. Enter the amount to increase (e.g., `+20G`).
6. Click **"Resize disk"**.

## Step 2: Resize Partition in Linux

You're resizing the physical partition (`/dev/sda3`) to include the new space.
#### 1. Check current layout:

```shell
lsblk
	sda
	├─sda1       (EFI or boot)
	├─sda2       /boot
	└─sda3       part of LVM group "ubuntu--vg"
```


#### 2. Resize partition (safely) with `growpart`

```shell
sudo apt install cloud-guest-utils 
sudo growpart /dev/sda 3
```


## Step 3: Resize the LVM Physical Volume

Now tell LVM to use the new space in `/dev/sda3`.

```shell
sudo pvresize /dev/sda3
```

