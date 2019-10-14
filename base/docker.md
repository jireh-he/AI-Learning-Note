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

## 三. Docker安装mariadb

1. 获取mariadb镜像

   ```bash
   sudo docker pull mariadb
   ```

   下载完成后可以查看

   ```bash
   sudo docker image ls
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   centos              latest              0f3e07c0138f        2 days ago          220MB
   mariadb             latest              92495405fc36        2 weeks ago         356MB
   ```

2. 启动mysql，将数据与本机映射

   ```bash
   docker run -p 12306:3306 --name mymysql -v /home/DockerData/mysql/:/etc/mysql/ -v /home/DockerData/mysql/logs:/logs -v /home/DockerData/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mariadb
   ```

   