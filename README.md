# 《深度学习技术图像处理入门》容器环境

登陆服务器，开启 docker 以及 nvidia-docker服务，并开启镜像。

## 使用方法

GPU 服务器完成 nvidia-driver, docker 以及 nvidia-docker 的安装后，请在 Linux 终端输入如下内容，启动本镜像:

```shell
systemctl start docker
systemctl start nvidia-docker

git clone https://github.com/Jinglue/dl4img
nvidia-docker pull hubq/dl4img
nvidia-docker run -d -v ~/dl4img/notebook/:/srv -p 8888:8888 -p 6006:6006 hubq/dl4img
```

镜像打开后，读者可以在浏览器中输入：

```
http://[购买云服务器的IP地址]:8888
```

进而输入密码 `dl4img`， 即可登录云端界面。

![](./jupyter1.png)

## notebook 使用入门

这里以问答的形式，简单介绍如何使用 jupyter notebook

### Jupyter notebook 最突出的优点是什么

在浏览器端混合编码可执行代码(特别是 python 和 bash)、Markdown 格式的文本，以及必要的图表。

### Markdown 是什么格式

### 如何区分 markdown 文本以及程序代码

### 如何新建 notebook

### 如何新建 linux 终端

### 如何管理 notebook 以及 linux 终端

### 如何执行 notebook 中编写的 python 代码

### 如何执行 notebook 中混编的 linux shell 脚本

### 如何让 python 画图函数在 notebook 里直接输出结果

### 如何中断执行 notebook 中编写的代码

### 如何重启 notebook

### 如何将编写执行完成的 notebook 从云端保存本地


## 安装  `nvidia-driver`, `docker` 以及 `nvidia-docker`

这一部分内容写给想自己折腾的人，如果租服务器，可以直接用镜像忽略这里。具体请参考《深度学习技术图像处理入门》第0章内容。简单说：

### nvidia-driver

参考腾讯云 GPU 官方指导  [https://www.qcloud.com/document/product/560/8048](https://www.qcloud.com/document/product/560/8048)。注意本环境使用的是 384.66。

安装遇到问题时，请根据具体情况选择 yes no，有报错多上网搜索答案，并且尝试重启机器。

### 使用 Ubuntu16.04

```shell
# 安装 CUDA
wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda

# 安装 docker
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" >/etc/apt/sources.list.d/docker.list
sudo apt-get update
sudo apt-get install docker-engine

# 安装 nvidia-docker
wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb
sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb

# 启动 docker 服务
systemctl start docker
systemctl start nvidia-docker

# 下载并启动镜像
sudo nvidia-docker pull hubq/dl4img
```

### 使用 CentOS 7

```shell
# 安装 CUDA
wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-rhel7-8-0-local-ga2-8.0.61-1.x86_64-rpm
rpm -i cuda-repo-rhel7-8-0-local-ga2-8.0.61-1.x86_64-rpm
yum install cuda


# 安装 docker
yum install docker

# 安装 nvidia-docker
wget https://github.com/NVIDIA/nvidia/docker/releases/download/v1.0.1/nvidia-docker-1.0.1-1.x86_64.rpm

rpm -i nvidia-docker-1.0.1-1.x86_64.rpm

# 启动 docker 服务
systemctl start docker
systemctl start nvidia-docker

# 下载并启动镜像

##########################################################################
## 如果使用腾讯云Centos 7 GPU服务器，这里建议换docker源为腾讯云docker源。#
## 需要修改 Docker 配置文件/etc/sysconfig/docker，添加：                 #
## OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'         #
##########################################################################

sudo nvidia-docker pull hubq/dl4img
```
