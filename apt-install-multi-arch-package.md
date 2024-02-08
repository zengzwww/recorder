# 在虚拟机里安装其他架构的软件包([参考](https://askubuntu.com/questions/430705/how-to-use-apt-get-to-download-multi-arch-library))

* 创建其他架构软件包的source.list

```
sudo vi /etc/apt/sources.list.d/aarch64-cross-compile-sources.list
```
然后把清华源的ubuntu-ports里的东东稍作修改(在deb之后插入[arch=arm64])写入
```
deb [arch=arm64] https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal main restricted universe multiverse
deb [arch=arm64] https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-updates main restricted universe multiverse
deb [arch=arm64] https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-backports main restricted universe multiverse
deb [arch=arm64] https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-security main restricted universe multiverse
```

* 修改原来amd64的source.list

```
sudo vi /etc/apt/sources.list
```

在deb之后插入[arch=amd64]

* 更新源

```
sudo apt update
```

* 添加架构

```
sudo dpkg --add-architecture arm64
```

* 安装软件包

```
sudo apt install xxx:arm64
```
库被安装到/usr/lib/x86_64-linux-gnu目录下. 不加:arm64默认安装amd64架构版本的包
