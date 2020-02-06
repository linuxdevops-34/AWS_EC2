# AWS_EC2
EC2 Samples


# AWS_EC2
EC2 Samples

```
## Adding EBS Volume to EC2 Instance with filesystem creation
[ec2-user@ip-xxxx ~]$ sudo su
[root@ip-xxxx ec2-user]# clear
[root@ip-xxxx ec2-user]# lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0    8G  0 disk
└─xvda1 202:1    0    8G  0 part /
xvdf    202:80   0  100G  0 disk
[root@ip-xxxx ec2-user]# file -s /dev/xvdf
/dev/xvdf: data
[root@ip-xxxx ec2-user]# mkfs -t ext4 /dev/xvdf
mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
6553600 inodes, 26214400 blocks
1310720 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2174746624
800 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624, 11239424, 20480000, 23887872

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

[root@ip-xxxx ec2-user]# file -s /dev/xvdf
/dev/xvdf: Linux rev 1.0 ext4 filesystem data, UUID=40a93de4-8a44-40da-9741-366a6de4bdd2 (extents) (64bit) (large files) (huge files)
[root@ip-xxxx ec2-user]# cd /
[root@ip-xxxx /]# mkdir filesystem
[root@ip-xxxx /]# mount /dev/xvdf /filesystem
[root@ip-xxxx /]# lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0    8G  0 disk
└─xvda1 202:1    0    8G  0 part /
xvdf    202:80   0  100G  0 disk /filesystem
[root@ip-xxxx /]# cd filesystem/
[root@ip-xxxx filesystem]# echo "Shiny Volume!" > vol.txt
bash: !": event not found
[root@ip-xxxx filesystem]# echo "Shiny FileSystem" > vol.txt
[root@ip-xxxx filesystem]# ls
lost+found  vol.txt
[root@ip-xxxx filesystem]# cat vol.txt
Shiny FileSystem
[root@ip-xxxx filesystem]# cd /
[root@ip-xxxx /]# umount /dev/xvdf
[root@ip-xxxx /]# lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0    8G  0 disk
└─xvda1 202:1    0    8G  0 part /
xvdf    202:80   0  100G  0 disk
```
