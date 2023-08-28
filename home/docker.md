### linux下安装
1. 官方一键安装命令 `curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun`
2. 为了避免每次命令都输入sudo，可以设置用户权限(将当前用户添加到docker组里面)，注意执行后须注销重新登录 `sudo usermod -a -G docker $USER`
- 启动`dockersudo service docker start`
- 停止`dockersudo service docker stop`
- 重启`dockersudo service docker restart`
3. 换源
sudo vim /etc/docker/daemon.json 插入如下内容
```
{
  "registry-mirrors": ["https://epsax6ut.mirror.aliyuncs.com"]
}
```
在重启`dockersudo service docker restart`

### 容器
- docker ps 查看所有容器
- docker ps -a 查看已停止容器
- docker start <容器id>  启动已停止的容器
- docker stop <容器id>  停止容器
- docker restart <容器id>  重启容器
- docker rm -f <容器id> 删除容器

### 镜像
- docker images 列出本地的镜像
- docker pull nginx:latest 获取最新镜像
- docker pull nginx:5.7 获取指定版本镜像
- docker search nginx 查找镜像
- docker rmi nginx 删除镜像

### 安装mysql
1. 拉取最新mysql镜像: docker pull mysql:latest
2. 运行容器：docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
3. 进入容器：docker exec -it mysql-test /bin/bash  进入 mysql mysql -h localhost -u root -p 

### 安装redis
1. 拉取最新镜像：docker pull redis:latest
2. 运行容器：docker run -itd --name redis-test -p 6379:6379 redis
3. 进入容器：docker exec -it redis-test /bin/bash   进入redis redis-cli

### 开机自动启动
1. docker update --restart=always 容器名称
2. docker run --name nginx -p 80:80  --restart=always nginx:latest

### docker compose 安装
1. curl -SL https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose 
2. sudo chmod +x /usr/local/bin/docker-compose
3. docker-compose --version