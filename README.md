linux-nvidia-egpu-boot-switch

# automate things with an integrated GPU and an NVIDIA eGPU

This repo is for people who use an external NVIDIA GPU with an NVIDIA driver that's not configured with the "AllowExternalGpus" X server flag by default.
For example the default Ubuntu 18.04 NVIDIA driver 3.90 is configured with that flag and no further configuration is required. Just install the NVIDIA driver and you are good to go.
Since I updated to the 3.96 driver from the "graphics-drivers" ppa I wasn't able to use the external GPU by default and had to use a custom xorg.conf with the "AllowExternalGpus" flag enabled. The scripts in this repo take care of changing the the xorg.conf file on boot when the eGPU is connected. Sure there won't be any hotplugging support but the NVIDIA driver does not support that anyway (why the flag "AllowExternalGpus" exists and is disabled by default - to prevent further crashes).

first of all: this is especially for my own setup. you would have to adjust things (for example the PCI-BUS ID in the xorg.conf file).

Setup:
- XPS 13 9370
- Ubuntu 18.04
- ASUS XG Station Pro + NVIDIA GPU

Prerequirements:
- eGPU with display attached
- UEFI:
  > enable Thunderbolt Boot support (pre-boot support is not needed)
- once booted connect the eGPU enclosure and authorize it (if user authentication is needed)
  > newest Ubuntu and Fedora versions with GNOME handles this via GUI
- install NVIDIA drivers
- disable gpu-manager (Ubuntu only)
  > 'systemctl disable gpu-manager'

How to install this:
- copy everything to the appropriate directories
- make /sbin/nvidia_egpu_detect bootable
  > 'chmod +x /sbin/nvidia_egpu_detect'
- enable the new gpuboot service
  > 'systemctl enable gpuboot'
  
What to expect from this:
- when the GPU is connected on boot the xorg.conf will be created

- when the GPU is NOT connected on boot the xorg.conf will be removed so modesetting with the intel GPU works again

- so just connect / disconnect and boot and everything should be set
  - performance at the desk
  - battery life on the go
