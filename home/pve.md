
### 1. PVE无法关闭虚拟机解决办法
#### 将101换成你自己虚拟机的ID
`ps -ef|grep "/usr/bin/kvm -id 101"|grep -v grep` 
#### 杀死进程
`kill 20582`
### 2. openwrt安装软件，出现错误：255
#### 原因：本地kernel版本是3.10.14，与安装包要求的3.10.49不同，因而安装时发出错误提示。如果确认所安装的软件没有依赖特定版本的内核功能，同样可以在其他版本的kernel使用，在opkg指令后加上--nodeps选项即可安装。
#### 解决：`opkg install luci-app-passwall2 --nodeps 后面加上 --nodeps`  

### 3. 安装docker
  #### a. ct模版里面下载，想要的系统，如：debian-12
  #### b. 创建ct，把无特权容器取消掉，ip4:192.168.0.106/24，其他正常配置/或者自己看着来
  #### c. 登录pve的shell容器，/etc/pve/nodes/pve/lxc 这目录下，对应【id】的conf文件，添加如下内容 
```
lxc.apparmor.profile: unconfined
lxc.cgroup.devices.allow: a
lxc.cap.drop: 
```
#### d. 启动容器：安装docker ，清华源安装docker   https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/
#### e. 切换docker源：vi /etc/docker/daemon.json
```
{
    "registry-mirrors": [ 
        "https://docker.mirrors.ustc.edu.cn" 
    ]
}
```
#### f. 配置docker开机自动启动：`systemctl enable docker.service`
#### g. 配置 docker容器内的 nginx 开机自动启动：
1. `docker update --restart=always 容器名称`
2. `docker run --name nginx -p 80:80  --restart=always nginx:latest重点是：--restart=always`

#### h. 安装：portainer
1. `docker volume create portainer_data`
2. `docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`
