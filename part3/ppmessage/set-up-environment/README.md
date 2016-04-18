# 配置PPMessage开发环境

### 获取PPMessage
首先需要安装git, 然后

    cd ~/Documents
    git clone git@github.com:PPMESSAGE/ppmessage.git

接下来，可以通过配置脚本或者Docker搭建开发环境。

### 通过配置脚本搭建开发环境
注意：当使用配置脚本时，我们默认认为你的机器上并没有安装配置脚本将要安装的软件。否则，某些软件可能会被
更新、覆盖，从而造成不可预知的影响。要尽量避免这种影响，你需要注意以下事项，并在必要的时候DIY配置
脚本。

    1. Mac & Linux
       配置脚本会通过源码编译安装 mysql-connector-python-2.1.3, 会覆盖你机器上已安装版本。

    2. Linux

       1. 配置脚本会通过源码编译安装 nginx-1.8.0, 会覆盖你机器上已安装版本。(之所以不用包管理器安装nginx,
       是因为包管理器安装nginx不包含nginx-upload-module)
       2. 配置脚本会通过源码编译安装 ffmpeg-2.8.5, 会覆盖你机器上已安装版本。


Mac和Linux(Debian/Ubuntu)都有对应的配置脚本，执行配置脚本可以自动安装所有开发所需的依赖软件。

    cd ~/Documents/ppmessage/ppmessage/deploy

在Mac下执行

    ./deploy-ppmessage-on-mac.sh

在Linux(Debian/Ubuntu)下执行

    ./deploy-ppmessage-on-linux.sh

### 通过Docker搭建开发环境
有时，通过配置脚本安装的依赖软件可能会“污染”你机器上已安装的相同依赖软件，使用Docker可以规避这个问题。
通过Docker搭建开发环境要求开发者对Docker的概念和应用有一定的理解，在这里我们对Docker不做过多讲述，有兴趣
的话可以浏览[Docker官网](https://www.docker.com/)。

#### 安装Docker

首先需要安装Docker，Mac用户请参考[Mac安装Docker](https://docs.docker.com/mac/step_one/), Linux
用户请参考[Linux安装Docker](https://docs.docker.com/engine/installation/)

#### 下载PPMessage Docker 镜像
打开Docker terminal，输入命令

    docker pull ppmessage/ppmessage

等待下载完成。

#### 启动Docker容器
在完成[PPMessage配置](./ppmessage-config.md)后, 运行Docker容器

    cd ~/Documents/ppmessage/ppmessage/deploy/docker
    ./run-ppmessage.sh

run-ppmessage.sh实际执行的是

    docker run -it -p 8080:8080 -v ~/Documents/ppmessage:/ppmessage ppmessage/ppmessage
                   ------------ ----------------------------------- -------------------
                      端口映射             目录映射                         Docker 镜像名

    -p 8080:8080 表示将本地的8080端口映射到 docker 容器的8080端口，如此就可以通过本地的8080端口访问在 docker 中运行的 PPMessage。

    -v ~/Documents/ppmessage:/ppmessage 表示将本地的PPMessage源码目录映射到 docker 容器的/ppmessage 目录，如此才可实现在本机开发源码，在docker里运行代码。
    
    最后的ppmessage/ppmessage 表示docker容器装载的是PPMessage的运行环境。

通俗地说，利用Docker容器允许PPMessage的原理是：PPMessage Docker镜像里安装了PPMessage所需的各种依赖软件，Docker容器装载PPMessage Docker镜像并运行这些依赖软件，构成PPMessage的运行环境。然后我们将宿主机的ppmessage源码拷贝到Docker容器里，让PPMessage在Docker里运行，最后通过端口映射，在宿主机监控Docker容器里PPMessage

#### 访问Docker中运行的PPMessage

在Linux 下，你可以直接通过 http://localhost:8080 访问 PPMessage，例如：

    http://localhost:8080/api
    http://localhost:8080/ppkefu
    http://localhost:8080/pphome
    ...

在 Mac 和 Windows下，需要先获取 docker 虚拟机 IP。打开 Docker Terminal，输入命令：

    docker-machine ip default
    
这会给出 docker 虚拟机的 IP 地址，例如 192.168.99.100。然后通过 http://192.168.99.100:8080访问 PPMessage
