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

## 四. Docker常用管理命令

1. 查看状态

   ```bash
   docker images ls
   docker container ls -a
   docker ps
   docker container stats [container name|id]
   ```

2. 控制台进入container

   ```bash
   docker exec -it <container name|id> /bin/bash
   ```

3. docker启动和映射

   前面的是物理机的端口，后面是docker 容器里面的端口，目录映射同理

   * 比如创建启动gitlab容器的命令如下

     ```bash
     docker run -d --net=gitlab_net -p 8443:443 -p 8880:80 -p 8022:22 --name gitlab -v /home/work/gitlab/config:/etc/gitlab -v /home/work/gitlab/logs:/var/log/gitlab -v /home/work/gitlab/data:/var/opt/gitlab -e 'GITLAB_SSH_PORT=8022' -e 'DB_HOST=127.0.0.1'  -e 'GITLAB_BACKUPS=weekly' -e 'GITLAB_HOST=111.231.228.178' -e 'GITLAB_SIGNUP=true' -e 'GITLAB_GRAVATAR_ENABLED=false' -e 'HOSTNAME=xxx' gitlab/gitlab-ce
     ```

   * 创建启动oracle11g的命令如下：

     ```bash
     docker run -d --name orcl -p 1521:1521 -e ORACLE_SID=orcl -e ORACLE_PWD=oracle -e ORACLE_CHARACTERSET=ZHS16GBK -e SGA_SIZE=4G -e PGA_SIZE=4G -e DB_ROLE=primary -e ENABLE_ARCH=true -v /home/db/oracle:/opt/oracle/oradata docker-oracle11g
     ```

   * 创建启动jupyter/datascience-notebook的命令:
   
   	```bash
   	docker run -d --name notebook -p 8888:8888 -v /home/DockerData/notebook:/home/jovyan jupyter/datascience-notebook
   	```
   	
   	执行以下命令查看日志：
   	
   	```bash
   	docker container logs notebook
   	```
   
   * 创建启动jupyter/all-spark-notebook全量容器的命令：
   
   ```bash
   docker run -d -v /home/DockerData/lab:/home/jovyan -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes --name mylab jupyter/all-spark-notebook
   ```

4. docker容器的用户不是管理员，如何以管理员登录？

   以jupyter lab为例，执行命令:

   ```bash
   docker exec -it -u 0 mylab /bin/bash
   ```

   以root（uid=0）用户登录管理container

   

