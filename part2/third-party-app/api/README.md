# API 列表

调用API的格式为

```
https://ppmessage.com/api/xxxxx
```

`api_level`：获取到的`token`有固定的`api level`，使用该`token`只用调用该`api_level`对应的`API`接口。



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
user_language          | string    | 用户语言，可为"en", "zh-cn", "zh-tw"
user_password          | string    | 用户密码
is_service_user        | boolean   | 用户是否是客服
user_status            | string    | 用户状态，值可为"OWNER_0", "OWNER_1", "OWNER_2", "OWNER_3", "ADMIN", "SERVICE", "ANONYMOUS", "THIRDPARTY"。如果不提供，默认为"THIRDPARTY"


返回结果（例子）：
```
{
    'user_status': u'SERVICE',
    'uuid': '97f90762-1c10-11e6-9869-0242ac110002',
    'error_string': 'success.',
    'is_anonymous_user': False,
    'user_name': u'dancer-info@ppmessage.com',
    'user_password': u'40bd001563085fc35165329ea1ff5c5ecbdbbeef',
    'user_fullname': u'dancer-info',
    'uri': '/PP_CREATE_USER',
    'user_language': None,
    'error_code': 0,
    'user_email': u'dancer-info@ppmessage.com'
}
```


#### 删除用户
```
POST /PP_REMOVE_USER
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**user_uuid**          | string    | 用户uuid
**user_password**      | string    | 用户密码

返回结果（例子）

```
{
    'error_cdoe': 0,
    'error_string': 'success.',
    'uri': '/PP_REMOVE_USER'
}
```


#### 更新用户
```
POST /PP_UPDATE_USER
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 用户uuid
is_distributor_user    | boolean   | 设置用户是否是distributor user
old_password           | string    | 旧密码
new_password           | string    | 新密码

返回结果（例子）

```
{
    'error_cdoe': 0,
    'error_string': 'success.',
    'uri': '/PP_UPDATE_USER'
}
```


#### 创建设备
```
POST /PP_CREATE_DEVICE
```

api_level:
```
PPCOM
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 用户uuid
**device_id**          | string    | 设备id
**device_ostype**      | string    | 设备操作系统类型
**ppcom_trace_uuid**   | string    | PPCom在浏览器端标示用户的uuid

说明 
```
"AND", # ANDROID
"IOS", # IOS
"ANB", # ANDROID BROWSER
"IOB", # IOS BROWSER
"WIP", # WIN PHONE
"MAC", # MAC OS X PC
"LIN", # LINUX PC
"WIN", # WINDOWS PC
"MAB", # MAC BROWSER
"LIB", # LINUX BROWSER
"WIB", # WINDOWS BROWSER
"W32", # WINDOWS 32 BIT
"W64", # WINDOWS 64 BIT
```

返回结果（例子）
```
{
    'error_code': 25,
    'uri': '/PP_CREATE_DEVICE',
    'error_string': 'device existed.',
    'device_uuid': '3534d9da-1828-11e6-946e-0242ac110002'
}
```


#### 更新设备
```
POST /PP_UPDATE_DEVICE
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**device_uuid**        | string    | 设备uuid
device_fullname        | string    | 设备全称
device_phonenumber     | string    | 设备电话号码
device_ostype          | string    | 设备操作系统类型
device_osversion       | string    | 设备操作系统版本
device_android_apilevel| string    | 安卓设备api level
device_android_gcmtoken| string    | 安卓设备gcm token
device_android_gcmpush | boolean   | 安卓设备是否使用gcm推送
device_ios_model       | string    | iOS设备model
device_ios_token       | string    | iOS设备token
device_is_online       | string    | 设备是否在线


返回结果（例子）

```
{
    'error_cdoe': 0,
    'error_string': 'success.',
    'uri': '/PP_UPDATE_DEVICE'
}
```


#### 创建对话
```
POST /PP_CREATE_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 设备全称
**conversation_type**  | string    | 对话类型，可为"P2S", "S2S"
conversation_name      | string    | 对话名称
member_list            | list      | 成员列表，如果对话类型为S2S，则必须提供此参数
group_uuid             | string    | 对话的组uuid

返回结果（例子）

```
{
    'status': 'NEW',
    'conversation_type': u'S2S',
    'conversation_icon': None,
    'uuid': '92035b7a-1c1d-11e6-a4dd-0242ac110002',
    'createtime': datetime.datetime(2016, 5, 17, 10, 53, 21, 73728),
    'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 21, 73728),
    'group_uuid': None,
    'createtimestamp': 1463482401.073728,
    'app_uuid': u'1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': 'right',
    'updatetimestamp': 1463482401.073728,
    'assigned_uuid': u'89d63aee-1c1d-11e6-a4dd-0242ac110002',
    'user_uuid': u'1ca235d4-17f1-11e6-9d01-0242ac110003',
    'user_list': [u'89d63aee-1c1d-11e6-a4dd-0242ac110002']
}
```


#### 更新对话
```
POST /PP_CREATE_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 设备全称
**conversation_type**  | string    | 对话类型，可为"P2S", "S2S"
conversation_name      | string    | 对话名称
member_list            | list      | 成员列表，如果对话类型为S2S，则必须提供此参数
group_uuid             | string    | 对话的组uuid

返回结果（例子）

```
{
    'status': 'NEW',
    'conversation_type': u'S2S',
    'conversation_icon': None,
    'uuid': '92035b7a-1c1d-11e6-a4dd-0242ac110002',
    'createtime': datetime.datetime(2016, 5, 17, 10, 53, 21, 73728),
    'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 21, 73728),
    'group_uuid': None,
    'createtimestamp': 1463482401.073728,
    'app_uuid': u'1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': 'right',
    'updatetimestamp': 1463482401.073728,
    'assigned_uuid': u'89d63aee-1c1d-11e6-a4dd-0242ac110002',
    'user_uuid': u'1ca235d4-17f1-11e6-9d01-0242ac110003',
    'user_list': [u'89d63aee-1c1d-11e6-a4dd-0242ac110002']
}
```




















