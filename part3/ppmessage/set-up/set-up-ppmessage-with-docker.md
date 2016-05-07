# 使用 Docker 搭建开发环境

依照以下操作，你可使用`Docker`在`Mac`，`Linux`上搭建`PPMessage`开发环境。

---

### 前言：Docker 的作用 ？
> Docker allows you to package an application with all of its dependencies into a standardized unit for software development. Docker containers wrap up a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries – anything you can install on a server. This guarantees that it will always run the same, regardless of the environment it is running in.

简而言之，`Docker`可以将`PPMessage`运行时的所有依赖软件打包成为一个`Docker`镜像。借助于此镜像，`PPMessage`可以在任何支持`Docker`的机器上运行，并且效果完全一样。

#### 安装 Docker
首先仔细阅读`Docker`的官方引导文档 [docker getting started](https://docs.docker.com/mac/) ，了解`Docker`的基本概念和安装、使用方法。

当你安装完`Docker`后，应该首先验证一下`Docker`命令是否可用。

* `Mac`
 
  点击 **启动面板(LaunchPad)** 里的 `Docker Quickstart Terminal` 打开 `Terminal`。
  
  等待`Docker`启动完毕，输入命令`docker info`。如果没有显示错误，说明`Docker`命令可用。
  
  需要注意的是，在`Mac`下，必须通过`Docker Quickstart Terminal`打开的`Terminal`才可以使用`Docker`命令。

* `Linux`
  
  打开系统Terminal， 输入命令`docker info`。如果没有错误，则说明 Docker 命令可用。
  
  如果提示以下错误：

  > Cannot connect to the Docker daemon. Is 'docker -d' running on this host?

  则先尝试重启 Docker 服务

  ```
  sudo service docker restart
  ```
  
  如果之后执行`docker info`还是出错的话，则将当前用户加入到`docker group`中，执行

  ```bash
  sudo usermod -aG docker $USER
  ```

  然后重新以当前用户登录系统，再打开系统`Terminal`，就应该可以使用`Docker`命令了。

#### 下载 PPMessage镜像
安装好`Docker`之后，下一步是下载`PPMessage`镜像。镜像托管在[Docker Hub](https://hub.docker.com/r/ppmessage/ppmessage/)上，你可以搜索`ppmessage`找到它。要下载`PPMessage`镜像，打开`Terminal`，输入命令：

```
docker pull ppmessage/ppmessage
```

下载过程可能比较漫长，等待过程中你可继续执行下面的步骤。

#### 下载 PPMessage 源码
启动 PPMessage 之前，首先需要获取PPMessage的源码。源码托管在 [github](https://github.com/PPMESSAGE/ppmessage) 上。

假设你将PPMessage克隆到目录`~/Documents/ppmessage`。

```
git clone git@github.com:PPMESSAGE/ppmessage.git
```

#### 下载geolite2
进入`~/Documents/ppmessage/api/geolite2`目录，执行

```
wget http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.mmdb.gz
gunzip GeoLite2-City.mmdb.gz
```

#### 下载bower, npm依赖
首先需要安装`nodejs`，在`Mac`上通过以下命令安装

```
brew install nodejs
```

在`Debian\Ubuntu`上，通过以下命令安装`nodejs 4.x`

```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```

然后，用`npm`安装`cnpm, bower, gulp`

```
sudo npm install -g cnpm
sudo npm install -g bower
sudo npm install -g gulp
```

最后，下载`PPCom, PPKefu, PPConsole`的`bower，npm`依赖。进入`~/Documents/ppmessage`目录，执行

```
./dist.sh bower
./dist.sh npm
```
在国内，从`npm`官方镜像源下载`npm`包速度比较慢，且会出现资源被屏蔽的现象。此时可以用`./dist.sh cnpm`代替上面的`./dist.sh npm`, 这会从淘宝`npm`镜像源下载`npm`依赖。

#### 配置 PPMessage
参考[配置PPMessage](./config-ppmessage.md)，生成配置文件。

#### 启动 PPMessage
启动 PPMessage 之前，确认你已经完成以下步骤：
* 下载`PPMessage`镜像
* 下载`PPMessage`源码
* 配置`PPMessage`
* 下载`bower, npm`依赖

然后，输入以下命令启动`PPMessage`(根据实际情况，你可能需要改变某些参数)

```
docker run -it -p 8080:8080 -v ~/Documents/ppmessage:/ppmessage ppmessage/ppmessage
```

`-p 8080:8080` 表示将本地的`8080`端口映射到`Docker`容器的`8080`端口，如此就可以通过本地的`8080`端口访问在`Docker`容器中运行的`PPMessage`。

`-v ~/Documents/ppmessage:/ppmessage` 表示将本地的`PPMessage`源码目录映射到`Docker`容器`/ppmessage`目录，如此可实现在本机开发源码，在`Docker`容器里运行代码。

你也可以通过运行脚本 `~/Documents/ppmessage/ppmessage/docker/run-ppmessage.sh` 来启动 `PPMessage`。


#### 访问 PPMessage
在用`Docker`启动`PPMessage`之后，我们还需要生成`PPCom, PPKefu, PPConsole`运行时所需要的`js，css`文件，才能使用这三个模块。

进入`~/Documents/ppmessage`目录，执行

```
./dist.sh gulp
```
以后，当你更新`PPMessage`源码后，都要重复这一操作。

现在，你可以访问`PPMessage`的各模块，

访问地址格式为：`http_protocol://server_ip:server_port/xxxx`。例如`http://127.0.0.1:8080/ppkefu`, `http://192.168.99.100:8080/user`。

* `http_protocol`与配置文件里`nginx`的`ssl`设置有关，为`http`或者`https`；

* `server_port`是配置文件里`nginx`监听端口，为80或8080。

* `server_ip`是`Docker Machine`的`IP`，在`linux`和`Mac`下获取方式不同。

  * `Linux`
  
    `Docker`直接运行在操作系统上，`server_ip`就是'127.0.0.1'。

  * `Mac`

    `Docker`运行在虚拟机中，`server_ip`是虚拟机的`IP`。要获取这个`IP`，打开`Terminal`，执行

    ```
    docker-machine ip default
    ```

    这会给出`Docker`虚拟机的 IP 地址，例如IP是 `192.168.99.100`。


#### 关闭、重新启动 PPMessage
通过`docker run`启动`PPMessage`总是会新建一个`Docker`容器，然后在新容器中初始化并运行 `PPMessage`。

实际上我们总是希望可以重用第一次创建的容器，因为这样才可以保留使用过程中产生的数据。

要做到这点，我们需要获取到容器的`ID`，然后对容器进行启动，重启，关闭等操作。

请参考以下命令。

* 查看所有容器 
  
  ```
  docker ps -a
  ```
  这会给出所有`Docker`容器的列表，你需要记住`ppmessage/ppmessage` 对应的容器id，以便对其进行关闭、启动、重启操作。

* 关闭容器
  
  ```
  docker stop container_id
  ```

* 启动容器
  
  ```
  docker start container_id
  ```

* 重启容器
  
  ```
  docker restart container_id
  ```

* 删除容器
 
 ```
 docker rm contaniner_id
 ```
