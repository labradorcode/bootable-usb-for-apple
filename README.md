# bootable-usb-for-apple
Image of bootable USB with GRUB for Apple Mac


Load image to USB flash drive
1. cfdisk /dev/sdX
2. delete all partitions and create one of 512M size
2. gunzip -c /path/to/usb.img.gz | dd of=/dev/sdX

If you want to customize you need hfsprogs
1. (debian/ubuntu) apt-get install hfsprogs
2. fsck.hfsplus /dev/sdX1
3. mount -t hfsplus -o force,rw /dev/sdX1 /mnt/target

Directories
- / root files for linux images
- boot/grub - files for grub
- boot/grub/grub.cfg - grub config

Example GRUB config in grub.cfg
