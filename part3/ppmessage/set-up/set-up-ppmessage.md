# 在Mac、Linux上搭建开发环境

依照以下操作，你可在`Mac`，`Linux(Debia/Ubuntu)`上搭建`PPMessage`开发环境。

---

#### 下载PPMessage源代码
首先需要安装`git`，然后从`github`下载源代码，假设保存路径为`~/Documents/ppmessage`。

```
git clone git@github.com:PPMESSAGE/ppmessage.git
```

#### 安装依赖软件
进入`~/Documents/ppmessage/ppmessage/scripts`目录。

* 在`Mac`下, 执行

  ```
  bash set-up-ppmessage-on-mac.sh
  ```

* 在`Linux(Debian/Ubuntu)`下, 执行

  ```
  bash set-up-ppmessage-on-linux.sh
  ```

注意：当执行脚本安装依赖时，操作系统原有的软件可能会被更新、覆盖。你需要注意以下事项，并在必要的时候DIY脚本。

* `Mac`下，配置脚本会通过源码编译安装`mysql-connector-python-2.1.3`, 会覆盖你机器上已安装版本。

#### 配置PPMessage
参考[配置PPMessage](./config-ppmessage.md)，生成配置文件。


#### 启动PPMessage
首先，确保`redis-server`已启动。

* 在`Mac`下，输入以下命令启动上述服务

  ```
  brew services start redis
  nginx
  ```

* 在`Linux（Debian/Ubuntu）`下，输入以下命令启动上述服务
  
  ```
  sudo service redis-server start
  ```

#### 访问PPMessage
一旦`PPMessage`完成配置成功运行，我们就可以访问`PPMessage`各模块。

地址格式为：`http_protocol://server_ip:server_port/service_name`。

其中，`http_protocol`可能是为`http`或者`https`, 默认是http, `server_ip`是配置文件里的服务器名字，默认是127.0.0.1，`server_port`默认是8945。

例子：

    PPKefu: http://127.0.0.0.1:8945/ppkefu
    PPConsole: http://127.0.0.1:8945/ppconsole



