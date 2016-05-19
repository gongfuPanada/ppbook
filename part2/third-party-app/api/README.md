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
{
    'list': [
        {
            'updatetime': '2016-05-18 04:56:45 515792',
            'user_count': 2,
            'group_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
            'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
            'conversation_uuid': None,
            'is_distributor': True,
            'group_desc': 'a dancer club',
            'group_name': 'Dancer Club',
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'createtime': '2016-05-18 04:56:26 024830'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_APP_ORG_GROUP_LIST',
    'error_string': 'success.'
}
```


#### 获取客服组信息
```
POST /PP_GET_ORG_GROUP_DETAIL
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid

返回结果（例子）
```
{
    'group_route_algorithm': None,
    'group_visible_order_for_ppcom': None,
    'updatetime': datetime.datetime(2016, 5, 18, 4, 56, 45, 515792),
    'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'error_string': 'success.',
    'conversation_uuid': None,
    'createtime': datetime.datetime(2016, 5, 18, 4, 56, 26, 24830),
    'is_distributor': True,
    'uri': '/PP_GET_ORG_GROUP_DETAIL',
    'group_desc': 'a dancer club',
    'is_root': None,
    'group_uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'group_work_time_str': None,
    'group_name': 'Dancer Club',
    'error_code': 0,
    'group_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
    'group_visible_for_ppcom': None
}
```


#### 获取客服组的客服列表
```
POST /PP_GET_ORG_GROUP_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid

返回结果（例子）
```
{
    'list': [
        {
            'updatetime': 1463547414,
            'group': {
                'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            'is_mobile_online': False,
            'user_email': 'jin.he@ppmessage.com'
        },
        {
            'updatetime': 1463482387,
            'group': {
                'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': 'right@ppmessage.com'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_ORG_GROUP_USER_LIST',
    'error_string': 'success.'
}
```


#### 创建客服组
```
POST /PP_CREATE_ORG_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_name**         | string    | 客服组名称
**group_desc**         | string    | 客服组描述信息
is_distributor         | boolean   | 是否设置为首选组

返回结果（例子）
```
{
    'group_visible_order_for_ppcom': None,
    'group_desc': 'a music club',
    'group_name': 'Music Club',
    'is_root': None,
    'group_work_time_str': None,
    'group_visible_for_ppcom': None,
    'group_route_algorithm': None,
    'updatetime': datetime.datetime(2016, 5, 18, 6, 22, 1, 125540),
    'uuid': 'd4c8c2bc-1cc0-11e6-b348-0242ac110002',
    'error_string': 'success.',
    'is_distributor': False,
    'uri': '/PP_CREATE_ORG_GROUP',
    'createtime': datetime.datetime(2016, 5, 18, 6, 22, 1, 125540),
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'error_code': 0,
    'group_icon': 'http://127.0.0.1:8080/identicon/d4c8c2bc-1cc0-11e6-b348-0242ac110002.png'
}
```


#### 更新客服组
```
POST /PP_UPDATE_ORG_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid
group_name             | string    | 客服组名称
group_desc             | string    | 客服组描述信息
group_icon             | string    | 客服组头像
is_distributor         | boolean   | 是否设置为首选组


返回结果（例子）
```
{
    'group_route_algorithm': None,
    'group_visible_order_for_ppcom': None,
    'updatetime': datetime.datetime(2016, 5, 18, 4, 56, 45, 515792),
    'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'error_string': 'success.',
    'createtime': datetime.datetime(2016, 5, 18, 4, 56, 26, 24830),
    'is_distributor': True,
    'uri': '/PP_UPDATE_ORG_GROUP',
    'group_desc': u'a dancer club',
    'is_root': None,
    'group_uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'group_work_time_str': None,
    'group_name': u'Dancer Club',
    'error_code': 0,
    'group_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
    'group_visible_for_ppcom': None
}
```


#### 删除客服组 
```
POST /PP_REMOVE_ORG_GROUP
```

api_level:
```
PPCONOSLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid

返回结果（例子）
```
{
    'error_code': 0,
    'uri': '/PP_REMOVE_ORG_GROUP',
    'error_string': 'success.'
}
```


#### 添加客服组成员
```
POST /PP_ADD_ORG_GROUP_USER
```

api_level:
```
PPCONOSLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid
**user_list**          | list      | 用户列表

返回结果（例子）
```
{
    'error_code': 0,
    'uri': '/PP_ADD_ORG_GROUP_USER',
    'error_string': 'success.'
}
```


#### 移除客服组成员
```
POST /PP_REMOVE_ORG_GROUP_USER
```

api_level:
```
PPCONOSLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid
**user_list**          | list      | 用户列表

返回结果（例子）
```
{
    'error_code': 0,
    'uri': '/PP_REMOVE_ORG_GROUP_USER',
    'error_string': 'success.'
}
```


#### 获取客服团队中不归属任何客服组的客服列表
```
POST /PP_GET_NO_GROUP_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONOSLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
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
            'user_status': 'ADMIN',
            'updatetime': '2016-05-18 04:56:54 905611',
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'is_anonymous_user': 'False',
            'user_lastname': 'He',
            'user_password': '40bd001563085fc35165329ea1ff5c5ecbdbbeef',
            'user_fullname': 'Jin He',
            'service_user_status': 'READY',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'user_signature': 'fight to the death ~',
            'user_email': 'jin.he@ppmessage.com',
            'browser_device_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
            'user_language': 'zh_cn',
            'createtime': '2016-05-12 03:25:01 000000',
            'latest_send_message_time': '2016-05-12 10:01:18 000000',
            'user_firstname': 'Jin'
        },
        {
            'user_status': 'SERVICE',
            'updatetime': '2016-05-17 10:53:07 000000',
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'is_anonymous_user': 'False',
            'user_password': '40bd001563085fc35165329ea1ff5c5ecbdbbeef',
            'user_fullname': 'right',
            'user_name': 'right@ppmessage.com',
            'createtime': '2016-05-17 10:53:07 000000',
            'user_email': 'right@ppmessage.com'
        },
        {
            'user_status': 'SERVICE',
            'updatetime': '2016-05-18 08:15:16 552382',
            'uuid': 'a7341f62-1cd0-11e6-950f-0242ac110002',
            'is_anonymous_user': 'False',
            'user_password': '40bd001563085fc35165329ea1ff5c5ecbdbbeef',
            'user_fullname': 'gitar',
            'user_name': 'gitar@ppmessage.com',
            'createtime': '2016-05-18 08:15:16 552382',
            'user_email': 'gitar@ppmessage.com'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_NO_GROUP_USER_LIST',
    'error_string': 'success.'
}
```


#### 获取客服组的对话
PPCom调用此API接口来获取某个客服组下，与当前PPCom用户关联的对话。
```
POST /PP_GET_ORG_GROUP_CONVERSATION
```

api_level:
```
PPCOM
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid
**user_uuid**          | string    | 用户uuid，此用户是PPCom用户

返回结果（例子）
```
{
    'conversation_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
    'error_code': 0,
    'uri': '/PP_GET_NO_GROUP_USER_LIST',
    'error_string': 'success.'
}
```


#### 更新对话成员
```
POST /PP_UPDATE_CONVERSATION_MEMBER
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**conversation_uuid**  | string    | 用户uuid，此用户是PPCom用户
group_uuid             | string    | 客服组uuid，设定此对话与那个客服组关联
action                 | string    | 操作类型，添加为"ADD", 删除为"REMOVE"
member_list            | list      | 需要添加或者删除的成员列表

返回结果（例子）
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_UPDATE_CONVERSATION_MEMBER'
}
```


#### 获取默认对话
PPCom调用此API来获取默认对话。
```
POST /PPCOM_GET_DEFAULT_CONVERSATION
```

api_level:
```
PPCOM
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**user_uuid**          | string    | 用户uuid，此用户是PPCom用户
**device_uuid**        | string    | 用户设备uuid，此用户是PPCom用户

返回结果（例子）
```
{
    'status': 'OPEN',
    'conversation_type': 'P2S',
    'app_name': 'ppmessage',
    'latest_task': '771d934d-9629-46df-d635-380858dd114a',
    'conversation_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
    'group_uuid': None,
    'updatetime': datetime.datetime(2016, 5, 18, 4, 43, 55, 628687),
    'app_welcome': '\xe6\x9c\x89\xe4\xbb\x80\xe4\xb9\x88\xe5\x8f\xaf\xe4\xbb\xa5\xe5\xb8\xae\xe5\xbf\x99\xe7\x9a\x84\xef\xbc\x8c\xe4\xb8\x80\xe8\xb5\xb7\xe8\x81\x8a\xe4\xb8\xa4\xe5\x8f\xa5\xe5\x90\xa7\xef\xbc\x9f',
    'uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
    'error_string': 'success.',
    'user_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
    'uri': '/PPCOM_GET_DEFAULT_CONVERSATION',
    'user_list': [
        {
            'updatetime': 1463563427,
            'group': None,
            'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'user_fullname': 'Unknown Area.User',
            'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': '9adb10@1ca35f'
        },
        {
            'updatetime': 1463547414,
            'group': None,
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            'is_mobile_online': False,
            'user_email': 'jin.he@ppmessage.com'
        },
        {
            'updatetime': 1463482387,
            'group': None,
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': 'right@ppmessage.com'
        }
    ],
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': 'Jin He,right',
    'assigned_uuid': None,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 18, 4, 43, 52, 603049)
}
```


#### 按组策略选择可加入到某个对话中的用户
```
POST /PP_SELECT_USERS_BY_GROUP_ALGORITHM
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
**group_uuid**         | string    | 客服组uuid
**conversation_uuid**  | string    | 对话uuid

返回结果（例子）
```
{
    'list': [
        '1ca235d4-17f1-11e6-9d01-0242ac110003',
        '89d63aee-1c1d-11e6-a4dd-0242ac110002'
    ],
    'error_code': 0,
    'uri': '/PP_SELECT_USERS_BY_GROUP_ALGORITHM',
    'error_string': 'success.'
}
```

#### 更新客服团队信息
```
POST /PP_UPDATE_APP_INFO
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | 客服团队uuid
app_name               | string    | 客服团队名称
app_icon               | string    | 客服团队头像
app_route_policy       | string    | 客户团队消息分发策略, 可为"ALL", "SMART", "GROUP"
welcome_message        | string    | PPCom显示的欢迎信息
ppcom_launcher_color   | string    | PPCom图标颜色
ppcom_launcher_style   | string    | PPCom图标样式

返回结果（例子）
```
{
    'return_offline_message': None,
    'app_name': 'ppmessage123',
    'robot_train_click': None,
    'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
    'robot_user_uuid': None,
    'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
    'ppcom_powered_by_visible': None,
    'robot_train_method': None,
    'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
    'ppcom_launcher_style': None,
    'robot_train_track': None,
    'show_ppcom_hover': None,
    'ppcom_powered_by_name': None,
    'app_billing_email': None,
    'updatetime': datetime.datetime(2016, 5, 18, 9, 57, 22, 455405),
    'app_route_policy': None,
    'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'error_string': 'success.',
    'welcome_message': None,
    'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'app_icon': None,
    'uri': '/PP_UPDATE_APP_INFO',
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'ppcom_powered_by_link': None,
    'robot_train_chat': None,
    'company_name': 'YOURUI',
    'app_billing_uuid': None,
    'error_code': 0,
    'offline_message': None,
    'ppcom_launcher_color': None
}
```


#### 获取某用户拥有的客服团队
```
POST /PP_GET_APP_OWNED_BY_USER
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**user_uuid**           | string    | 客服团队uuid

返回结果（例子）
```
{
    'app': {
        'return_offline_message': None,
        'app_name': 'ppmessage123',
        'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
        'robot_user_uuid': None,
        'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
        'robot_train_track': None,
        'app_billing_email': None,
        'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
        'welcome_message': None,
        'robot_train_click': None,
        'ppcom_powered_by_visible': None,
        'ppcom_powered_by_link': None,
        'company_name': 'YOURUI',
        'ppcom_launcher_style': None,
        'ppcom_powered_by_name': None,
        'app_icon': None,
        'offline_message': None,
        'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
        'show_ppcom_hover': None,
        'updatetime': datetime.datetime(2016, 5, 18, 9, 57, 22, 455405),
        'app_route_policy': None,
        'robot_train_method': None,
        'robot_train_chat': None,
        'app_billing_uuid': None,
        'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
        'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
        'ppcom_launcher_color': None
    },
    'bill': None,
    'error_code': 0,
    'uri': '/PP_GET_APP_OWNED_BY_USER',
    'error_string': 'success.'
}
```


#### 验证邮箱是否有效
```
POST /PP_IS_EMAIL_VALID
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**user_email**          | string    | 客服团队uuid

返回结果（例子）
```
{
    'valid': False,
    'uri': '/PP_IS_EMAIL_VALID',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### 创建客服团队
```
POST /PP_CREATE_APP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**user_uuid**           | string    | 用户uuid，用户是客服团队的创建者，同时也是管理员
**app_name**            | string    | 客服团队名称

返回结果（例子）
```
{
    'uri': '/PP_CREATE_APP',
    'error_code': 0,
    'error_string': 'success.',
    'uuid': '82baa504-1ce2-11e6-b4ca-0242ac110002',
    'app_name': 'nodejs',
    'app_billing_email': 'nodejs@ppmessage.com',
    'app_key': '82baa324-1ce2-11e6-b4ca-0242ac110002',
    'app_secret': '82baa464-1ce2-11e6-b4ca-0242ac110002',
    'app_route_policy': 'BROADCAST'
}
```


#### 将客服移出客服团队
```
POST /PP_LEAVE_APP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | 客服团队uuid
**user_list**           | list      | 要移除的客服列表

返回结果（例子）
```
{
    'uri': '/PP_LEAVE_APP',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### 删除客服团队
```
POST /PP_REMOVE_APP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | 客服团队uuid
**user_uuid**           | string    | 该客服团队的所有者uuid

返回结果（例子）
```
{
    'uri': '/PP_REMOVE_APP',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### 获取对话成员列表
```
POST /PP_GET_CONVERSATION_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | 客服团队uuid
**conversation_uuid**   | string    | 对话uuid

返回结果（例子）
```
{
    'list': [
        {
            'updatetime': datetime.datetime(2016, 5, 18, 9, 39, 50, 243510),
            'group': {
                'uuid': '71a93470-1cdc-11e6-bdfe-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            'is_mobile_online': False,
            'user_email': 'jin.he@ppmessage.com'
        },
        {
            'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 7),
            'group': {
                'uuid': '71a93470-1cdc-11e6-bdfe-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': 'right@ppmessage.com'
        },
        {
            'updatetime': datetime.datetime(2016, 5, 18, 9, 23, 47, 399007),
            'group': None,
            'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'user_fullname': 'Unknown Area.User',
            'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': '9adb10@1ca35f'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_CONVERSATION_USER_LIST',
    'error_string': 'success.'
}
```


#### 按页获取某个用户的对话
```
POST /PP_PAGE_USER_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | 客服团队uuid
**user_uuid**           | string    | 用户uuid
page_offset             | number    | 页码索引，按页获取时需提供此参数
page_size               | number    | 每页对话数目，按页获取时需提供此参数
min_uuid                | string    | 最旧一个对话的uuid，按uuid范围获取时需提供此参数
max_uuid                | string    | 最新一个对话的uuid，按uuid范围获取时需提供此参数

返回结果（例子）
```
{
    'list': [
        {
            'status': 'OPEN',
            'conversation_type': 'P2S',
            'updatetime': '2016-05-18 04:43:55 628687',
            'uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002', 
            'latest_message': {
                'message_body': '{
                    "ci": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                    "ft": "DU",
                    "tt": "AP",
                    "bo": "hi",
                    "ts": 1463546635.627932,
                    "mt": "NOTI",
                    "tl": null,
                    "ms": "TEXT",
                    "ti": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                    "fi": "9adb1032-1cac-11e6-bce9-0242ac110002",
                    "id": "771d934d-9629-46df-d635-380858dd114a",
                    "ct": "P2S"
                }',
                'body': 'hi',
                'updatetime': '2016-05-18 04:43:55 662741',
                'uuid': '771d934d-9629-46df-d635-380858dd114a',
                'from_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
                'from_type': 'DU',
                'message_subtype': 'TEXT',
                'conversation_type': 'P2S',
                'message_type': 'NOTI',
                'createtime': '2016-05-18 04:43:55 627932'
            },
            'latest_task': '771d934d-9629-46df-d635-380858dd114a',
            'conversation_data': {
                'updatetime': '2016-05-18 04:43:55 631181',
                'uuid': '1efdcee4-1cb3-11e6-93e2-0242ac110002',
                'conversation_uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
                'conversation_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
                'createtime': '2016-05-18 04:43:52 605386',
                'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
                'conversation_name': 'Unknown Area.User',
                'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
                'conversation_status': 'OPEN'
            },
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'from_user': {
                'user_fullname': 'Unknown Area.User',
                'user_email': '9adb10@1ca35f',
                'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
                'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002'
            },
            'user_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'createtime': '2016-05-18 04:43:52 603049'
        }
    ],
    'return_count': 1,
    'error_string': 'success.',
    'max_uuid': None,
    'total_count': 1,
    'uri': '/PP_PAGE_USER_CONVERSATION', 
    'page_size': 15,
    'min_uuid': None,
    'page_offset': 0,
    'error_code': 0
}
```


#### 按页获取对话历史消息
```
POST /PP_PAGE_HISTORY_MESSAGE
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**conversation_uuid**   | string    | 对话uuid
**page_offset**         | number    | 页码索引，如果按页获取需要提供此参数
**page_size**           | number    | 每页消息数目，如果按页获取需要提供此参数
**min_uuid**            | string    | 最旧一条消息uuid
**max_uuid**            | string    | 最新一条消息uuid

返回结果（例子）
```
{
    'return_count': 1,
    'error_string': 'success.',
    'total_count': 1L,
    'list': [
        {
            'message_body': '{
                "ci": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                "ft": "DU",
                "tt": "AP",
                "bo": "hi",
                "ts": 1463546635.627932,
                "mt": "NOTI",
                "tl": null,
                "ms": "TEXT",
                "ti": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                "fi": "9adb1032-1cac-11e6-bce9-0242ac110002",
                "id": "771d934d-9629-46df-d635-380858dd114a",
                "ct": "P2S"
            }',
            'conversation_type': 'P2S',
            'updatetime': '2016-05-18 04:43:55 662741',
            'uuid': '771d934d-9629-46df-d635-380858dd114a',
            'message_subtype': 'TEXT',
            'conversation_uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
            'from_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'body': 'hi',
            'from_type': 'DU',
            'from_device_uuid': '9ae44076-1cac-11e6-bce9-0242ac110002',
            'to_type': 'AP',
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'from_user': {
                'user_fullname': 'Unknown Area.User',
                'user_email': '9adb10@1ca35f',
                'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
                'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002'
            },
            'to_uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
            'task_status': 'PROCESSED',
            'message_type': 'NOTI',
            'createtime': '2016-05-18 04:43:55 627932'
        }
    ],
    'uri': '/PP_PAGE_HISTORY_MESSAGE',
    'page_size': 12,
    'page_offset': 0,
    'error_code': 0
}
```


#### 按页获取在线的PPCom用户
```
POST /PP_PAGE_ONLINE_PORTAL_USER
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | 客服团队uuid
**page_offset**         | number    | 页码索引
**page_size**           | number    | 每页用户数目

返回结果（例子）
```

```


#### PPKefu用户登录
```
POST /PPKEFU_LOGIN
```

api_level:
```
PPKEFU
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**user_email**          | string    | 用户登录邮箱
**terminal**            | string    | 登录设备uuid
**ostype**              | string    | 登录设备操作系统类型
token                   | string    | iOS设备token
osmodel                 | string    | 设备model
osversion               | string    | 设备操作系统版本
device_fullname         | string    | 设备全称
ios_app_development     | string    | iOS APP是否处于开发模式

返回结果（例子）
```
{
    'app': {
        'return_offline_message': None,
        'app_name': 'ppmessage123',
        'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
        'robot_user_uuid': None,
        'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
        'robot_train_track': None,
        'app_billing_email': None,
        'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
        'welcome_message': None,
        'robot_train_click': None,
        'ppcom_powered_by_visible': None,
        'ppcom_powered_by_link': None,
        'company_name': 'YOURUI',
        'ppcom_launcher_style': None,
        'ppcom_powered_by_name': None,
        'app_icon': None,
        'offline_message': None,
        'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
        'show_ppcom_hover': None,
        'updatetime': datetime.datetime(2016, 5, 18, 9, 57, 22, 455405),
        'app_route_policy': None,
        'robot_train_method': None,
        'robot_train_chat': None,
        'app_billing_uuid': None,
        'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
        'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
        'ppcom_launcher_color': None
    },
    'user_language': 'zh_cn',
    'create_status': None,
    'user_wechat': None,
    'mobile_device_uuid': None,
    'user_company': None,
    'user_status': 'ADMIN', 
    'ppcom_browser_device_uuid': None,
    'mqtt_topic': '68a2feca-1c1d-11e6-a4dd-0242ac110002/#',
    'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'user_lastname': 'He',
    'user_firstname': 'Jin',
    'user_qq': None,
    'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
    'user_defined': None,
    'user_mobile': None,
    'user_signature': 'fight to the death ~',
    'is_email_verified': None,
    'browser_device_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
    'user_name': None,
    'is_anonymous_user': False,
    'service_user_status': 'READY',
    'ppcom_trace_uuid': None,
    'user_show_badge': None,
    u'is_owner_user': True,
    'user_mute_other_mobile_device': None,
    'latest_send_message_time': datetime.datetime(2016, 5, 12, 10, 1, 18),
    u'is_service_user': True,
    'updatetime': 1463571257,
    'user_silence_notification': None,
    'is_mobile_verified': None,
    'error_string': 'success.',
    'user_fullname': 'Jin He',
    'uri': '/PPKEFU_LOGIN',
    'ppcom_mobile_device_uuid': None,
    'user_mute_notification': None,
    u'is_distributor_user': True,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'user_email': 'jin.he@ppmessage.com'
}
```


#### PPKefu用户退出登录
```
POST /PPKEFU_LOGOUT
```

api_level:
```
PPKEFU
```

参数

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | 客服团队uuid
**user_uuid**           | string    | 用户uuid
**device_uuid**         | string    | 设备uuid

返回结果（例子）
```
{
    'uri': '/PPKEFU_LOGOUT',
    'error_code': 0,
    'error_string': 'success.'
}
```
