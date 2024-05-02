Proxmox full course from **LearnLinuxTV**: [link](https://www.youtube.com/playlist?list=PLT98CRl2KxKHnlbYhtABg6cF50bYa8Ulo)
Proxmox doc: [link](https://pve.proxmox.com/wiki/Main_Page)

##### QEMU-guest-agent
The qemu-guest-agent is a helper daemon, which is installed in the guest. It is used to exchange information between the host and guest, and to execute command in the guest.

In Proxmox VE, the qemu-guest-agent is used for mainly three things:
1. To properly shutdown the guest, instead of relying on ACPI commands or windows policies
2. To freeze the guest file system when making a backup/snapshot (on windows, use the volume shadow copy service VSS). If the guest agent is enabled and running, it calls _guest-fsfreeze-freeze_ and _guest-fsfreeze-thaw_ to improve consistency.
3. In the phase when the guest (VM) is resumed after pause (for example after shapshot) it immediately synchronizes its time with the hypervisor using qemu-guest-agent (as first step).

>[!Tip]- When should use Qemu Guest Agent?
The only time it's not useful is then your trying to make sure you're VM doesn't "know" it's a VM. Like when your trying to "fool" Nvidia drivers.
>
Otherwise you should always install the agent on the clients THEN check the qemu guest option on the host.
>
This all the host to request actions from the VM. From simple things like shutdown to more "extreme" things like flush the write buffer buffer and freeze and writes.

For the complete installation guide see: [link](https://pve.proxmox.com/wiki/Qemu-guest-agent)

##### Cloud-init
Tool per automatizzare il templating delle VM linux.
Creare molte vm a partire da un template necessita che alcuni elementi non siano replicati nelle varie macchine:
- chiavi ssh
- /etc/machine-id (/var/lib/dbus/machine-id should be a symbolic link to /etc/machine-id)
- cache (sudo apt clean)