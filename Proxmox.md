

##### QEMU-guest-agent
The qemu-guest-agent is a helper daemon, which is installed in the guest. It is used to exchange information between the host and guest, and to execute command in the guest.

In Proxmox VE, the qemu-guest-agent is used for mainly three things:
1. To properly shutdown the guest, instead of relying on ACPI commands or windows policies
2. To freeze the guest file system when making a backup/snapshot (on windows, use the volume shadow copy service VSS). If the guest agent is enabled and running, it calls _guest-fsfreeze-freeze_ and _guest-fsfreeze-thaw_ to improve consistency.
3. In the phase when the guest (VM) is resumed after pause (for example after shapshot) it immediately synchronizes its time with the hypervisor using qemu-guest-agent (as first step).

For the complete installation guide see[link](https://pve.proxmox.com/wiki/Qemu-guest-agent)

