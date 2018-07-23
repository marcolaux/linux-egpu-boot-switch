linux-nvidia-egpu-boot-switch

# automate things with an integrated GPU and an NVIDIA eGPU

EDIT: Now I am able to use the eGPU with a screen attached without further configuration and without these scripts - also expanded workspace just works. I don't really know why but Ubuntu Mainline Kernel 4.17.9 could have done the trick.

first of all: this is especially for my own setup. you would have to adjust things.

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
  > 
- when the GPU is NOT connected on boot the xorg.conf will be removed so modesetting with the intel GPU works again

- so just connect / disconnect and boot and everything should be set
  - performance at the desk
  - battery life on the go
