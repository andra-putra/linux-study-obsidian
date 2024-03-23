# Format and Disk Space Commands

## Disk Formatting and Partitioning in Linux
#### From the beginning:
- Started with `fdisk`, and has been updated since for Linux
	- Now supports GUID Partition Table (GPT) format for larger disks etc.
After some evolution..:
- New commands like `mke2fs` are made
- creates `ext2` or `ext3` filesystem
	- More efficient, less data loss
Days of cloud storage & virtualization:
- Enabled use of virtual disks
- Tools like Amazon's Elastic Block Store (EBS) are made to attach virtual disks to instances

#### Types of partitions:
1. Primary Partition
	1. Basic partition
	2. Can be used to boot OS from
	3. Can make max 4 primary per hard drive
		1. If want more, need to make an extended partition
2. Extended Partition
	1. Special partition used to make logical partitions
	2. Can only be made IF already 4 primary partitions on 1 disk
3. Logical Partitions
	1. Created inside extended partition
		1. Can make multiple logicals inside an extended 

Why even make partitions?
- Managing data in case data failure, data loss, OS corruption, etc.
	- Organize data into logical units
- Reduce disk fragmentation for HDD
	- Improves performance
- Isolating sensitive data on separate (secured) partitions
	- Improves security
#note maybe in the future consider making partition for backups?
## Steps to Create Partition
General steps:
1. Identify physical drive
	1. Can use `fdisk`,`lsblk`,`df`,`du`commands
2. Decide on size and location of partition
	1. Can use `fdisk` command
3. Format the filesystem
	1. Can use `mkfs` command
4. Mount the partition

Example of selecting drive, clearing partition, and making new one:
1. `lsblk` --> Checks available devices
	1. We'll use `/dev/sdb` from here on
2. `fdisk -l /dev/sdb` --> Opens fdisk utility for `/dev/sdb`
	1. `p` "Print" or display information about the selected drive
	2. `d` "Delete" the selected partition (we want to start fresh)
	3. `w` "Write" the changes onto the disk
3. `lsblk` --> Check drives again, making sure the partition is actually deleted
4. `fdisk /dev/sdb` --> Select the drive again
	1. `n` Creates "New" partition
		1. Here can choose either `p` ([[Chapter-4#Types of partitions|primary]]) or `e` ([[Chapter-4#Types of partitions|extended]])
	2. Then prompted to select amount of partitions (1-4)
	3. Then asked to remove signature (?)
	4. `w` To "write" changes on the disk
5. `fdisk -l /dev/sdb` and `lsblk` to verify changes
6. Done!


#note The choices for `fdisk` utility are [[fdisk commands|here]]
## fdisk, lsblk, df, and du
#### fdisk
Used to manage disk partitions
- Create partition tables
- Modify partition tables
- Delete partition tables
- etc.
Common command:
`fdisk -l` Lists partitions 

#### lsblk
Lists all [[block devices]].
Used to identify storage devices and details.

#### df (Disk Free)
Displays disk space used and available on filesystems.
Used to monitor filesystem usage, identifying storage space problems, etc.
e.g.
`df -h` for "human readable" file size (GB, MB, etc.)

#### du (Disk Usage)
Displays space used by directories or files.
Used to find files/directories that are hogging up space to be deleted, moved, etc.
e.g.
`du -sh` "Summarize" and "Human Readable". Displays disk usage of current directory.
`du -ah | sort -rn | head -n 10` Finds 10 largest files in this directory

## Displaying Package Space (DPKG and RPM)
