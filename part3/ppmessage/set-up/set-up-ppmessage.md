# 在Mac、Linux上配置开发环境

依照以下操作，你可在Mac，Linux（Debian或Ubuntu）上搭建PPMessage开发环境。

---

### 下载PPMessage源代码
首先需要安装git，然后从github下载PPMessage源代码，假设保存路径为`~/Documents/ppmessage`。

```
git clone git@github.com:PPMESSAGE/ppmessage.git
```

### 下载geolite2
PPMessage源代码下载完成后，进入`~/Documents/ppmessage/api/geolite2`目录，执行

```
wget http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.mmdb.gz
gunzip GeoLite2-City.mmdb.gz
```

### 安装依赖
进入`~/Documents/ppmessage/ppmessage/scripts`目录。

* 在Mac下, 执行

  ```
  bash set-up-ppmessage-on-mac.sh
  ```

* 在Linux(Debian/Ubuntu)下, 执行

  ```
  bash set-up-ppmessage-on-linux.sh
  ```

注意：当执行脚本安装依赖时，操作系统原有的软件可能会被更新、覆盖。你需要注意以下事项，并在必要的时候DIY配置脚本。

* Mac下，配置脚本会通过源码编译安装 mysql-connector-python-2.1.3, 会覆盖你机器上已安装版本。

* Linux下，配置脚本会通过源码编译安装 nginx-1.8.0、ffmpeg-2.8.5、mysql-connector-python-2.1.3, 会覆盖你机器上已安装版本。(之所以不用包管理器安装nginx,是因为包管理器安装nginx不包含nginx-upload-module)


### 安装npm, bower包
执行：

```
cd ~/Documents/ppmessage
./dist.sh bower
./dist.sh npm
```

如果执行`./dist.sh npm`出现资源被墙无法下载的错误，可以执行`./dist.sh cnpm`，这会从淘宝的npm镜像源下载npm包。

### 配置PPMessage
参考[配置PPMessage](./config-ppmessage.md)，生成PPMessage配置文件。


### 启动PPMessage
首先，启动PPMessage之前，确保mysql server, redis-server, nginx已启动。

* 在Mac下，输入以下命令启动上述服务

  ```
  brew services start mysql
  brew services start redis
  nginx
  ```

* 在Linux（Debian/Ubuntu）下，输入以下命令启动上述服务
  
  ```
  sudo service mysql start
  sudo service redis-server start
  sudo nginx
  ```

然后，进入`~/Documents/ppmessage`目录，执行以下操作：

1. 将ppmessage加入Python PATH

  ```
  sudo ./dist.sh dev
  ```
  
2. 初始化数据库、redis缓存，更新nginx配置文件（Linux下需要`sudo`）

  ```
  ./dist.sh bootstrap
  ```
  
3. 重新加载nginx配置文件(linux下需要`sudo`)

  ```
  nginx -s reload
  ```
4. 生成PPKefu, PPConsole, PPCom的js, css文件
  
  ```
  ./dist.sh gulp
  ```
  
5. 启动PPMessage(Linux下需要`sudo`)

  ```bash
  # for Mac
  ./dist.sh start

  # for Debian/Ubuntu
  sudo ./dist.sh start
  ```

### 访问PPMessage
一旦PPMessage成功运行，我们就可以访问PPMessage各个模块。

地址格式为：`http_protocol://server_ip:server_port/service_name`。

其中，`http_protocol`与配置文件里nginx的ssl设置有关，为http或者https, `server_ip`是配置文件里的服务器名字，`server_port`是配置文件里nginx监听的端口。

例子：

    访问PPKefu: http://192.168.0.52:8080/ppkfu
    访问PPConsole: http://192.168.0.52:8080


### 其他

* 启动PPMessage

`./dist.sh bootstrap`会初始化数据库，平时启动PPMessage只需要执行以下命令即可

```bash
# Mac
./dist.sh start

# Linux
sudo ./dist.sh start
```

* 停止PPmessage

```bash
# Mac
./dist.sh stop

# Linux
sudo ./dist.sh stop
```
  
* 查看PPMessage运行状态
    
```supervisorctrl```
    
* 查看日志
日志目录为 /usr/local/var/log

```
./dist.sh log                                  # 所有日志
tail -f /usr/local/var/log/ppmessage-api.log   # 单独某模块的日志
```
