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
