# 在Mac、Linux上搭建开发环境

依照以下操作，你可在`Mac`，`Linux(Debia/Ubuntu)`上搭建`PPMessage`开发环境。

---

#### 下载PPMessage源代码
首先需要安装`git`，然后从`github`下载源代码，假设保存路径为`~/Documents/ppmessage`。

```
git clone git@github.com:PPMESSAGE/ppmessage.git
```

#### 下载geolite2
源代码下载完成后，进入`~/Documents/ppmessage`目录，执行

```
ppmessage/scripts/download_geolite2.sh
```

#### 安装依赖软件
进入`~/Documents/ppmessage/ppmessage/scripts`目录。

* 在`Mac`下, 执行

  ```
  bash set-up-ppmessage-on-mac.sh
  ```

* 在`Linux(Debian/Ubuntu)`下, 执行

  ```
  bash set-up-ppmessage-on-debian-or-ubuntu.sh
  ```

注意：当执行脚本安装依赖时，操作系统原有的软件可能会被更新、覆盖。你需要注意以下事项，并在必要的时候DIY脚本。

* `Mac`下，配置脚本会通过源码编译安装`mysql-connector-python-2.1.3`, 会覆盖你机器上已安装版本。

* `Linux`下，配置脚本会通过源码编译安装`nginx-1.8.0`，`ffmpeg-3.0.2`，`mysql-connector-python-2.1.3`, 会覆盖你机器上已安装版本。


#### 安装npm, bower包
进入`~/Documents/ppmessage`目录

```
./dist.sh bower
./dist.sh npm
```

如果执行`./dist.sh npm`出现资源被屏蔽、无法下载的错误，可以执行`./dist.sh cnpm`，这会从淘宝的`npm`镜像源下载`npm`包。

#### 配置PPMessage
参考[配置PPMessage](./config-ppmessage.md)，生成配置文件。


#### 启动PPMessage
首先，确保`mysql server`, `redis-server`, `nginx`已启动。

* 在`Mac`下，输入以下命令启动上述服务

  ```
  brew services start mysql
  brew services start redis
  nginx
  ```

* 在`Linux（Debian/Ubuntu）`下，输入以下命令启动上述服务
  
  ```
  sudo service mysql start
  sudo service redis-server start
  sudo nginx
  ```

然后，进入`~/Documents/ppmessage`目录，执行以下操作

1. 将`ppmessage`加入`Python PATH`

  ```
  sudo ./dist.sh dev
  ```
  
2. 初始化数据库，初始化缓存，更新`nginx`配置文件（`Linux`下需要`sudo`）

  ```
  ./dist.sh bootstrap
  ```
  
3. 重新加载`nginx`配置文件(`Linux`下需要`sudo`)

  ```
  nginx -s reload
  ```
4. 生成`PPKefu`, `PPConsole`, `PPCom`的`js`, `css`文件
  
  ```
  ./dist.sh gulp
  ```
  
5. 启动`PPMessage`(`Linux`下需要`sudo`)

  ```
  ./dist.sh start
  ```

#### 访问PPMessage
一旦`PPMessage`成功运行，我们就可以访问`PPMessage`各模块。

地址格式为：`http_protocol://server_ip:server_port/service_name`。

其中，`http_protocol`与配置文件里`nginx`的`ssl`设置有关，为`http`或者`https`, `server_ip`是配置文件里的服务器名字，`server_port`是配置文件里`nginx`监听端口。

例子：

    PPKefu: http://192.168.0.52:8080/ppkefu
    PPConsole: http://192.168.0.52:8080

可能出现的错误：

* 登录、注册时，出现ppauth 400 error
  
  解决办法：先更新PPMessage源码（`git pull`），然后执行`./dist.sh gulp`，最后清空浏览器缓存。

其他命令列举如下：

* 启动`PPMessage`（`Linux`下需要`sudo`）

  执行`./dist.sh bootstrap`会初始化数据库，平时启动`PPMessage`只需要执行

  ```
  ./dist.sh start
  ```

* 停止PPmessage（`Linux`下需要`sudo`）

  ```
  ./dist.sh stop
  ```
  
* 查看运行状态
    
  ```
  supervisorctrl
  ```
    
* 查看日志
  
  日志保存目录为 `/usr/local/var/log`

  ```
  ./dist.sh log                                  # 所有日志
  tail -f /usr/local/var/log/ppmessage-api.log   # 单独某模块的日志
  ```
