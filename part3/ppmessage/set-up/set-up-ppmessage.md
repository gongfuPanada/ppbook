# 配置开发环境

### 下载PPMessage源代码
首先需要安装git, 然后

    cd ~/Documents
    git clone git@github.com:PPMESSAGE/ppmessage.git

添加geolite2

    cd ~/Documents/ppmessage/api/geolite2
    wget http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.mmdb.gz
    gunzip GeoLite2-City.mmdb.gz


### 搭建开发环境
搭建开发环境有两种方式，一种是通过配置脚本搭建，另一种是通过Docker搭建。
        
##### 通过配置脚本搭建开发环境

注意：当使用配置脚本时，我们默认认为你的机器上并没有安装配置脚本将要安装的软件。否则，你机器上原有的软件可能会被
更新、覆盖，从而造成不可预知的影响。要尽量避免这种影响，你需要注意以下事项，并在必要的时候DIY配置脚本。
    
    1. Mac & Linux
      配置脚本会通过源码编译安装 mysql-connector-python-2.1.3, 会覆盖你机器上已安装版本。
    
    2. Linux
      配置脚本会通过源码编译安装 nginx-1.8.0、ffmpeg-2.8.5, 会覆盖你机器上已安装版本。(之所以
      不用包管理器安装nginx,是因为包管理器安装nginx不包含nginx-upload-module)


执行配置脚本可以自动安装所有开发所需的依赖软件。进入配置脚本所在目录

    cd ~/Documents/ppmessage/ppmessage/deploy

在Mac下执行

    ./deploy-ppmessage-on-mac.sh

在Linux(Debian/Ubuntu)下执行

    ./deploy-ppmessage-on-linux.sh

检查依赖是否已经全部满足，如果提示没有安装某软件的话，可以手动安装。

    sudo python ~/Documents/ppmessage/ppmessage/scripts/require.py
    

##### 通过Docker搭建开发环境
有时，通过配置脚本安装的依赖软件可能会“污染”你机器上已安装的相同依赖软件。如果你想规避这个问题，可以使用Docker来搭建开发环境。

通过Docker搭建开发环境要求开发者对Docker的概念和应用有一定的理解。在这里我们对Docker的使用不做过多讲述。如果你不熟悉Docker的话，在搭建开发环境之前，请先参考[Docker官网](https://www.docker.com/)的使用文档。

1. 安装Docker

  首先需要安装Docker，Mac用户请参考[Mac安装Docker](https://docs.docker.com/mac/step_one/), Linux用户请参考[Linux安装Docker](https://docs.docker.com/engine/installation/)

2. 下载PPMessage Docker 镜像
   
  打开Docker terminal，输入命令

        docker pull ppmessage/ppmessage

  等待下载完成


### 下一步
开发环境搭建好后，下一步需要[配置PPMessage](./config-ppmessage.md)。
