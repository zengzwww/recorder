# Linux

## 递归统计目录下的文件个数
```bash
find ./ -type f | wc -l
```

## 罗列非空的目录
```bash
find . -mindepth 1 -maxdepth 1 -not -empty -type d
```

## 初始化和更新[git子模块](https://www.cnblogs.com/jyroy/p/14367776.html)
```bash
git submodule update --init --recursive
```

## 建立桌面快捷方式

参考[它](https://linuxconfig.org/how-to-create-desktop-shortcut-launcher-on-ubuntu-20-04-focal-fossa-linux)

## 新建用户并将用户目录放置在非home目录下

```bash
sudo useradd -m -d <custom_home_dir_location> <username>
```
赋予新用户root权限   
先添加sudoers文件的写权限   
```bash
chmod u+w /etc/sudoers
vi /etc/sudoers
```
添加：xxx ALL=(ALL) ALL (这里的xxx是你的用户名)   
撤销sudoers文件写权限   
```bash
chmod u-w /etc/sudoers
```

## 同步本地文件到服务器

```bash
rsync -av -e 'ssh -p 2234' source/ user@remote_host:/destination
```
参考[rsync 用法教程](https://www.ruanyifeng.com/blog/2020/08/rsync.html)
[变慢的解决方法](https://virtuallyfun.com/2022/05/06/how-to-fix-rsync-slowing-down-over-time-solved/)

## linux系统下watch和其他命令的结合使用

### 1秒钟查看一次目录下文件的数量
```bash
watch -n 1 "find . -type f | wc -l"
```

## 让securecrt保持连接
参考[它](https://www.howtogeek.com/71/keep-securecrt-ssh-sessions-from-disconnecting/)

## 批量改后缀名

比如, 将png改为jpg
```bash
rename 's/\.png/.jpg/' *.png
```

## 进程暂停和继续

```
kill -STOP <PID>
kill -CONT <PID>
```

## 以关键字杀死进程/获取进程号

```bash
pgrep -f keyword
```

```bash
kill -9 `pgrep -f keyword`
```

参考[stackoverflow](https://stackoverflow.com/questions/8120304/getting-pids-from-ps-ef-grep-keyword)


## 搜索同一网段下的所有IP
```bash
sudo apt-get install arp-scan
sudo arp-scan -I wlo1 --localnet
```
将wlo1替换为用ifconfig查出来的网卡名

## 解码中文zip压缩包

```bash
unar xxx.zip
```


## 解决Ubuntu20.04进不了桌面的问题

添加如下两行

```text
blacklist nouveau
options nouveau modeset=0
```

禁用驱动nouveau

```bash
root@industai-Super-Server:~# cat /etc/modprobe.d/blacklist.conf 
# This file lists those modules which we don't want to be loaded by
# alias expansion, usually so some other driver will be loaded for the
# device instead.

# evbug is a debug tool that should be loaded explicitly
blacklist evbug

# these drivers are very simple, the HID drivers are usually preferred
blacklist usbmouse
blacklist usbkbd

# replaced by e100
blacklist eepro100

# replaced by tulip
blacklist de4x5

# causes no end of confusion by creating unexpected network interfaces
blacklist eth1394

# snd_intel8x0m can interfere with snd_intel8x0, doesn't seem to support much
# hardware on its own (Ubuntu bug #2011, #6810)
blacklist snd_intel8x0m

# Conflicts with dvb driver (which is better for handling this device)
blacklist snd_aw2

# replaced by p54pci
blacklist prism54

# replaced by b43 and ssb.
blacklist bcm43xx

# most apps now use garmin usb driver directly (Ubuntu: #114565)
blacklist garmin_gps

# replaced by asus-laptop (Ubuntu: #184721)
blacklist asus_acpi

# low-quality, just noise when being used for sound playback, causes
# hangs at desktop session start (Ubuntu: #246969)
blacklist snd_pcsp

# ugly and loud noise, getting on everyone's nerves; this should be done by a
# nice pulseaudio bing (Ubuntu: #77010)
blacklist pcspkr

# EDAC driver for amd76x clashes with the agp driver preventing the aperture
# from being initialised (Ubuntu: #297750). Blacklist so that the driver
# continues to build and is installable for the few cases where its
# really needed.
blacklist amd76x_edac
blacklist nouveau
options nouveau modeset=0
```

## 开机自动挂载硬盘

```text
UUID=a6879c64-e7fc-4319-9e80-5749c0b1b429 /mnt/data ext4 defaults 1 1
```

see (here)[https://blog.csdn.net/mochou111/article/details/81298613]
