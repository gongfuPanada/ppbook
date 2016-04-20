# 运行PPMessage

在完成PPMessage配置后，下一步是运行PPMessage

### 准备工作
运行PPMessage之前，确保mysql server, redis-server, nginx已在运行中。

在Linux下，输入以下命令启动上述服务

    sudo service mysql start
    sudo service redis-server start
    sudo nginx

在Mac下，输入以下命令启动上述服务
  
    brew services start mysql
    brew services start redis
    nginx
    
最后，进入PPMessage根目录

    cd ~/Documents/ppmessage
    
### 首次运行前
首次运行需要做一些额外工作。

1. 将ppmessage加入到Python Path

       sudo ./dist.sh dev

2. 初始化数据库、redis缓存，更新nginx.conf
    
       ./dist.sh bootstrap

3. 重新加载 nginx.conf

       # Linux 下需要 sudo
       nginx -s reload


### 运行PPMessage
* 在首次运行后，再次运行PPMessage

      ./dist.sh start
  一旦PPMessage成功运行，我们就可以访问PPMessage各个模块。格式为：http_protocol://server_ip:server_port/service_name，例如：
  
      http://localhost:8080/api
      http://localhost:8080/ppauth
      http://localhost:8080/ppkefu
      ...

* 停止运行

      ./dist stop
  
    
### 其他
* 为PPConsole、PPCom、PPKefu安装bower, npm依赖，执行gulp任务

      ./dist.sh bower
      ./dist.sh npm
      ./dist.sh gulp
  如果遇到electron无法下载的问题，请参考[set-up-PPKefu](./ppkefu/set-up-ppkefu.md)。

* 查看PPMessage运行状态
    
      supervisorctrl
  RUNING状态表示服务正常运行。

* 查看日志

      ./dist.sh log                                  # 所有日志
      tail -f /usr/local/var/log/ppmessage-api.log   # 单独某模块的日志
  日志目录为 /usr/local/var/log



