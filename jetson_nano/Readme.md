# Setup Jetson Orin Nano
## TBD

# Setup SSD 
1. Copy disk path
2. Create partition by running `sudo parted /dev/nvme0n1 mklabel gpt` in terminal. The `/dev/nvme0n1` is the path in the system to be replaced
3. In disk application of system select `+` and follow the process to create partition. Select EXT4 partition style
4. Copy the UUID of the disk
5. In terminal, create a mounting directory by runnning,
   ```
   sudo mkdir /SSD
   sudo mount /dev/nvme0n1p1 /SSD
   sudo chmod 755 /SSD
   ```
6. Create a backup of `/etc/fstab` so we can get back to it if any mess. The command is `sudo cp /etc/fstab /etc/fstab.bkup`
7. Now open the file using `sudo gedit /etc/fstab`
8. Paste the following content at the end with replacing the uuid,
   ```
   UUID=<uuid> /SSD ext4 defaults 0 2
   ```
9. Unmount and remount to check if it is working,
    ```
    sudo unmount /SSD
    sudo mount -a
    ```
10. Create symlink to access it directly from desktop using, `ln -s /SSD ~/Desktop/SSD`
