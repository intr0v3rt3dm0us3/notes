\## ====================================================== \## Hetzner
Online GmbH - installimage - standard config \##
======================================================

\## ==================== \## HARD DISK DRIVE(S): \##
====================

\# Device Model: SAMSUNG MZVL2512HCJQ-00B00, Serial Number:
S675NX0T581146 DRIVE1 /dev/nvme0n1 \# Device Model: SAMSUNG
MZVL2512HCJQ-00B00, Serial Number: S675NX0T581344 DRIVE2 /dev/nvme1n1

\## =============== \## SOFTWARE RAID: \## ===============

\## activate software RAID? \< 0 \| 1 \>

SWRAID 1

\## Choose the level for the software RAID \< 0 \| 1 \| 10 \>

SWRAIDLEVEL 1

\## ========== \## HOSTNAME: \## ==========

\## which hostname should be set? \##

\## This must be a FQDN otherwise installation will fail \##

HOSTNAME Proxmox-VE.yourdomain.localdomain

\## ================ \## NETWORK CONFIG: \## ================

\# IPV4_ONLY no

\## ============= \## MISC CONFIG: \## =============

USE_KERNEL_MODE_SETTING yes

\## ========================== \## PARTITIONS / FILESYSTEMS: \##
==========================

\## define your partitions and filesystems like this: \## \## PART
\<mountpoint/lvm/btrfs.X\> \<filesystem/VG\> \<size in MB\> \## \## \*
\<mountpoint/lvm/btrfs.X\> \## mountpoint for this filesystem \*OR\* \##
keyword \'lvm\' to use this PART as volume group (VG) for LVM \*OR\* \##
identifier \'btrfs.X\' to use this PART as volume for \## btrfs
subvolumes. X can be replaced with a unique \## alphanumeric keyword \##
NOTE: no support btrfs multi-device volumes \## NOTE: reiserfs support
is deprecated and will be removed in a future version \## \*
\<filesystem/VG\> \## can be ext2, ext3, ext4, btrfs, reiserfs, xfs,
swap \*OR\* name \## of the LVM volume group (VG), if this PART is a VG.
\## \* \<size\> \## you can use the keyword \'all\' to assign all the
\## remaining space of the drive to the \*last\* partition. \## you can
use M/G/T for unit specification in MiB/GiB/TiB \## \## notes: \## -
extended partitions are created automatically \## - \'/boot\' cannot be
on a xfs filesystem \## - \'/boot\' cannot be on LVM! \## - when using
software RAID 0, you need a \'/boot\' partition \## \## example without
LVM (default): \## -\> 4GB swapspace \## -\> 1024MB /boot \## -\> 10GB /
\## -\> 5GB /tmp \## -\> all the rest to /home #PART swap swap 4G #PART
/boot ext2 1024M #PART / ext4 10G #PART /tmp xfs 5G #PART /home ext3 all
\# \## \## to activate LVM, you have to define volume groups and logical
volumes \## \## example with LVM: \# \## normal filesystems and volume
group definitions: \## -\> 1024MB boot (not on lvm) \## -\> all the rest
for LVM VG \'vg0\' #PART /boot ext3 1024M #PART lvm vg0 all \# \##
logical volume definitions: #LV \<VG\> \<name\> \<mount\> \<filesystem\>
\<size\> \# #LV vg0 root / ext4 10G #LV vg0 swap swap swap 4G #LV vg0
home /home xfs 20G \# \## \## to use btrfs subvolumes, define a volume
identifier on a partition \## \## example with btrfs subvolumes: \## \##
-\> all space on one partition with volume \'btrfs.1\' #PART btrfs.1
btrfs all \## \## btrfs subvolume definitions: #SUBVOL \<volume\>
\<subvolume\> \<mount\> \# #SUBVOL btrfs.1 @ / #SUBVOL btrfs.1 @/usr
/usr #SUBVOL btrfs.1 \@home /home \# \## your system has the following
devices: \# \# Disk /dev/nvme0n1: 512.12 GB (=\> 476.94 GiB) \# Disk
/dev/nvme1n1: 512.12 GB (=\> 476.94 GiB) \# \## Based on your disks and
which RAID level you will choose you have \## the following free space
to allocate (in GiB): \# RAID 0: \~952 \# RAID 1: \~476 \#

#######OEM

#######PART /boot ext3 1024M #######PART lvm vg0 all \####### #######LV
vg0 root / ext3 15G #######LV vg0 swap swap swap 6G

#######NEW

\#######

PART swap swap 32G PART /boot ext3 1024M PART / ext4 all

\#######

\## ======================== \## OPERATING SYSTEM IMAGE: \##
========================

\## full path to the operating system image \## supported image sources:
local dir, ftp, http, nfs \## supported image types: tar, tar.gz,
tar.bz, tar.bz2, tar.xz, tgz, tbz, txz \## examples: \# \# local:
/path/to/image/filename.tar.gz \# ftp:
ftp://\<user\>:\<password\>@hostname/path/to/image/filename.tar.bz2 \#
http: http://\<user\>:\<password\>@hostname/path/to/image/filename.tbz
\# https:
https://\<user\>:\<password\>@hostname/path/to/image/filename.tbz \#
nfs: hostname:/path/to/image/filename.tgz \# \# for validation of the
image, place the detached gpg-signature \# and your public key in the
same directory as your image file. \# naming examples: \# signature:
filename.tar.bz2.sig \# public key: public-key.asc

IMAGE
/root/.oldroot/nfs/install/../images/Debian-bookworm-latest-amd64-base.tar.gz
