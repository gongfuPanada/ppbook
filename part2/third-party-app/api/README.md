# API 列表

调用API的格式为

```
https://ppmessage.com/api/xxxxx
```

`api_level`：获取到的`token`有固定的`api level`，使用该`token`只用调用该`api_level`对应的`API`接口。
在下面的API列表中，用数字指代各种`api_level`。

api_level               | number
------------------------|--------------------
PPCOM                   | 0
PPKEFU                  | 1
PPCONSOLE               | 2
THIRD_PARTY_KEFU        | 3
THIRD_PARTY_CONSOLE     | 4
PPCONSOLE_BEFORE_LOGIN  | 5


API列表：

uri                         | app_uuid | api_level       | short descriptions
----------------------------|----------|-----------------|--------------------
/PP_CREATE_ANONYMOUS        | yes      | 0               | 创建匿名用户
/PP_CREATE_USER             | yes      | 2, 4            | 创建新用户
/PP_REMOVE_USER             | no       | 2, 4            | 删除用户
/PP_UPDATE_USER             | yes      | 0, 1, 2, 3, 4   | 更新用户
/PP_CREATE_DEVICE           | yes      | 0, 1, 3         | 创建新设备
/PP_UPDATE_DEVICE           | no       | 0, 1, 3         | 更新设备
/PP_CREATE_CONVERSATION     | yes      | 0, 1, 3         | 创建对话
/PP_UPDATE_CONVERSATION     | yes      | 0, 1, 3         | 更新对话
/PP_GET_CONVERSATION_INFO   | yes      | 0, 1, 2, 3, 4   | 获取对话信息


#### 创建匿名用户
```
POST /PP_CREATE_ANONYMOUS
```

api_level:
```
PPCom
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队的app_uuid
**ppcom_trace_uuid**   | string    | ppcom在浏览器端标示该匿名用户的uuid

返回结果（例子）：
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_CREATE_ANONYMOUS',
    'user_fullname': 'Unknown Area.User',
    'user_icon': 'http://127.0.0.1:8080/identicon/7dac54f4-1b11-11e6-8b7a-0242ac110002.png',
    'user_uuid': '7dac54f4-1b11-11e6-8b7a-0242ac110002',
    'user_email': '7dac54@1ca35f'
}
```

#### 创建用户
```
POST /PP_CREATE_USER
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队的app_uuid
**user_email**         | string    | 用户的登录邮箱
**user_fullname**      | string    | 用户的全称
user_status            | string    | 用户状态，值可为"OWNER_0", "OWNER_1", "OWNER_2", "OWNER_3", "ADMIN", "SERVICE", "ANONYMOUS", "THIRDPARTY"。如果不提供，默认为"THIRDPARTY"
user_language          | string    | 用户语言，可为"en", "zh-cn", "zh-tw"
user_password          | string    | 用户密码
is_service_user        | boolean   | 用户是否是客服


返回结果（例子）：
```

```


































