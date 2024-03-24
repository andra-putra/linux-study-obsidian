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
Tools like `dpkg` (Debian-based) and `rpm` (RHEL based) used to install, view, check out info about software packages. 
Other uses:
- Look at disk space used by installed packages. 
- Look at info about package dependencies
	- Check which packages can be removed without breaking other stuff
- Update or install packages along with dependencies

Examples using [[rpm]]:
`rpm -i /path/to/file.rpm` --> "Installs" a local `.rpm` package file into the system
`rpm -qi packagename` --> "Queries" the details of a package installed on the system

## Disk Formatting Commands (mkfs, mk3fs, fdformat, etc.)
To prep disk for file storage, first need to format it.

#### mkfs (Make Filesystem)
Tool to make filesystem on storage device (HDD, USB drives, etc.)
Can make ext2, ext3, ext4, XFS, btrfs, etc. filesystem types.
Usually when you add a new HDD into a Linux system, you'd first format it using this tool.
e.g.
`mkfs.ext4 /dev/sdb1` --> Formats /dev/sdb1 partition with ext4 filesystem. After this, it can be mounted and used

#### mke2fs
Variant of `mkfs` to make ext2, ext3, and ext4 filesystems.
#note Find the difference between the different ext types later
e.g.
`mke2fs -t ext3 /dev/sdb1` --> Creates ext3 filesystem on /dev/sdb1 partition

#### fdformat (Floppy Disk Format)
To format floppy disks. Different tool since this is more low-level apparently. 
Don't use it for USB drives and such.

#### mkswap
Used to make [[swap area]] on Linux systems.
Initializes disk partition or file as swap area, then assigns unique identifier.
e.g. step by step
1. `lsblk` --> Check available disk partitions
	1. "Ok, I want to make /dev/sdb1 as SWAP area now."
2. `mkswap /dev/sdb1` --> Formats partition as swap area

### gdisk
Used to partition hard drives on Linux systems.
Designed for the [[GPT partitioning scheme]].
e.g.
- `gdisk /dev/sdb` --> Launches the gdisk util for specified disk
	- `n` --> "New" partition is made
	- Follow the promps here for different settings, then `w` to "write" changes to disk

## parted
Partition editor to modify partitions.
Supports [[GPT partitioning scheme|GPT and MBR]] and can work with different filesystem types.
Commonly used for servers.
e.g. want to make new partition on /dev/sdb disk
1. `parted /dev/sdb` --> Launch parted util on specified disk
2. `mklabel gpt` --> Makes new GPT partition table on disk (to ensure compatability with modern systems and larger disk sizes)
3. `mkpart primary ext4 0% 100%` --> Make new primary partition that spans 100% of the disk using ext4 filesystem
4. `print` --> Verify partition layout and details
5. `quit` --> Quits parted utility

## dd
Low-level tool to copy/convert data between files, disks, and partitions.
Common uses:
- Making bootable USB drives
- Backing up and restoring disk images
- Cloning disks
- Write zeroes to hard drive (erasing data)
e.g. Want to copy contents of file to USB device /dev/sdb
1. `dd if=/home/user/backup.tar.gz of=/dev/sdb bs=4M` --> 
	1. `if` (input file) is the source file
	2. `of` (output file) is the target location USB device
	3. `bs` (block size) of data transfer. #note check out what this means