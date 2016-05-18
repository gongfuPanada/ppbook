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
    'uri': '/PP_CREATE_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.',
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


#### 更新对话（弃用）
```
POST /PP_UPDATE_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**conversation_uuid**  | string    | 对话uuid
**assigned_uuid**      | string    | 对话被分配给这个客服

返回结果（例子）

```
{
    'uri': '/PP_UPDATE_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### 获取对话信息
```
POST /PP_GET_CONVERSATION_INFO
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**conversation_uuid**  | string    | 对话uuid
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 用户uuid

返回结果（例子）

```
{
    'status': 'OPEN',
    'conversation_type': 'P2S',
    'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 509645),
    'uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
    'error_string': 'success.',
    'conversation_data': {
        'conversation_type': 'P2S',
        'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 511172),
        'uuid': '0ab3f9c2-1c1d-11e6-a4dd-0242ac110002',
        'conversation_uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
        'user_mute_notification': None,
        'conversation_icon': 'http://127.0.0.1:8080/identicon/351f147e-1828-11e6-946e-0242ac110002.png',
        'conversation_status': 'OPEN',
        'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
        'user_name': None,
        'conversation_name': 'Unknown Area.User',
        'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
        'createtime': datetime.datetime(2016, 5, 17, 10, 49, 34, 57641)
    },
    'latest_task': '119dab7d-98d9-42c7-f4ca-ad80f8a65fdb',
    'user_uuid': '351f147e-1828-11e6-946e-0242ac110002',
    'uri': '/PP_GET_CONVERSATION_INFO',
    'group_uuid': None,
    'conversation_icon': None,
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': None,
    'assigned_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 17, 10, 49, 34, 56363)
}
```


#### 获取客服团队下的所有对话
```
POST /PP_GET_APP_CONVERSATION_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid

返回结果（例子）

```
{
    'list': [
        {
            'status': 'OPEN',
            'conversation_type': 'P2S',
            'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 509645),
            'uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
            'latest_message': {
                'body': '2',
                'conversation_type': 'P2S',
                'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 519090),
                'uuid': '119dab7d-98d9-42c7-f4ca-ad80f8a65fdb',
                'from_uuid': '351f147e-1828-11e6-946e-0242ac110002',
                'conversation_uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
                'title': None,
                'to_device_uuid': None,
                'from_type': 'DU',
                'from_device_uuid': '3534d9da-1828-11e6-946e-0242ac110002',
                'is_development': None,
                'to_type': 'AP',
                'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
                'to_uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
                'message_body': '{
                    "ci": "0ab12db4-1c1d-11e6-a4dd-0242ac110002",
                    "ft": "DU",
                    "tt": "AP",
                    "bo": "2",
                    "ts": 1463483638.508707,
                    "mt": "NOTI",
                    "tl": null,
                    "ms": "TEXT",
                    "ti": "0ab12db4-1c1d-11e6-a4dd-0242ac110002",
                    "fi": "351f147e-1828-11e6-946e-0242ac110002",
                    "id": "119dab7d-98d9-42c7-f4ca-ad80f8a65fdb",
                    "ct": "P2S"
                 }',
                'task_status': 'PROCESSED',
                'message_type': 'NOTI',
                'createtime': datetime.datetime(2016, 5, 17, 11, 13, 58, 508707),
                'message_subtype': 'TEXT'
            },
            'latest_task': '119dab7d-98d9-42c7-f4ca-ad80f8a65fdb',
            'conversation_icon': None,
            'group_uuid': None,
            'create_user': {
                'user_firstname': None,
                'user_mute_other_mobile_device': None,
                'create_status': None,
                'user_wechat': None,
                'mobile_device_uuid': None,
                'user_company': None,
                'user_status': 'ANONYMOUS',
                'ppcom_browser_device_uuid': '3534d9da-1828-11e6-946e-0242ac110002',
                'uuid': '351f147e-1828-11e6-946e-0242ac110002',
                'user_lastname': None,
                'user_qq': None,
                'user_icon': 'http://127.0.0.1:8080/identicon/351f147e-1828-11e6-946e-0242ac110002.png',
                'user_defined': None,
                'user_mobile': None,
                'user_signature': None,
                'is_email_verified': None,
                'browser_device_uuid': None,
                'user_name': 'Unknown Area.User',
                'is_anonymous_user': True,
                'service_user_status': None,
                'ppcom_trace_uuid': 'ce4253cc-6fd6-45ae-ebe5-042e74aa46c1',
                'user_show_badge': None,
                'user_language': None,
                'latest_send_message_time': datetime.datetime(2016, 5, 12, 9, 59, 56),
                'updatetime': datetime.datetime(2016, 5, 17, 9, 59, 6, 686846),
                'user_silence_notification': None,
                'is_mobile_verified': None,
                'user_fullname': 'Unknown Area.User',
                'createtime': datetime.datetime(2016, 5, 12, 9, 59, 26),
                'user_mute_notification': None,
                'ppcom_mobile_device_uuid': None,
                'user_email': '351f14@1ca35f'
            },
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'conversation_name': None,
            'message_total_count': 1,
            'assigned_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_uuid': '351f147e-1828-11e6-946e-0242ac110002',
            'createtime': datetime.datetime(2016, 5, 17, 10, 49, 34, 56363)
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_APP_CONVERSATION_LIST',
    'error_string': 'success.'
}
```


#### 获取用户的所有对话
```
POST /PP_GET_USER_CONVERSATION_LIST
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

返回结果（例子）
```
{
    'list': [],
    'error_code': 0,
    'uri': '/PP_GET_USER_CONVERSATION_LIST',
    'error_string': 'success.'
}
```


#### 开启对话
一个对话的状态为`CLOSE`状态，当调用API接口获取对话列表时，这个对话总是会被忽略。要取消忽略，需要设置对话状态为`OPEN`，即开启对话。

```
POST /PP_OPEN_CONVERSATION
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
**conversation_uuid**  | string    | 对话uuid

返回结果（例子）
```
{
    'uri': '/PP_OPEN_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### 关闭对话
一个对话的状态为`CLOSE`状态，当调用API接口获取对话列表时，这个对话总是会被忽略。要忽略对话，需要设置对话状态为`CLOSE`，即关闭对话。

```
POST /PP_CLOSE_CONVERSATION
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
**conversation_uuid**  | string    | 对话uuid

返回结果（例子）
```
{
    'uri': '/PP_OPEN_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### 获取客服团队信息
```
POST /PP_GET_APP_INFO
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid

返回结果（例子）
```
{
    'return_offline_message': None,
    'app_name': 'ppmessage',
    'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
    'robot_user_uuid': None,
    'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
    'robot_train_track': None,
    'app_billing_email': None,
    'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'welcome_message': None,
    'app_icon': None,
    'ppcom_powered_by_visible': None,
    'ppcom_powered_by_link': None,
    'company_name': 'YOURUI',
    'ppcom_launcher_style': None,
    'ppcom_powered_by_name': None,
    'robot_train_click': None,
    'offline_message': None,
    'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
    'show_ppcom_hover': None,
    'updatetime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'app_route_policy': None,
    'error_string': 'success.',
    'robot_train_method': None,
    'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'uri': '/PP_GET_APP_INFO',
    'robot_train_chat': None,
    'app_billing_uuid': None,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'ppcom_launcher_color': None
}
```


#### 获取客服团队下所有客服
```
POST /PP_GET_APP_SERVICE_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid

返回结果（例子）
```
{
    'list': [
        {
            'updatetime': datetime.datetime(2016, 5, 18, 2, 36, 19, 726229),
            'group': None,
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            u'is_owner_user': True,
            'is_mobile_online': False,
            u'is_distributor_user': True,
            'user_email': 'jin.he@ppmessage.com',
            u'is_service_user': True
        },
        {
            'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 7),
            'group': None,
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            u'is_owner_user': False,
            'is_mobile_online': False,
            u'is_distributor_user': True,
            'user_email': 'right@ppmessage.com',
            u'is_service_user': True
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_APP_SERVICE_USER_LIST',
    'error_string': 'success.'
}
```


#### 发送消息(待完善)
```
POST /PP_SEND_MESSAGE
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid

返回结果（例子）
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_SEND_MESSAGE'
}
```


#### 获取用户uuid（需改名）
检查服务器是否有某个email对应的用户，如果没有，则创建这个用户，并返回用户uuid；如果有这个用户并且这个用户是客服，则返回错误；如果有这个用户并且这个用户不是客服，则返回用户uuid。

```
POST /PP_GET_USER_UUID
```

api_level:
```
PPCOM
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_email**         | string    | 用户邮箱
user_icon              | string    | 用户头像，如果需要创建用户，会用到
user_fullname          | string    | 用户全称，如果需要创建用户，会用到

返回结果（例子）
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_GET_USER_UUID',
    'user_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003'
}
```


#### 获取对话历史消息
获取对话中的历史消息，可以按页(`page_size, page_offset`)获取；也可以按照消息id范围(`since_id, max_id`)获取。
```
POST /PP_GET_HISTORY_MESSAGE
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**conversation_uuid**  | string    | 客服团队uuid
**page_offset**        | string    | 第几页消息
page_size              | string    | 一页消息的数目
since_id               | string    | 最早一条历史消息的id
max_id                 | string    | 最近一条历史消息的id


返回结果（例子）
```
{
   'error_code': 0,
   'error_code': 'success.',
   'uri': '/PP_GET_HISTORY_MESSAGE',
   'total_count': 23,
   'count': 12,
   'page_size': 12,
   'page_offset': 0,
   'list': [
       ...
   ],
   'max_id': 'xxxx'
}
```


#### 获取用户信息
```
POST /PP_GET_USER_INFO
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 第几页消息


返回结果（例子）
```
{
...
}
```


#### 获取客服团队的客服组列表
```
POST /PP_GET_APP_ORG_GROUP_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid

返回结果（例子）
```

```

















