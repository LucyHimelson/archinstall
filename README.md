# archinstall
> Oh, u seem to have forgotten how to do that, silly
### Well this method includes UEFI mode only
> [!TIP]
>You may have to use tmux and vim. Just install it now and later in chroot mode to make it easier to read a document. (vim is already installed in the ISO)
   ```
   pacman -Sy tmux --noconfirm 
   ```
> If you don't know how to use tmux, check this out **[simple-tmux](https://github.com/LucyHimelson/simpletmux)**

> Before we start, this is the easiest way for me to burn an iso

   ```
   sudo dd bs=4M if=file.iso of=/dev/sdX conv=fdatasync status=progress && sync
   ```
## Here we go

1. Check ur hard disk 

   ```
   lsblk 
   ```
   
2. We will prepare the partitions as follows

    - **boot**
    - **root**
    - **home**
    - **swap**
 
> [!NOTE]
> In addition, use any Linux partition editor you want. We usually use **cfdisk**.
 
3. Formatting Disk Partition

- > for boot 
   ```
   mkfs.fat -F32 /dev/sdXx 
   ```
- > for /root 
   ```
   mkfs.ext4 /dev/sdXx 
   ```
- > for home 
   ```
   mkfs.ext4 /dev/sdXx 
   ```
- > for swap 
   ```
   mkfs.swap /dev/sdXx 
   ```
> [!NOTE]
> For the **root** and **home** partitions, use any format u want . but who care.

4. Mount a partitions & Activate swap

- > for /root 
   ```
   mount /dev/sdXx /mnt
   ```
- > for home
  ```
   mkdir /mnt/home 
   ```
   ```
   mount /dev/sdXx /mnt/home
   ```
- > for swap 
   ```
   mkswap on
   ```
> [!IMPORTANT]
> And maybe before we start the next step, check out the changes by run **lsblk** command.

5. Install the Base and Firmware
   
   ```
   pacstrap /mnt base linux linux-firmware
   ```
   
6. Idk wat to call this step, just do it (Oh i remembered, This is to load partitions automatically upon booting)
   
   ```
   genfstab -U /mnt >> /mnt/etc/fstab
   ```
   
7. Arch-Chroot time

   ```
   arch-chroot /mnt 
   ```
> [!IMPORTANT]
> If the command fails to execute, check a previous step.

8. Set the time, key-lang, and a hostname

   ```
   In -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
   ```
   ```
   echo " en_US.UTF-8 UTF-8 >> /etc/local.gen"
   ```
   ```
   echo -e "LANG=en_US.UTF-8\nLC_COLLATE=C.UTF-8" > /etc/locale.conf"
   ```
   ```
   echo "your_hostname" > /etc/hostname
   ```
   ```
   echo -e "127.0.0.1\tlocalhost.localdomin\tarchPc" > /etc/hosts
   ```
9. Enable Network

   ```
   pacman -S networkManager --noconfirm
   ```
   ```
   systemctl enable NetworkManager
   ```
10. Set root password
   ```
   passwd
   ```
11. Installing **grub**&**EFI boot manager**
   ```
   pacamn -S grub efibootmgr --noconfirm
   ```
12. Create efi directory & mount it

- > Load the partition you previously selected for the boot
   ```
   mkdir /boot/efi && mount /dev/sdXb
   ```
13. run this
   ```
   grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB --removable && grub-mkconfig -o /boot/grub/grub.cfg && exit
   ```
14.last but not least

   ```
   umount -R /mnt & reboot
   ```
