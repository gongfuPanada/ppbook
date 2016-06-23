# 配置PPMessage

运行PPMessage前，需要对PPMessage做一些全局设置。

#### 生成配置文件
> 启动 ppmessage.py，如果是首次使用那么使用浏览器访问 http://127.0.0.1:8945 就会进入配置界面。判断是否配置过的唯一标准是`ppmessage/bootstrap/config.json`这个文件是否存在且其中的`configed: true`。如果想重新配置系统哦，只需要将这个json文件删除，再次启动 ppmessage.py。

```bash
python ppmessage.py
```


```bash
cd ~/Documents/ppmessage/ppmessage/bootstrap
more config.json
```

#### 配置文件说明

配置文件里有如下设置项目：

#### 超级管理员

```python
"user": {
    "user_language": "",
    "user_fullname": "",
    "user_email": "",
    "user_password": "",
},
```

此用户是超级管理员，可以管理 PPMessage下的所有用户和客服组。各项设置介绍如下：

选项             | 说明          
-----------------|-------------
user_language    | 管理员的语言设置，决定系统创建PPCom匿名用户时，用何种语言生成用户名，以及PPCom的默认欢迎信息语言。可选zh_cn(简体中文), zh_tw(繁体中文), en_us(英文)
user_fullname    | 管理员的全名
user_email       | 管理员的登录邮箱
user_password    | 管理员的登录密码


#### 超级管理员客服团队

```python
"team": {
    "app_uuid": "",
    "app_name": ""
}
```

此团队是超级管理员的客服团队，各项设置解释如下：

选项              | 说明          
-----------------|-------------
app_uuid         | 客服团队的唯一标识
app_name         | 客服团队的名称


#### mysql 设置

```python
"mysql": {
    "db_host": "127.0.0.1",
    "db_port": "3306",
    "db_user": "root",
    "db_pass": "test",
    "db_name": "ppmessage",
},
```

此处设置PPMessage登录mysql时所需要的参数，各项设置解释如下：

选项              | 说明          
-----------------|-------------
db_host          | mysql server地址，默认连接本地数据库，值为`127.0.0.1`
db_port          | mysql server端口，默认3306
db_user          | mysql 登录用户名，默认为`root`
db_pass          | mysql 登录密码，需要将其设置为你的mysql登录密码（安装mysql时会提示设置密码）
db_name          | ppmessage数据库名，默认为`ppmessage`

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
name             | 服务器名称或者IP地址，例如`191.168.0.110`，PPKefu, PPCom都需要读取这个配置
identicon_store  | PPCom用户头像文件存储路径
generic_store    | 普通文件存储路径

#### iOS 设置
> iOS推送是否配置过

```python
"iOS": {
    "configed": true or false
},
```

#### gcm 设置

```python
"gcm": {
    "api_key": "your gcm api key",
},
```

