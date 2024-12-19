
# Linux Labs

### Lab Project - 6

#### Objective:  Linux filesystem management lab 

#### DURATION: 2 - 3 Hourse

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### Lab 1: Disk Partitioning and File System Creation

####	Objective: Learn how to partition a disk, create filesystems, and mount them.
####	Task:

     1.	Partition a Disk:
      
      #  Use fdisk or parted to create partitions on a disk (e.g., /dev/sdb).
      
      #  Create a primary partition and a swap partition.
      
      #  Use lsblk and fdisk -l to confirm the new partitions.
     
     2.	Create File Systems:
      
      #  Format the partitions with different file systems (e.g., ext4, xfs, btrfs) using the mkfs command.
      
      #  Check the file system using fsck.
     
     3.	Mount Partitions:
      
      #  Mount the new partitions manually using mount (e.g., mount /dev/sdb1 to /mnt/data).

      #  Add entries to /etc/fstab to ensure automatic mounting on boot.
     
     4.	Verify and Access:
      
      #  Use df -h to check mounted file systems and disk usage.
      
      #  Access files from the new mount point and test read/write operations.

####	Outcome: 
This lab will help you gain hands-on experience in disk partitioning, file system creation, and mounting partitions on Linux.
________________________________________
#### Lab 2: Directory Structure and Permissions Management

####	Objective: Practice managing directories and controlling permissions in a Linux file system.

####	Task:
     
     1.	Create Directories:
      
      #	Use the mkdir command to create a complex directory structure (e.g., /home/user/docs, /home/user/projects).

     2.	Set Permissions:
      
      #	Use chmod to set permissions for different directories and files. For example, set read/write/execute permissions for the owner, group, and others.
      
      #	Use chown to change ownership of files and directories.

     3.	Test Directory Permissions:
 
      #	Ensure that users without proper permissions cannot access directories.

      #	Test creating, deleting, and modifying files inside these directories.

     4.	Use Access Control Lists (ACLs):

      #	Use setfacl to set additional ACLs for files and directories, allowing more fine-grained control over file access.

####	Outcome: 
This lab will help you manage directories, control access to them, and work with advanced permissions and ACLs.
________________________________________
#### Lab 3: Mounting and Using Network File Systems (NFS)

####	Objective: Set up and mount a Network File System (NFS) to share files between two Linux machines.

####	Task:

     1.	Install NFS Server:
      
      #	Install and configure the NFS server on a Linux machine using apt-get or yum.

      #	Edit /etc/exports to specify which directories are shared (e.g., /mnt/data).
     
     2.	Configure NFS Server:
      
      #  	Export the shared directory using the exportfs command.
      
      #	Start the NFS service with systemctl start nfs-server.

     3.	Mount NFS on Client:

      # 	On another Linux machine, mount the shared directory using the mount command (e.g., mount <server_ip>:/mnt/data /mnt/nfs).

     4.	Verify NFS Functionality:
     
      #	Test file creation and modification across the network to verify that NFS is functioning correctly.

####	Outcome: 
This lab will teach you how to configure and use NFS for sharing files across multiple systems, a critical task for centralized storage in Linux environments.
________________________________________
#### Lab 4: Disk Usage Analysis and Cleanup

####	Objective: Learn to analyze disk usage and clean up disk space by removing unnecessary files.

####	Task:

     1.	Check Disk Usage:
      
      #	Use the df -h command to check the disk space usage of the file system.

      #	Use du -sh <directory> to check the size of specific directories.

     2.	Find Large Files:

      #	Use find / -type f -size +100M to locate files larger than 100MB.

      #	Use ncdu to interactively view and navigate through disk usage.

     3.	Clean Up Old Files:

      #	Identify and delete unnecessary files using the rm command.

      #	Empty the trash using rm -rf ~/.local/share/Trash/*.

     4.	Automate Cleanup:
      
      #	Set up a cron job to automate cleanup tasks like deleting old log files or temporary files.

####	Outcome: 
This lab will help you manage disk usage effectively by identifying and cleaning up large or unnecessary files.
________________________________________
#### Lab 5: LVM (Logical Volume Management) Setup

####	Objective: Set up and manage logical volumes for flexible disk space management.

