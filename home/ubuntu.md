1. 换源
  a. 备份源文件sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
  b. 编辑源文件 sudo vim /etc/apt/sources.list清空sources.list里内容，换上下面源地址，最后sudo apt update
  
```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
```

2. 源码安装软件（node实例）【也可以不建立软连接，添加环境变量也行】
  - 安装包下载 `curl -o node.tar.xz https://nodejs.org/dist/v18.13.0/node-v18.13.0-linux-x64.tar.xz `
  - 移动安装包到指定安装目录下 `mv node.tar.xz ./sdk/`【推荐放到/opt/ 目录下面】
  - 解压安装包 `tar -xf node.tar.xz`
  - 建立 node软连接  `sudo ln -s /home/qingshanshui/sdk/node-v18.13.0-linux-x64/bin/node /usr/bin/`
  - 建立 npm 软连接  `sudo ln -s /home/qingshanshui/sdk/node-v18.13.0-linux-x64/bin/npm /usr/bin/`
3. 环境变量
  - 全局永久环境变量，全局生效 `sudo vim /etc/profile`
  - 用户环境变量，当前账号生效 用户目录下 .bash_profile 
  - 当前shell设置的环境变量，shell生效 `export PATH=/usr/bin:/bin`
打开profile文件`sudo vim /etc/profile` 写入如下
```
# go 环境变量
export GOROOT=/home/qingshanshui/sdk/go1.20rc3 # GOROOT
export PATH=$PATH:$GOROOT/bin # GOROOT/bin
export PATH=$PATH:/home/qingshanshui/go/bin # GOPATH/bin
```
更新环境变量 `source /etc/profile`
4. 查看端口占用情况 `lsof -i:80`
5. :端口 终止程序 `kill -9 pid号码`