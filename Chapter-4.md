# Format and Disk Space Commands

## Disk Formatting and Partitioning in Linux
From the beginning:
- Started with `fdisk`, and has been updated since for Linux
	- Now supports GUID Partition Table (GPT) format for larger disks etc.
After some evolution..:
- New commands like `mke2fs` are made
- creates `ext2` or `ext3` filesystem
	- More efficient, less data loss
Days of cloud storage & virtualization:
- Enabled use of virtual disks
- Tools like Amazon's Elastic Block Store (EBS) are made to attach virtual disks to instances

Types of partitions:
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
#note maybe in the future consider making partition for backups?
## Steps to Create Partition



## fdisk, lsblk, df, and du
#### fdisk
