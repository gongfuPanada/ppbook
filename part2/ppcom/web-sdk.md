# PPCom Web SDK

Web SDK帮助开发者在Web端集成PPCom。

----

### 集成 Web SDK
集成Web sdk之前你应该在PPConsole创建一个客服团队，然后在**团队设置-基本信息**栏获取团队uuid(下文的app_uuid），之后可以选择**嵌入代码**或者**加载文件**两种方式进行Web集成。

#### 嵌入代码
PPConsole的**团队设置-应用集成**栏目提供了最简版本的嵌入代码。要在某一个网页中集成PPCom，只需要复制嵌入代码并将其插入到网页html文件的**body**标签之中即可。

最简版的嵌入代码示例如下，你可以参考下文的 **Web SDK接口** 修改window.ppSettings对象。如果你想要调用其他的SDK接口，请使用下文的**加载文件**方式集成PPCom。

```html
<script>
window.ppSettings = {
    // replace app_uuid
    app_uuid:'my-app-uuid'
};
(function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
</script>
```

#### 加载文件
使用直接加载Javascript文件的方法集成PPCom，能确保你调用任何接口之前，PPCom SDK已经加载完毕。

方法很简单，只需要将下列代码插入到html文件的**head**标签里，然后就可以在你的js源码里调用PPCom SDK接口。具体接口请参考下文的 **Web SDK接口**。

```html
<script src="https://ppmessage.com/ppcom/assets/pp-library.min.js" type="text/javascript"></script>
```

### Web SDK 接口

- 配置选项
  
  在调用`PP.boot`或`PP.update`时传入的参数和`window.ppSettings`格式一样。如果调用时不传入参数，会以`window.ppSettings`作为替代参数。
  
  `window.ppSettings`内容如下所示：

  ```javascript
  window.ppSettings = {
	// app_uuid，必填字段，是客服团队的uuid，可在PPConsole的 团队设置-基本信息 中找到
	app_uuid: "xxxxxx",
	
    // 第三方用户email，可选字段，不填则会以匿名用户身份启动PPCom，否则以具名用户身份启动PPCom
	user_email: "somebody.web@ppmessage.com",
    // 用户姓名，可选字段，客服看到的PPCom用户的名称
    user_name: "张三",
    // 用户头像，可选字段，客服看到的PPCom用户的头像
    user_icon: "http://xxxx.com/avatar.png",
	// 语言配置，可选字段，zh-CN:"中文"，en:"英文", 默认为中文，决定PPCom界面显示语言
	language: "zh-CN",
  };
  ```

- `PPCom.boot`
  
  以匿名或具名用户的身份启动PPCom。一旦启动PPCom，再次调用`PP.boot`不会重启PPCom。如果确实需要重启PPCom，你需要先调用`PP.shutdown`，然后调用`PP.boot`。
  
  参数可选，不填写参数的话，则默认使用`window.ppSettings`来启动`PPCom`。
  
  ```javascript
  PP.boot({
    app_uuid: 'your-app_uuid',
    user_name: 'ppcom-user-name',
    user_icon: 'ppcom-user-icon',
    language: 'zh-CN'
  }, function(isSucess, errorCode) {
    //回调函数
  });
  ```

- `PPCom.update`
  
  当需要更换PPCom用户，更新PPCom用户的信息（邮箱，头像，显示名称）时，调用PP.update方法。
  
  参数可选，不填写参数的话，则默认使用`window.ppSettings`来更新`PPCom`。
  
  ```javascript
  /**
   * @description 更新 PPCom
   * @return 无返回值
   */
  PP.update({
    app_uuid: 'your-app_uuid',
    user_email: 'somebody.web@ppmessage.com',
    user_name: 'new-user-name',
    user_icon: 'new-user-icon'
    user_language: 'zh-CN'
  });
  ```
  
- `PP.show`
 
  显示`PPCom`消息面板。消息面板指的是对话列表或对话界面。用户可以通过在对话列表和对话界面，点击最小化按钮隐藏消息面板。要重新显示消息面板，调用`PP.show`。

  ```javascript
  /**
   * @description 显示 PPCom
   * @return 无返回值
   */
  PP.show();
  ```

- `PP.hide`
 
  隐藏`PPCom`消息面板。消息面板指的是对话列表或对话界面。用户可以通过在对话列表和对话界面，点击最小化按钮关闭消息面板。
  
  ```javascript
  /**
   * @description 隐藏 PPCom
   * @return 无返回值
   */
  PP.dismiss();
  ```

- `PPCom.shutdown`
  
  完全移除PPCom，但是不会清空window.ppSettings对象。一旦关闭PPCom，如果想要重新显示PPCom，需要调用PP.boot方法。

  当用户注销的时候，可以调用此接口销毁用户数据，此接口将会移除掉PPCom。

  ```javascript
  /**
   * @description 关闭 PPCom
   * @return 无返回值
   */
  PP.shutdown();
  ```


### 使用Web SDK

当PPCom启动时，会根据开发者传入的参数去PPMessage服务器创建或获取一个用户（该用户属于PPMessage系统，与开发者网站用户不是一个概念）。如果PPCom启动时带着`user_email`参数，则称用户为具名用户，否则称为匿名用户。具名用户通过`user_email`将开发者网站用户和PPMessage系统用户关联起来。 

典型情景：一个有自己的用户系统（支持用户登录）的网站，集成了PPCom Web SDK。网站用户在网站上可能做出登录，修改头像，修改昵称，退出登录等操作。针对网站用户的不同行为，网站开发者需要调用不同的SDK接口来正确地显示PPCom。

考虑以下用户行为：

* **网站用户打开网站**

  用户在浏览网站，但是没有登录，此时应该将该用户视为匿名用户，并以匿名用户的身份启动PPCom。开发者可以给匿名用户指定默认名称和默认头像，如果没有指定的话，PPMessage系统会给匿名用户创建名称（根据用户IP）和头像（随机头像）。PPCom会在浏览器缓存中存储匿名用户信息，除非用户清空浏览器缓存，否则下次打开网站还是会用之前创建的匿名用户启动PPCom。
  
  如果你想让PPCom在网站一打开就自动出现，只需要创建`window.ppSettings`对象即可，SDK加载完成后会自动以此对象作为参数启动PPCom。

  ```javascript
  window.ppSettings = {
      app_uuid: 'your-app-uuid',
      user_name: 'anonymous-user',
      user_icon: 'http://xxx/anonymous-user/icon.png',
      language: 'zh-CN'
  };
  ```
  
  如果你想要自己控制PPCom何时出现，则不要创建`window.ppSettings`对象，而是直接调用`PP.boot`方法。
  
  ```javascript
  PP.boot({
    app_uuid: 'your-app-uuid',
    user_name: 'anonymous-user',
    user_icon: 'http://xxx/anonymous-user/icon.png',
    language: 'zh-CN'
  });
  ```
  
* **网站用户登录**
 
  网站用户登录网站后，开发者需要以具名用户的身份更新PPCom。这样，当网站客服收到网站用户的消息时，就能知道该用户是网站的注册用户。关键在于调用`PP.update`时传入的参数对象里必须包含`user_email`。如果网站支持显示用户名称和用户头像，开发者应该同时传入`user_name`和`user_icon`。如果没有指定的话，PPMessage系统会给该用户创建名称（根据用户IP）和头像（随机头像）。
  
  ```javascript
  PP.update({
    app_uuid: 'your-app-uuid',
    user_email: 'nameduser@test.com',
    user_name: 'named-user',
    user_icon: 'http://xxx/named-user/icon.png',
    language: 'zh-CN'
  });
  ```

* **网站用户修改自身信息**

  网站用户修改了自身信息（显示名称、头像）后，开发者需要告诉PPCom更新用户信息。`user_email`标识需要更新的用户。
  
  ```javascript
  PP.update({
    app_uuid: 'your-app-uuid',
    user_email: 'nameduser@test.com',
    user_name: 'named-user-123',
    user_icon: 'http://xxx/named-user-123/icon.png',
    language: 'en'
  });
  ```
 
* **网站用户退出登录**

  网站用户退出登录后，开发者需要以匿名用户身份更新PPCom。之前创建的匿名用户在本地已经缓存，所以此次不会创建新的匿名用户。
  
  ```javascript
    PP.update({
      app_uuid: 'your-app-uuid'
      user_name: 'anonymous-user',
      user_icon: 'http://xxx/anonymous-user/icon.png',
      language: 'zh-CN'
    });
  ```
  
### 错误码

当`window.ppSettings`的配置信息有误而导致`PPCom`无法正常显示的时候，`PPCom`会在浏览器的`console`中打印出相应的错误信息和错误码。

下面是所有可能出现的错误码所对应的错误描述信息。

Error Code(错误码) | Error description(错误描述)
----------------- | -------------------------------
10000             | app_uuid 填写有误
10001             | 找不到 user_email 对应的用户，可能未注册或者邮箱填写有误
10002             | PPCom 暂时还无法运行在 IE9 或以下版本中
10003             | 无法连接PPMessage服务器
10004             | user_email 不是有效的邮箱