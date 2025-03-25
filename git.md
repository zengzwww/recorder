## 给远程仓库设置Personal access tokens，方便push
```
git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git
```

比如对于token`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`
```
git remote set-url origin  https://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@github.com/ts-eng/sysmonitor.git
```

## [关联多个远程仓库](https://zhuanlan.zhihu.com/p/82388563)

```bash
git remote set-url --add origin git@gitee.com:ji-dao/nncore.git
```

去除关联

```bash
git remote set-url --delete origin git@gitee.com:ji-dao/nncore.git
```

## 添加submodule
```
git submodule add xxx.git
```

## 拉取含submodule的完整仓库
```
git clone xxx.git --recurse-submodules
```

## [拉取submodule的代码](https://stackoverflow.com/questions/1030169/pull-latest-changes-for-all-git-submodules)

第一次
```bash
git submodule update --init --recursive
```

后面
```bash
git pull --recurse-submodules
```

## 轻量级版本管理工具Gogs
启动Gogs服务器
```
cd /path/to/gogs
gogs web
```
将本地项目初始化为一个本地仓库
```
cd xxx
git init
git add .
git commit -m "first commit"
```
在[Gogs页面](http://localhost:3000/install)新建一个仓库，把仓库地址(xxx.git)复制下来，然后关联本地仓库到git仓库
```
git remote add origin xxx.git
```
把本地文件推送到远程仓库里  
```
git push -u origin master
```

## git克隆报错(Permission denied (publickey))

将自己的电脑的SSH key添加到对应的git服务器上, 先生成key
```bash
ssh-keygen -t rsa -C “xxxxx@xxxxx.com” 
```

xxxxx@xxxxx.com是自己的邮箱, 查看key值
```bash
cat ~/.ssh/id_rsa.pub 
```

登录git, 将key添加上去

参考[Git报错：Permission denied (publickey) 解决办法](https://blog.csdn.net/libeiqi1201/article/details/117107099)

## git克隆报: Are you sure you want to continue connecting (yes/no)

```bash
vim /etc/ssh/ssh_config
```
将`# StrictHostKeyChecking ask`改成`StrictHostKeyChecking no`

## git报错: Failed to connect to 127.0.0.1 port 8001: 拒绝连接

[取消代理](https://blog.csdn.net/qq_37500838/article/details/118018524)
```bash
git config --global --replace-all remote.origin.proxy ''
```

## Add correct host key in /root/.ssh/known_hosts to get rid of this message.

[在连接的目标主机上的~/.ssh/known_hosts文件，去除过时的认证。](https://blog.csdn.net/yjk13703623757/article/details/81290185)

## 设置代理

参考[这里](https://gist.github.com/laispace/666dd7b27e9116faece6), 克隆的时候添加代理:
```bash
git clone -c https.proxy="127.0.0.1:7890" https://github.com/0x90d/videoduplicatefinder.git
```

## 重命名本地和远程分支

参考[这里](https://stackoverflow.com/questions/30590083/how-do-i-rename-both-a-git-local-and-remote-branch-name)

## 切换子模块的分支

参考[这里](https://stackoverflow.com/questions/1777854/how-can-i-specify-a-branch-tag-when-adding-a-git-submodule)

## 修改历史commit的作者信息

参考[这里](https://stackoverflow.com/questions/3042437/how-can-i-change-the-commit-author-for-a-single-commit)

## 从指定的commit创建tag

参考[这里](https://stackoverflow.com/questions/4404172/how-to-tag-an-older-commit-in-git)和[这里](https://stackoverflow.com/questions/4404172/how-to-tag-an-older-commit-in-git/21759466#21759466)
