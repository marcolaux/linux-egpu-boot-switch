linux-egpu-boot-switch

# automate things with an integrated GPU and an NVIDIA / AMD eGPU

Tested Setup:
- XPS 13 9370 / Lenovo X1 Yoga
- Ubuntu 18.04 / Ubuntu 19.04 / Fedora 29
- ASUS XG Station Pro + NVIDIA GPU

Prerequirements:
- once booted connect the eGPU enclosure and authorize it (if user authentication is needed)
  > newest Ubuntu and Fedora versions with GNOME handles this via GUI
- if on NVIDIA install NVIDIA drivers

How to install this:
- find the BusID of your egpu via "lspci"
- copy everything to the appropriate directories
  - change the BusID in /etc/X11/xorg.conf.egpu
    - if on AMD, change the Driver "nvidia" to your AMD driver (eg. "amdgpu")
  - change the BusID in /usr/sbin/egpu_detect
- make /usr/sbin/egpu_detect executable
  > 'chmod +x /usr/sbin/egpu_detect'
- enable the new gpuboot service
  > 'systemctl enable gpuboot'
  
What to expect from this:
- when the GPU is connected on boot the xorg.conf will be created

- when the GPU is NOT connected on boot the xorg.conf will be removed

- so just connect / disconnect and boot and everything should be set
  - performance at the desk
  - battery life on the go
