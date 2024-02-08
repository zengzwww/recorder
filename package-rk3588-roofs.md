
查看插入的硬盘名
```
$ sudo fdisk -l
[sudo] password for blueberry:
Disk /dev/ram0: 4 MiB, 4194304 bytes, 8192 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/mmcblk0: 116.49 GiB, 125069950976 bytes, 244277248 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 8C130000-0000-4B36-8000-2E7900001DBB

Device            Start       End   Sectors   Size Type
/dev/mmcblk0p1    16384     24575      8192     4M unknown
/dev/mmcblk0p2    24576     32767      8192     4M unknown
/dev/mmcblk0p3    32768    163839    131072    64M unknown
/dev/mmcblk0p4   163840    425983    262144   128M unknown
/dev/mmcblk0p5   425984    491519     65536    32M unknown
/dev/mmcblk0p6   491520  29851647  29360128    14G unknown
/dev/mmcblk0p7 29851648  30113791    262144   128M unknown
/dev/mmcblk0p8 30113792 244277183 214163392 102.1G unknown


Disk /dev/sda: 1.84 TiB, 2000365289472 bytes, 3906963456 sectors
Disk model: Elements SE 2623
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: BC648F14-6020-48AB-9249-FB6CCDE9C519

Device     Start        End    Sectors  Size Type
/dev/sda1   2048 3906961407 3906959360  1.8T Microsoft basic data
```
[将硬盘挂载到/userdata节点](https://superuser.com/questions/134734/how-to-mount-a-drive-from-terminal-in-ubuntu)
```
$ sudo mount /dev/sda1 /userdata
```
用dd命令输出rootfs
```
$ sudo dd if=/dev/mmcblk0p6 of=/userdata/rootfs.img
29360128+0 records in
29360128+0 records out
15032385536 bytes (15 GB, 14 GiB) copied, 1522.87 s, 9.9 MB/s
```
修复rootfs错误
```
$ e2fsck -p -f /userdata/rootfs.img
/userdata/rootfs.img: recovering journal
/userdata/rootfs.img: 142320/915712 files (0.5% non-contiguous), 2178622/3670016 blocks
```
同步, 防止数据没有写入
```
$ sync
```
缩小rootfs的大小
```
$ cd /userdata
$ mkdir rootfs
$ sudo mount rootfs.img rootfs
$ cd rootfs
$ sudo rm -rf  ./var/lib/misc/firstrun
$ cd ..

$ e2fsck -p -f rootfs.img
rootfs.img: 142319/915712 files (0.5% non-contiguous), 2178622/3670016 blocks

$ resize2fs -M rootfs.img
resize2fs 1.45.5 (07-Jan-2020)
Resizing the filesystem on rootfs.img to 2613639 (4k) blocks.
The filesystem on rootfs.img is now 2613639 (4k) blocks long.
```
卸载rootfs.img
```
$ sudo umount -v rootfs.img
umount: /userdata/rootfs (/dev/loop0) unmounted
```
卸载硬盘
```
$ sudo umount -v /dev/sda1
umount: /userdata (/dev/sda1) unmounted
```
