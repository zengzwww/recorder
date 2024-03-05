# apt

### 执行apt update时报错: 404  Not Found [IP: 91.189.91.81 80]

打开sources.list

```bash
sudo gedit /etc/apt/sources.list
```

定位到下面一行(例如)

```text
deb http://security.ubuntu.com/ubuntu jammy-security main
```

添加架构信息

```text
deb [arch=amd64] http://security.ubuntu.com/ubuntu jammy-security main
```
