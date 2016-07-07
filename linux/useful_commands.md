## Hardware

* **inxi -Fx** - Nicely formatted list of hardware
* **sudo sh -c "echo 1 > /sys/bus/pci/rescan"** - Rescan pci bus for hardware

## Misc

* **$(dd if=/dev/urandom bs=1 count=32 2>/dev/null | base64 | tr -d '\n')** - Base64 Hash

## Network

* **netstat -ltun** - Show all listening ports (tcp & udp)

## KVM

* Thin Provision Virtual Disk - **virt-sparsify -q <image_name> <new_image_name>**
* Set static ip address for VM
** **virsh  net-list** - Get name of virtual network.
** **virsh  net-edit  <NETWORK_NAME>** - Edit the xml config file.
** Modify /network/ip/dhcp/range to start at .100 to stop any conflicts.
** Then under /network/ip/dhcp add as many <host mac='' name='' ip='' /> as you need.
