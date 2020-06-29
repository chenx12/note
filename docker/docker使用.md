# Docker

## 一、安装

### 1 卸载旧版本

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### 2 安装Docker Engine-Community

#### (1) 设置仓库

```bash
### 安装所需的软件包
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

```bash
### 设置稳定的仓库
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

#### (2) 安装

1. 安装稳定版本

   ```bash
   sudo yum install docker-ce docker-ce-cli containerd.io
   ```

2. 安装指定版本

   1. 列出可用版本

      ```bash
      yum list docker-ce --showduplicates | sort -r
      ```

   2. 通过其完整的软件包名称安装特定版本，该软件包名称是软件包名称（docker-ce）加上版本字符串（第二列），从第一个冒号（:）一直到第一个连字符，并用连字符（-）分隔。例如：docker-ce-18.09.1。

      ```bash
      sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
      ```

## 二、使用

### 容器

#### 1 启动docker

```bash
systemctl start docker
```

#### 2 运行交互式容器

```bash
docker run -itd -p 443:443 -v /opt:/opt --name docker1 ubuntu:15.10 /bin/bash
```

参数解析：

- docker: Docker 的二进制执行文件。
- run: 与前面的 docker 组合来运行一个容器。
- `ubuntu:15.10` 指定要运行的镜像，Docker 首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 Docker Hub 下载公共镜像。
- `/bin/bash` 在启动的容器里执行的命令
- -t 在新容器内指定一个伪终端或终端。
- -i 交互式操作。
- -d 后台模式运行。
- -p 指定端口,格式：主机端口:容器端口。
- -v 挂载目录。
- --name 指定容器名称。

> 运行 exit 命令或者使用 CTRL+D 来退出容器。
>
> docker ps 查看运行的容器
>
> docker ps -a 查看所有容器
>
> 在容器内使用 docker logs 命令，查看容器内的标准输出

#### 3 停止容器

`docker stop 容器id/容器名称` 停止容器  
`docker start 容器id` 启动一个已经停止的容器  
`docker restart 容器id` 重启容器

#### 4 进入后台容器

`docker exec -it 容器id /bin/bash`

#### 5 导出/导入容器

`docker export 容器id > 导出文件名`  导出容器快照到本地文件 

`cat docker/ubuntu.tar | docker import - test/ubuntu:v1`  从容器快照文件中导入为镜像

#### 6 删除容器

`docker rm -f 容器ID/名称`

`docker container prune` 删除所有处于终止状态的容器

#### 7 运行web应用

`docker pull training/webapp`  载入镜像
`docker run -d -P training/webapp python app.py`

`docker run -d -p 127.0.0.1:5001:5000 training/webapp python app.py`

  - -d 后台运行
  - -P 容器内网络端口映射到主机上
  - -p 指定端口 也可以指定主机。 主机:主机端口:容器端口/协议端口(tcp/udp)
  - --name 命名容器

`docker logs -f` 容器ID/名称 查看容器内部标准输出

`docker top` 查看容器内部运行的进程

`docker inspect` 查看 Docker 的底层信息

`docker stop` 停止web应用容器

`docker start` 重启已经停止的web容器

`docker rm` 删除不需要的容器（容器必须是停止状态）

### 镜像

#### 1 查看本机镜像

`docker images`

#### 2 下载新镜像

`docker pull`

#### 3 查找镜像

`docker search`

#### 4 删除镜像

`docker rmi`

## 三、Dockerfile

### 常用指令

- FROM：定制的镜像都是基于 FROM 的镜像
- RUN：用于执行后面跟着的命令行命令。有shell格式和exec格式，用`&&`连接命令只会创建一层镜像
- COPY：复制指令，从上下文目录中复制文件或者目录到容器里指定路径。

```dockerfile
COPY [--chown=<user>:<group>] <源路径1>...  <目标路径>
COPY [--chown=<user>:<group>] ["<源路径1>",...  "<目标路径>"] #用户和用户组可选
```

### 构建镜像

`docker build -t 镜像名:标签 .` 

.代表本次执行的上下文路径。上下文路径，是指 docker 在构建镜像，有时候想要使用到本机的文件（比如复制），docker build 命令得知这个路径后，会将路径下的所有内容打包。 