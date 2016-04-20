# 用Docker运行PPMessage

#### 启动Docker容器
在完成[PPMessage配置](./config-ppmessage.md)后, 运行Docker容器

    cd ~/Documents/ppmessage/ppmessage/deploy/docker
    ./run-ppmessage.sh

run-ppmessage.sh 实际执行的是

    docker run -it -p 8080:8080 -v ~/Documents/ppmessage:/ppmessage ppmessage/ppmessage
                   ------------ ----------------------------------- -------------------
                      端口映射             目录映射                         Docker 镜像名

    -p 8080:8080 表示将本地的8080端口映射到 docker 容器的8080端口，如此就可以通过本地的8080
    端口访问在 Docker 中运行的 PPMessage。

    -v ~/Documents/ppmessage:/ppmessage 表示将本地的PPMessage源码目录映射到Docker容器
    的/ppmessage 目录，如此才可实现在本机开发源码，在Docker容器里运行代码。
    
    ppmessage/ppmessage 表示Docker容器装载的是PPMessage镜像

通俗地说，利用Docker容器允许PPMessage的原理是：PPMessage Docker镜像里安装了PPMessage所需的各种依赖软件。Docker容器装载PPMessage Docker镜像并运行这些依赖软件，构成PPMessage的运行环境。然后我们将宿主机的ppmessage源码拷贝到Docker容器里，让PPMessage在Docker里运行，最后通过端口映射，在宿主机访问Docker容器里运行的PPMessage。

#### 访问Docker中运行的PPMessage

在Linux下，你可以直接通过 http://localhost:8080 访问PPMessage，例如：

    http://localhost:8080/api
    http://localhost:8080/ppkefu
    ...

在Mac下，需要先获取Docker虚拟机IP。打开 Docker Terminal，输入命令：

    docker-machine ip default
    
这会给出Docker虚拟机的IP地址，例如 192.168.99.100。然后通过 http://192.168.99.100:8080 访问PPMessage。


#### 关闭、重启Docker容器
通过 docker run 启动 PPMessage 总是会新建一个 docker 容器，然后在新容器中初始化并运行 PPMessage。
实际上我们总是希望可以重用第一次创建的 docker 容器，因为这样才可以保留 PPMessage 使用过程中产生的数据。

    查看所有容器
    docker ps -a
    这会给出所有docker 容器的列表，你需要记住 PPMessage 容器的 id，以便对其进行关闭、启动、重启操作

    启动容器
    docker start container_id

    重启容器
    docker restart container_id
    
    关闭容器
    docker stop container_id
    
    删除容器
    docker rm contaniner_id
