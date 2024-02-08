# tensorboard

## 访问服务器上运行的tensorboard

1. 连接ssh时，将服务器的6006端口重定向到自己机器上来
```bash
ssh -L 16006:127.0.0.1:6006 username@remote_server_ip
```
16006:127.0.0.1代表自己机器上的16006号端口，6006是服务器上tensorboard使用的端口. 端口号可换.

2. 在服务器上使用6006端口正常启动tensorboard

```bash
tensorboard --logdir=xxx --port=6006
```

3. 在本地浏览器中输入地址

```text
127.0.0.1:16006
```
要是端口被占了, 通过如下命令查询对应的进程ID
```bash
lsof -i:6006
```
然后把这个进程杀死
```bash
kill -9 xxx
```