####	Task:

     1.	Create Physical Volume (PV):

       #	Use pvcreate to initialize a physical volume on a disk (e.g., /dev/sdb).

     2.	Create Volume Group (VG):
      
      #	Use vgcreate to create a volume group (e.g., vg_data).

     3.	Create Logical Volume (LV):
      
      #	Use lvcreate to create a logical volume from the volume group (e.g., lv_data).

     4.	Create File System:

      #	Format the logical volume with a file system (e.g., mkfs.ext4 /dev/vg_data/lv_data).

     5.	Mount and Extend Logical Volume:
     
      #   Mount the logical volume and use lvextend to increase its size as needed.

     6.	Resize File System:
      
      #	Use resize2fs or xfs_growfs to resize the file system after extending the logical volume.

####	Outcome: 
You will learn how to create, manage, and resize logical volumes using LVM, which is a flexible method for managing disk space in Linux.
________________________________________
#### Lab 6: Disk Encryption with LUKS

####	Objective: Set up disk encryption using LUKS to secure sensitive data.

####	Task:
     1.	Install Cryptsetup:
      
      #	Install cryptsetup to manage LUKS encryption.
     
     2.	Create an Encrypted Partition:
      
      #  	Use cryptsetup luksFormat /dev/sdb1 to encrypt the partition.
     
     3.	Open Encrypted Volume:
      
      #	Use cryptsetup luksOpen /dev/sdb1 encrypted_data to open the encrypted volume.
     
     4.	Create File System on Encrypted Partition:
      
      #	Format the opened volume with mkfs.ext4 or another file system.
     
     5.	Mount and Configure Auto-Mount:

      #	Mount the encrypted partition and configure /etc/crypttab for automatic unlocking during boot.

     6.	Verify Encryption:
      
      #	Test encryption by mounting the partition and ensuring data is unreadable without the correct passphrase.

####	Outcome: 
This lab will help you secure sensitive data by setting up disk encryption with LUKS, which is crucial for protecting data in transit or on disk.
________________________________________
#### Lab 7: Creating and Managing Swap Space

####	Objective: Set up and manage swap space to improve system performance, especially when physical memory is full.

####	Task:

     1.	Create a Swap Partition:

      #	Use fdisk or parted to create a swap partition.

      #	Format the partition with mkswap.
     
     2.	Enable Swap:
      
      #	Enable the swap space using swapon /dev/sdb1.
     
     3.	Add Swap to /etc/fstab:
      
      #	Edit /etc/fstab to ensure that the swap partition is mounted automatically at boot.
     
     4.	Create Swap File:
      
      #	Create a swap file using dd if=/dev/zero of=/swapfile bs=1M count=1024 and enable it using swapon /swapfile.
     
     5.	Verify Swap:

      #	Use swapon -s to verify the active swap spaces.

      #	Check system memory and swap usage using free -h.

####	Outcome: 
You will gain knowledge of how to manage swap space to optimize system performance.
________________________________________
#### Lab 8: Filesystem Repair with fsck

####	Objective: Learn how to check and repair a corrupted file system.

####	Task:

     1.	Simulate File System Corruption:
      
      #	Unmount a file system and use mount -o ro to create read-only access for a file system, simulating corruption.

     2.	Run fsck:
      
      #	Use fsck /dev/sdb1 to check and repair the file system.
     
     3.	Repair Options:
      
      #	Explore different fsck options such as -A (check all file systems) or -y (automatically fix errors).
     
     4.	Recover Lost Files:
     
      #	Use extundelete to attempt recovery of deleted files from an ext3/ext4 file system.

####	Outcome: 
You will learn how to use fsck for diagnosing and fixing file system errors.
________________________________________
#### Lab 9: File System Quotas

####	Objective: Set up and manage file system quotas to control disk space usage for users and groups.

####	Task:
     
     1.	Enable Quotas on File System:

      #	Edit /etc/fstab to enable quotas on a partition (e.g., usrquota, grpquota).

      #	Remount the file system using mount -o remount /.
     
     2.	Create and Assign Quotas:
      
      #	Use edquota to set soft and hard disk quotas for users.
     
     3.	Monitor Quotas:

      #	Use repquota to generate reports on disk usage by users and groups.
     
     4.	Test Quotas:
      
      #	Test the quotas by trying to create files that exceed the assigned limits.

####	Outcome: 
You will learn to implement and manage disk quotas to control storage usage in a multi-user environment.
________________________________________
#### Conclusion
These Linux filesystem management labs cover a wide range of essential tasks, including partitioning, mounting, disk usage analysis, file system creation, management, and troubleshooting. These labs are designed to give you practical experience with the Linux file system, which is critical for system administration and maintaining a secure and efficient storage infrastructure.



