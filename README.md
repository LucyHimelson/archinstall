# archinstall
> Oh, u seem to have forgotten how to do that, silly
### Well this method includes UEFI mode only
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

