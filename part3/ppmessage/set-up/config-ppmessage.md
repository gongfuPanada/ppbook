# 配置PPMessage

在搭建好PPMessage开发环境后，运行PPMessage之前，需要对PPMessage做一些全局设置。

### 配置config.py
配置文件目录 ~/Documents/ppmessage/ppmessage/bootstrap，找到config.localhost.py，然后

    cp config.localhost.py config.py

请参照config.py里的注释填写配置信息

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
        "team": {
            "app_name": "ppmessage",
            "company_name": "YOURUI",
        },

        "user": {
            "user_language": "zh_cn", # zh_cn, en_us, zh_tw
            "user_firstname": "Guijin",
            "user_lastname": "Ding",
            "user_fullname": "Guijin Ding",
            # email is user account
            "user_email": "dingguijin@gmail.com",
            "user_password": "123",
        },

        "mysql": {
            "db_host": "127.0.0.1",
            "db_user": "root",
            "db_pass": "test",
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
        "nginx": {
            # In Ubuntu/Debian, "nginx_conf_path" is "/usr/local/nginx/conf/nginx.conf"
            # In Mac, "nginx_conf_path" is "/usr/local/etc/nginx/nginx.conf"
            "nginx_conf_path": "/usr/local/etc/nginx/nginx.conf",
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
            "api_key": "your gcm api key",
            "sender_id": "your gcm sender id",
        },
    }

其中必填的是

    BOOTSTRAP_DATA.team
    BOOTSTRAP_DATA.user
    BOOTSTRAP_DATA.mysql
    BOOTSTRAP_DATA.nginx
    BOOTSTRAP_DATA.js
    
选填的有

    BOOTSTRAP_DATA.apns
    BOOTSTRAP_DATA.gcm

###下一步
完成配置后，下一步是运行PPMessage
    
    1. 用配置脚本搭建开发环境，下一步是[运行PPMessage](./run-ppmessage.md)
    2. 用Docker搭建开发环境，下一步是[用docker运行PPMessage](./run-ppmessage-with-docker.md)
