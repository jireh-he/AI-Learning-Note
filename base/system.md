#TensorFlow Docker基础环境安装
##基础环境规划
操作系统：Centos 7 最小安装
主机名hostname:docker.lc
基本操作系统文件空间:/ 50g		/dev/centos_docker/root
/boot 500m  /dev/sda1
Swap 1g     /dev/centos_docker/swap
docker空间: /var/lib/docker	 50g		/dev/dockervg/lvdocker
关闭selinux
vi /etc/selinux/config 
SELINUX=disabled
:wq
Setenforce 0
配置本地yum源
Mkdir -p /media/dvd
Mount /dev/sr0 /media/dvd
[root@docker yum.repos.d]# vi  local.repo 
[dvd]
name=dvd
baseurl=file:///media/dvd
enabled=1
gpgcheck=0



##安装docker
1、安装必要系统工具
yum install -y yum-utils device-mapper-persistent-data lvm2

添加阿里yum源:
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
更新 yum 缓存：

yum makecache fast

3、安装 Docker-ce：

yum -y install docker-ce

4、docker加速
[root@docker yum.repos.d]# vi /etc/docker/daemon.json 
{
  "registry-mirrors": ["http://hub-mirror.c.163.com"]
}

5、启动 Docker 后台服务

sudo systemctl start docker

6、测试docker可用
docker run hello-world

7、启用GPU支持
安装nvidia-docker
https://github.com/NVIDIA/nvidia-docker
CentOS 7 (docker-ce), RHEL 7.4/7.5 (docker-ce), Amazon Linux 1/2

$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.repo | sudo tee /etc/yum.repos.d/nvidia-docker.repo

$ sudo yum install -y nvidia-container-toolkit
$ sudo systemctl restart docker


##安装portainer可视化管理面板

添加数据卷
docker volume create portainer_data

下载并启动portainer
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

通过网页连接:
http://192.168.**.**:9000/

创建用户后连接


##安装TensorFlow Docker
下载镜像
    docker pull tensorflow/tensorflow                     # latest stable release
    docker pull tensorflow/tensorflow:devel-gpu           # nightly dev release w/ GPU support
    docker pull tensorflow/tensorflow:latest-gpu-jupyter  # latest release w/ GPU support and Jupyter
    
测试TensorFlow安装成功
docker run -it --rm tensorflow/tensorflow \       python -c "import tensorflow as tf; tf.enable_eager_execution(); print(tf.reduce_sum(tf.random_normal([1000, 1000])))"    
其他详见：https://tensorflow.google.cn/install/docker

