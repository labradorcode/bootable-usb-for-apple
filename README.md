# bootable-usb-for-apple
How to create bootable USB with linux / windows for Apple iMac MacBook 

1. apt-get install mactel-boot hfsprogs gdisk grub-efi-amd64
2. cfdisk /dev/sdX
3. remove all paritions and create one
   - Parition size: 512MB
   - Primary
   - Set Type for HFS / HFS+ or "af"
   - Write and Quit
4. mkfs.hfsplus /dev/sdX1 -v Linux
5. fsck.hfsplus /dev/sdX1
6. mount -t hfsplus -o force,rw /dev/sdX1 /mnt/sdX1
7. mkdir -p "/mnt/sdX1/boot/efi/EFI/Linux/"
8. echo "This file is required for booting" > /mnt/sdX1/boot/efi/EFI/Linux/mach_kernel
9. echo "This file is required for booting" > /mnt/sdX1/boot/efi/mach_kernel
10. grub-install --target x86_64-efi --boot-directory=/mnt/sdX1/boot --efi-directory=/mnt/sdX1/boot/efi --bootloader-id="Linux"
11. hfs-bless "/mnt/sdX1/boot/efi/EFI/Linux/System/Library/CoreServices/boot.efi"
12. copy grub.cfg to /mnt/sdX1/boot/grub
13. umount /mnt/sdX1
14. fsck.hfsplus /dev/sdX1


If you want to customize you need hfsprogs
1. (debian/ubuntu) apt-get install hfsprogs
2. fsck.hfsplus /dev/sdX1
3. mount -t hfsplus -o force,rw /dev/sdX1 /mnt/target

Directories
- / root files for linux images
- boot/grub - files for grub
- boot/grub/grub.cfg - grub config

Example GRUB config in grub.cfg
