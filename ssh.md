# ssh

## 如何在命令里面带密码

安装sshpass
```bash
sudo apt install sshpass
```

ssh登录
```bash
sshpass -p passward ssh [-p port] username@ip
```

scp传文件
```bash
sshpass -p passward scp [-P port] username@ip:/path/to/file
```
