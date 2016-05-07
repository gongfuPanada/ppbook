# 使用 Docker 搭建开发环境

要想使用或者开发 PPMessage，首先必须搭建 PPMessage 开发环境。即使对于 PPMessage 团队的开发人员，从头开始搭建开发环境也是一件费时费力的事情。幸运的是，借助 Docker 的魔力，这些困难已经迎刃而解。

---

### 前言：Docker 的作用 ？
> Docker allows you to package an application with all of its dependencies into a standardized unit for software development. Docker containers wrap up a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries – anything you can install on a server. This guarantees that it will always run the same, regardless of the environment it is running in.

简而言之，Docker可以将程序运行时的所有依赖软件打包成为一个标准的 Docker 镜像。借助于此 Docker 镜像，该程序可以在任何支持 Docker 的机器上运行，并且效果完全一样。

#### 关于 Docker
首先仔细阅读 Docker 的官方引导文档 [docker getting started](https://docs.docker.com/mac/) ，了解 Docker 的基本概念和使用方法。

当你安装完 Docker 后，应该验证一下 Docker 命令是否可用。

**Mac 下**， 点击 **启动面板(LaunchPad)** 里的 Docker Quickstart Terminal 打开 Terminal。等待docker启动完毕，输入命令`docker info`。如果没有显示错误，说明 Docker 命令可用。（需要注意的是，在Mac下，必须通过Docker Quickstart Terminal 打开的 Terminal才可以使用Docker命令）

**Linux 下**，打开系统Terminal， 输入命令`docker info`。如果没有错误，则说明 Docker 命令可用。如果提示以下错误：

> Cannot connect to the Docker daemon. Is 'docker -d' running on this host?

则先尝试重启 Docker 服务

```bash
sudo service docker restart
```

如果之后执行`docker info`还是出错的话，则将当前用户加入到docker组中，执行

```bash
sudo usermod -aG docker $USER
```

然后重新登录当前用户，在打开系统Terminal，就应该可以使用 Docker 命令了。

#### 下载 PPMessage Docker镜像
安装好 Docker 之后，下一步是下载 PPMessage Docker 镜像。镜像托管在[Docker Hub](https://hub.docker.com/r/ppmessage/ppmessage/)上。要下载它，打开 Terminal，输入命令：

```bash
docker pull ppmessage/ppmessage
```

下载过程可能比较漫长，请继续看下面两个步骤：**下载 PPMessage 源码**， **配置PPmessage**

#### 下载 PPMessage 源码
启动 PPMessage 之前，首先需要获取PPMessage的源码。源码托管在 [github](https://github.com/PPMESSAGE/ppmessage) 上。要下载它，执行以下命令(下载到`~/Documents`目录下)：

```bash
cd ~/Documents
git clone git@github.com:PPMESSAGE/ppmessage.git
```

#### 下载geolite2

```bash
cd ~/Documents/ppmessage/api/geolite2
wget http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.mmdb.gz
gunzip GeoLite2-City.mmdb.gz
```

#### 安装Nodejs, Npm包
下载PPMessage源码之后，我们还需要从源码中生成PPCom, PPKefu, PPConsole运行时需要的js, css文件。

首先需要安装nodejs，在Mac上通过以下命令安装:

```bash
brew install nodejs
```

在Debian\Ubuntu上，通过以下命令安装nodejs 4.x

```bash
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```

安装完nodejs之后，下一步是安装cnpm, bower, gulp

```bash
sudo npm install -g bower
sudo npm install -g gulp
sudo npm install -g cnpm
```

最后，下载PPCom, PPKefu, PPConsole的bower 和 npm 依赖。

```bash
cd ~/Documents/ppmessage
./dist.sh bower
./dist.sh npm
```
在国内，从npm官方镜像源下载 npm 依赖速度比较慢，且会出现部分资源被墙的现象。此时可以用`./dist.sh cnpm`代替上面的`./dist.sh npm`, 这会从淘宝npm镜像源下载npm依赖。

因为生成PPConsole、PPKefu、PPConsole的js, css文件必须在PPMessage首次启动之后完成，我们将会在用Docker启动PPMessage后再执行这一操作。

#### 配置 PPMessage
PPMessage 源码下载完成后，在启动 PPMessage之前，你需要先生成 PPMessage 的配置文件。要生成配置文件，执行以下命令：

```bash
cd ~/Documents/ppmessage/bootstrap
cp config.template.py config.py
```

然后按照配置文件里的注释修改并保存 `~/Documents/ppmessage/bootstrap/config.py`：

```python
# -*- coding: utf-8 -*-
#
# Copyright (C) 2010-2016 PPMessage.
# Guijin Ding, dingguijin@gmail.com
# All rights reserved
#

"""
BOOSTRAP_CONFIG is the first place for developer edit before run PPMessage.

required:
    "team", to run PPMessage needing a team who is the first service team of the PPMessage
    "user", to run PPMessage needing a user who create the first service team and admin the whole PPMessage system
    "mysql", database config
    "nginx", nginx config
    "js",   client javascript minimization

optional:
    "apns", apple push service
    "gcm",  google clould message

"""

BOOTSTRAP_CONFIG = {
    # This team is the super admin's team
    "team": {
        "app_name": "your-team-name",            # your service team name
        "company_name": "your-company-name",     # your company name
    },

    # This user is the super user, who has two roles:
    # 1. the team admin of first service team
    # 2. the super admin of all service teams
    "user": {
        "user_language": "zh_cn", # zh_cn, en_us, zh_tw
        "user_firstname": "your-first-name",
        "user_lastname": "your-last-name",
        "user_fullname": "your-fullname",
        "user_email": "your-login-email",
        "user_password": "your-password",
    },

    "mysql": {
        "db_host": "127.0.0.1",
        "db_user": "root",
        "db_pass": "test",    # If you use docker to launch ppmessage, please set db_pass to 'test'
        "db_name": "ppmessage",
    },

    "server": {
        "name": "", # server's ip, like '192.168.0.110', PPKefu need this to know which server to connect
        "identicon_store": "/usr/local/opt/ppmessage/identicon",
        "generic_store": "/usr/local/opt/ppmessage/generic",
    },

    "js": {
        "min": "no", # `yes` or `no` for minimized the PPCOM/PPKEFU javascript file
    },

    # nginx conf
    # In Ubuntu/Debian/Docker, "nginx_conf_path" is "/usr/local/nginx/conf/nginx.conf"
    # In Mac, "nginx_conf_path" is "/usr/local/etc/nginx/nginx.conf"
    "nginx": {
        "nginx_conf_path": "/path-to-your-nginx.conf",
        "server_name": ["ppmessage.com", "www.ppmessage.com"],
        "listen": "8080", #80

        "upload_store": "/usr/local/opt/ppmessage/uploads 1",
        "upload_state_store": "/usr/local/opt/ppmessage/upload_state",

        # on for https, off for http
        "ssl": "off", # off/on
        "ssl_listen": "443",
        "ssl_certificate": "/path-to-your-ssl-cert",
        "ssl_certificate_key": "/path-to-your-ssl-server-key",
    },

    # optional, apns push certificate, dev for developer, pro for production
    "apns": {
        "name": "your-app's-bundle-id",
        "dev": "/path-to-your-apns-development.p12",
        "pro": "/path-to-your-apns-production.p12",
    },

    # optional, google cloud message
    "gcm": {
        "api_key": "your gcm apikey",
        "sender_id": "your gcm sender id",
    },
}
```

#### 启动 PPMessage
启动 PPMessage 之前，确认已经完成以下步骤：
* 下载PPMessage Docker 镜像
* 下载PPMessage源码
* 配置PPMessage

然后，输入以下命令启动PPMessage:

```bash
docker run -it -p 8080:8080 -v ~/Documents/ppmessage:/ppmessage ppmessage/ppmessage
```

`-p 8080:8080` 表示将本地的8080端口映射到 docker 容器的8080端口，如此就可以通过本地的8080端口访问在 docker 中运行的 PPMessage。

`-v ~/Documents/ppmessage:/ppmessage` 表示将本地的PPMessage 源码目录映射到 docker 容器的/ppmessage 目录，如此才可实现在本机开发源码，在docker里运行代码。

你也可以通过运行脚本 `~/Documents/ppmessage/ppmessage/docker/run-ppmessage.sh` 来启动 PPMessage。


#### 访问 PPMessage
在用docker启动PPMessage之后，我们需要生成PPCom, PPKefu, PPConsole运行时所需要的js，css文件。执行

```bash
cd ~/Documents/ppmessage
./dist.sh gulp
```
以后，当你更新PPMessage源码后，都要重复这一操作。

然后，你可以访问PPMessage的各项服务，例如api, ppkefu, pphome。

**在Linux 下**，Docker运行在本机上，你可以直接通过 `http://localhost:8080` 访问 PPMessage，例如：

```bash
http://localhost:8080/ppkefu
http://localhost:8080/pphome
```

**在 Mac 和 Windows下**，Docker运行在虚拟机中，你需要先获取 Docker 虚拟机的 IP。打开 Docker Terminal，输入命令：

```bash
docker-machine ip default
```

这会给出 docker 虚拟机的 IP 地址，假设IP是 `192.168.99.100`，则可通过 `http://192.168.99.100:8080`访问 PPMessage。


#### 关闭、重新启动 PPMessage
通过`docker run`启动 PPMessage 总是会新建一个 docker 容器，然后在新容器中初始化并运行 PPMessage。实际上我们总是希望可以重用第一次创建的 docker 容器，因为这样才可以保留 PPMessage 使用过程中产生的数据。要做到这点，我们需要获取到容器的ID，然后对容器进行启动，重启，关闭等操作。请参考以下命令。

* 查看所有容器 `docker ps -a`
  这会给出所有docker 容器的列表，你需要记住 PPMessage 容器的 id，以便对其进行关闭、启动、重启操作。

* 关闭容器`docker stop container_id`

* 启动容器`docker start container_id`

* 重启容器`docker restart container_id`

* 删除容器`docker rm contaniner_id`
