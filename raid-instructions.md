Create a RAID 1 Array:
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/disk1 /dev/disk2
Check with cat /proc/mdstat

Partition raid array:
sudo fdisk /dev/md0
Create MBR table/DOS table
Add 1GB primary partition
Add extended partition
Add logical partition
Write and exit
Check with ls /dev | grep md0
Format the primary (p1) and logical (p5) partitions with mkfs.ext4
Create directories to mount the partitions in

Create a RAID 5 Array:
sudo mdadm --create /dev/md1 --level=5 --raid-devices=3 /dev/disk3 /dev/disk4 /dev/disk5

Partition raid array:
sudo gdisk /dev/md1
Create GPT table
Add 3 partitions (2GB), hex code: 8300
Write and exit

/etc/fstab config:
Basic format:
UUID=<UUID>  <mount-point>  <file-system>  defaults  0 0

UUID can be found with sudo blkid /dev/<disk> for standard disks
UUID for raids: sudo mdadm --detail /dev/md0
