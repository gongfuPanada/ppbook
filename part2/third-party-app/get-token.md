# 获取token

获取`token`分为两个步骤，第一步是获取授权码，第二步才是获取`token`。

---

### 获取授权码 

请求格式：

```
GET https://ppmessage.com/ppauth/auth?state=xxxx&client_id=xxxx&redirect_id=xxxx&response_type=code
```

参数说明：

参数              | 说明
-----------------|-----------
`state`          | 表示客户端的当前状态，可以指定任意值，`PPMessage`服务器会原封不动地返回这个值
`client_id`      | 表示客户端的`api_key`(即`kefu api_key`和`console api_key`)
`redirect_uri`   | 表示重定向`URI`，最终获取`token`成功后，PPMessage服务器会把用户导向这个`URI`
`response_type`  | 表示授权类型，此处为授权码类型，值为`code`

返回结果：

成功获取授权码后，`PPMessage`服务器会把用户导向`PPMessage`的 **应用授权** 页面。

在**应用授权**页面，用户输入他的邮箱和密码，然后点击继续按钮。如果邮箱和密码匹配，PPMessage服务器会将用户导向你指定的`redirect_uri`，并带上授权码和`state`。

最终的uri格式：
```
http://you-site.com?code=xxxxxx&state=xxxx
```

### 获取 Token

PPMessage服务器将用户导向你的`redirect_uri`后，你能从这个uri里获取到`authorization code`和`state`。

`state`应该和你上一步提供的`state`一致。

现在你可以通过`authorization code`来获取token。

请求: 

```
POST https://ppmessage.com/ppauth/token
```

请求body参数:

参数               | 说明
------------------|-------------------------
`code`            | 你获取的授权码
`client_id`       | 表示客户端的`api_key`(即`kefu api_key`和`console api_key`)
`client_secret`   | 表示客户端的`api_secret`(即`kefu api_secret`和`console api_secret`)
`redirect_uri`    | 重定向uri, 应该和之前的一致
`grant_type`      | token 类型, 值为`authorization_code`


返回结果：

参数              | 说明
-----------------|-------------
`access_token`   | 表示`token`，用这个`token`可以调用`PPMessage API`
`token_type`     | 表示`token`类型，值为`Bearer`
`expires_in`     | 表示`token`有效时间，值为`3600*24`秒，即24小时

### 调用API

成功获取到`token`之后，你可以使用`token`调用`PPMessage API`。

* `headers`：请求`headers`必须包括`Content-Type`和`Authorization`(需要用你获取的`token`替代`xxxxxx`)。
  ```
  {
      "Content-Type": "application/json",
      "Authorization": "OAuth xxxxxx"
  }
  ```
  
* `body`: 部分API需要你提供`app_uuid`(即`kefu api_uuid`和`console api_uuid`)，或`user_uuid`(在 **应用授权** 界面输入邮箱和密码的用户)。此时body应包括相应参数。
  ```
  {
      "app_uuid": "xxxx",
      "user_uuid": "xxxx",
      ...
  }
  ```

* `uri`: 请求`uri`格式
  ```
  POST https://ppmessage.com/api/xxxx
  ```
 
* `response`: 返回结果（例子）
  ```
  {
      "list": [],
      "error_code": "0",
      "error_string": "success",
      "uri": "/PP_GET_APP_SERVICE_USER_LIST"
  }
  ```
  
  要获取所有`API`的调用方法，请查看[API列表](./api/README.md)。
