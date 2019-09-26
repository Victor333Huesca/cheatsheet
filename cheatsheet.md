# Cheatsheet for divers linux commands

This cheatsheet provides various of things on linux that are not used daily and
are often not easy to remember / to search for. Those things may be command
lines, basic scripts, how to with some GUI, useful programs, extensions...

Everything is grouped by topic to ease the search for a specific use-case.

## Virtualisation

### KVM/QEMU

#### From command prompt

- `virsh` is the main command when it come to visualization via **KVM**. This
  programs centralize all the visualization commands under the same interface.
  It provides a nice bash completion and the man page is well documented.
  Commands are invoked via `virsh <cmd>`.
  Note that VM are only visible by the used who started them.
  Here is a list of the main command to remember:
  - `virsh create <XML file> [--console]` this starts a VM from an XML file and
    allow to directly login via a text console.
  - `virsh destroy <VM name>` forced the VM to quit.
  - `virsh list` list the VMs that belong to the current user (and all VM in
     case of root).
  - `virsh help` for further information about **virsh**.
- `guestmount -d <domain> -i <mount point>` allows to mount a drive from virsh
   domain, the drive must be off (ie. the VM must be turned off beforehand). The
   drive will be mounted to the given mount-point with the ability to `chroot
   in`. Mounting a VM drives may help to repair it in some case (like having no
   access to the shell prompt).


## Customization

- `/etc/inputrc` and `~/.inputrc` are files to change the behavior of keys in
  the interactive shell. Here is a small example I like to use:
  ```inputrc
  # Load system-wide inputrc
  $include /etc/inputrc

  # Define custom keys
  "\C-H": backward-kill-word
  "\e[3;5~": kill-word
  ```

- `/etc/profile`, `/etc/profile.d/*.{sh,csh}` and `~/.bash_profile` are file
  sourced to provide bash customization (ie. adding variables, functions,

- `/etc/bashrc` and `~/.bashrc` are files to change the behavior of keys in


## Editing

### Nano

- `/etc/nanorc` and `~/.nanorc` are the file to edit when it come to customizing
  the default behavior of this nice editor.

- Shortcuts are indicated at the bottom of the screen, here are the most useful imo:
  - `<ctrl> + <T>`: start spell checking
  - `<ctrl> + <K>`: cut the line and add it to the buffer, don't move and
    continue to use this shortcut to add block to the buffer.
  - `<ctrl> + <U>`: paste the current buffer to the following line.
  - `<ctrl> + <L>`: enable hard-warping, the size for hard-wrap is defined in
    the nanorc file.
  - `<esc> + <T>`: remove everything starting from the current line.
  - `<esc> + <U>`: undo.
  - `<esc> + <E>`: redo.



## Adminsys

### Miscalenious

#### Full chroot from usb

In order to mount a *partition* or *image* 

```sh
mount <partition or image> /mnt
mount --bind /dev /mnt/dev
mount -t proc /proc /mnt/proc
mount --bind /run /mnt/run
mount -t sysfs /sys /mnt/sys
```


### Networking

## RedHat based distros

- In RHEL linux distributions, the network configuration uses a different
  approach from Debian linux. The network confif files are located at
  `/etc/sysconfig/network-scripts/ifcfg-<NAME>`. Each entry in this file
  represents a network interface. Here is an exemple of a basic static config:
  ```
  DEVICE=eth0
  BOOTPROTO=none
  ONBOOT=yes
  NETMASK=255.255.255.0
  IPADDR=10.0.1.27
  USERCTL=no
  ```
  Further information about this file can be found in [the fedora doc](https://docs.fedoraproject.org/en-US/Fedora/14/html/Deployment_Guide/s1-networkscripts-interfaces.html).

