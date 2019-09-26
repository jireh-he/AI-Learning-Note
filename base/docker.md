# Docker学习

[返回-首页](../README.md)

## 一. Docker架构

![Docker架构图](images/docker1.png)

Docker可已通过远程API管理和创建本地和远程的容器。

## 二. Docker安装

1. 添加软件源

```bash
echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
```
2. 更新缓存
```bash
sudo apt-get update
```

3. 安装docker
```bash
sudo apt-get install docker-engin
```


4. 启动docker

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

