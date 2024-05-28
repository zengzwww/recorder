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
