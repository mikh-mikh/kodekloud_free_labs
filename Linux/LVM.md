# LVM Configuration Lab

This lab demonstrates the configuration and management of Logical Volume Manager (LVM) on a Linux system. 
Below, I’ve documented the steps, commands, and thought processes used to complete the tasks.

---

## Prerequisites
- Commands requiring root access are executed using `sudo`.
- Bob's default password: `caleston123`.

---

## Task 1: Verify LVM Installation

### Question
Is LVM installed on this machine?

### Solution
To verify LVM installation, I used the `lvdisplay` command:

```bash
sudo su -
lvdisplay

--- Logical volume ---
LV Path                /dev/vagrant-vg/root
LV Name                root
VG Name                vagrant-vg
LV UUID                aXeCm7-yCOC-srdD-T55P-wpHZ-c46Q-XJcX1t
LV Write Access        read/write
LV Creation host, time vagrant, 2021-11-21 18:46:22 +0000
LV Status              available
# open                 1
LV Size                <9.04 GiB
Current LE             2314
Segments               1
Allocation             inherit
Read ahead sectors     auto
- currently set to     256
Block device           253:0

--- Logical volume ---
LV Path                /dev/vagrant-vg/swap_1
LV Name                swap_1
VG Name                vagrant-vg
LV UUID                K00a0k-hD5J-CJZj-a3zj-CaDv-F82n-Q6ZDl0
LV Write Access        read/write
LV Creation host, time vagrant, 2021-11-21 18:46:22 +0000
LV Status              available
# open                 2
LV Size                980.00 MiB
Current LE             245
Segments               1
Allocation             inherit
Read ahead sectors     auto
- currently set to     256
Block device           253:1
```

Conclusion
Yes, LVM is installed and in use.

## Task 2: Identify Physical Volume (PV)
### Question
What is the name of the physical volume already created?

### Solution
I used the pvdisplay command to identify the physical volume:

```
pvdisplay

--- Physical volume ---
PV Name               /dev/vda1
```
### Conclusion
The physical volume is named vda1.

### Question
What is the size of this physical volume?

### Solution
The size is displayed in the pvdisplay output:

```
PV Size               <10.00 GiB / not usable 2.00 MiB
```
### Conclusion
The size of the physical volume is 10 GB.

Task 3: Identify Volume Group (VG)
### Question
What is the name of the volume group created using this PV?

### Solution
From the lvdisplay output earlier, the volume group name is:

```
VG Name               vagrant-vg
```
### Conclusion
The volume group is named vagrant-vg.

## Task 3: Create a New Volume Group

### Question
What are the sizes of the disks /dev/vdb and /dev/vdc?

### Solution
I used the lsblk command to check the disk sizes:

```
lsblk

NAME                   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
vda                    252:0    0   10G  0 disk 
└─vda1                 252:1    0   10G  0 part 
  ├─vagrant--vg-root   253:0    0    9G  0 lvm  /
  └─vagrant--vg-swap_1 253:1    0  980M  0 lvm  [SWAP]
vdb                    252:16   0    1G  0 disk 
vdc                    252:32   0    1G  0 disk
```

### Conclusion
Both /dev/vdb and /dev/vdc are 1 GB in size.

## Task 4: Create Physical Volumes (PVs)

I created PVs using /dev/vdb and /dev/vdc:

```
pvcreate /dev/vdb
Physical volume "/dev/vdb" successfully created.
pvcreate /dev/vdc
Physical volume "/dev/vdc" successfully created.
```

## Task 5: Create a New Volume Group

### Solution
I created a new volume group named caleston_vg using the newly created PVs:

```
vgcreate caleston_vg /dev/vdb /dev/vdc
Volume group "caleston_vg" successfully created.
```

## Task 6: Create a Logical Volume (LV)
Create a Logical Volume named "data"

### Solution
I created a logical volume named data with a size of 1 GB:

```
lvcreate -L 1G -n data caleston_vg
Logical volume "data" created.
```

## Task 7: Create and Mount a Filesystem
Create an ext4 filesystem on this logical volume and mount it at /mnt/medi

### Solution
I created an ext4 filesystem on the logical volume:

```
mkfs.ext4 /dev/mapper/caleston_vg-data
```

I mounted the filesystem at /mnt/media and updated /etc/fstab for persistence:

```
echo "/dev/mapper/caleston_vg-data /mnt/media ext4 defaults 0 0" >> /etc/fstab
mkdir /mnt/media
mount -v /mnt/media
/dev/mapper/caleston_vg-data mounted on /mnt/media.
```

## Task 8: Extend the Logical Volume
Add 500M to the logical volume called data.
Do not unmount the filesystem.
### Solution
I extended the logical volume data by 500 MB without unmounting the filesystem:

```
lvextend /dev/mapper/caleston_vg-data -L +500M
resize2fs /dev/mapper/caleston_vg-data
Size of logical volume caleston_vg/data changed from 1.00 GiB (256 extents) to <1.49 GiB (381 extents).
Logical volume caleston_vg/data successfully resized.
Filesystem on /dev/mapper/caleston_vg-data is now 390144 (4k) blocks long.
```

## Conclusion
Through this lab, I successfully:

- Verified LVM installation.
- Identified and created physical volumes, volume groups, and logical volumes.
- Created and mounted a filesystem.
- Extended a logical volume without unmounting the filesystem.

This exercise proved my understanding of LVM and its practical applications in managing disk storage on Linux systems.