# 运行PPMessage

在完成PPMessage配置后，下一步是运行PPMessage

### 准备工作
运行PPMessage之前，确保mysql server, redis-server, nginx已在运行中
进入PPMessage根目录

    cd ~/Documents/ppmessage
    
### 首次运行
首次运行需要做一些额外工作。

将ppmessage 加入到 Python Path

    ./dist.sh dev

初始化数据库，更新nginx.conf，启动PPMessage
    
    ./dist.sh bootstrap

加载新生成 nginx.conf

    nginx -s reload

### 运行、停止运行PPMessage
在首次运行后，再次运行PPMessage

    ./dist.sh start

停止运行

    ./dist stop
    
### 其他
查看PPMessage运行状态
    
    supervisorctrl

查看所有模块的日志

    ./dist.sh log

查看某一模块的日志

    api 日志:
    tail -f /usr/local/var/log/ppmessage-api.log
    
    dispatcher 日志:
    tail -f /usr/local/var/log/ppmessage-dispatcher.log
    
    ...
    

