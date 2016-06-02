# 配置PPMessage

运行PPMessage前，需要对PPMessage做一些全局设置。

#### 生成配置文件
进入配置文件目录，生成config.py

```bash
cd ~/Documents/ppmessage/ppmessage/bootstrap
cp config.template.py config.py
```

#### 配置文件说明

配置文件里有如下设置项目：

#### 超级管理员

```python
"user": {
    "user_language": "",
    "user_firstname": "",
    "user_lastname": "",
    "user_fullname": "",
    "user_email": "",
    "user_password": "",
},
```

此用户是超级管理员，可以管理PPMessage下的所有用户和客服团队。各项设置介绍如下：

选项              | 说明          
-----------------|-------------
user_language    |  管理员的语言设置，决定系统创建PPCom匿名用户时，用何种语言生成用户名，以及PPCom的默认欢迎信息语言。可选zh_cn(简体中文), zh_tw(繁体中文), en_us(英文)
user_firstname   | 管理员的名
user_lastname    |  管理员的姓
user_fullname    |  管理员的全名
user_email       |     管理员的登录邮箱
user_password    |  管理员的登录密码


#### 超级管理员客服团队

```python
"team": {
    "app_name": "",
    "company_name": "",
}
```

此团队是超级管理员的客服团队，各项设置解释如下：

选项              | 说明          
-----------------|-------------
app_name         | 客服团队的名称
company_name     | 公司或组织名称


#### mysql 设置

```python
"mysql": {
    "db_host": "127.0.0.1",
    "db_user": "root",
    "db_pass": "test",
    "db_name": "ppmessage",
},
```

此处设置PPMessage登录mysql时所需要的参数，各项设置解释如下：

选项              | 说明          
-----------------|-------------
db_host          | mysql server地址，默认连接本地数据库，值为`127.0.0.1`，无需修改
db_user          | mysql 登录用户名，默认为`root`，无需修改
db_pass          | mysql 登录密码，需要将其设置为你的mysql登录密码（安装mysql时会提示设置密码）
db_name          | ppmessage数据库名，默认为`ppmessage`，无需修改

#### 服务器设置

```python
"server": {
    "name": "127.0.0.1",
    "identicon_store": "/usr/local/opt/ppmessage/identicon",
    "generic_store": "/usr/local/opt/ppmessage/generic",
},
```

此处设置PPMessage服务器IP，文件存储路径。

选项              | 说明          
-----------------|-------------
name             | 服务器IP，例如`191.168.0.110`，PPKefu需要读取此设置，决定要连接哪个服务器
identicon_store  | PPCom用户头像文件存储路径
generic_store    | 普通文件存储路径

#### js 设置
```python
"js": {
    "min": "no", # "no" or "yes"
},
```

设置`js.min`为`yes`，PPCom，PPConsole执行gulp任务时会压缩js, css文件，为`no`则不压缩。

#### nginx 设置

```python
"nginx": {
    "nginx_conf_path": "/usr/local/nginx/conf/nginx.conf",
    "server_name": ["ppmessage.com", "www.ppmessage.com"],
    "listen": "8080", #80

    "upload_store": "/usr/local/opt/ppmessage/uploads 1",
    "upload_state_store": "/usr/local/opt/ppmessage/upload_state",

    "ssl": "off", # off/on
    "ssl_listen": "443",
    "ssl_certificate": "/Users/dingguijin/ppmessage/ppmessage/certs/ppmessage.cn.instant/issue/ssl_bundle.crt",
    "ssl_certificate_key": "/Users/dingguijin/ppmessage/ppmessage/certs/ppmessage.cn.instant/server.key",
},

```

各项设置说明如下：

选项              | 说明          
-----------------|-------------
nginx_conf_path  | nginx配置文件路径，在Mac下部署时，路径为`/usr/local/etc/nginx/nginx.conf`，在Linux下或用Docker部署时，路径为`/usr/local/nginx/conf/nginx.conf`
server_name      | 服务器名称，格式为 `[some-server.com`, `www.some-server.com]`
listen           | nginx监听的端口，开发时设为8080，发布时设为80
upload_store     | 通过nginx上传文件时的存储路径
upload_state_store | 通过nginx上传文件时保存进度的目录
ssl              | 设为off使用http协议，设为on使用https协议
ssl_listen       | ssl 端口
ssl_certificate  | ssl 证书
ssl_certifcate_key | ssl 证书密钥


#### apns 设置

```python
"apns": {
    "name": "your-app's-bundle-id",
    "dev": "/path-to-your-apns-development.p12",
    "pro": "/path-to-your-apns-production.p12"
},
```

#### gcm 设置

```python
"gcm": {
    "api_key": "your gcm api key",
    "sender_id": "your gcm sender id"
},
```





















