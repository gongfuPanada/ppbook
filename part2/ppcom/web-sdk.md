# PPCom Web SDK

Web SDK帮助开发者在Web端集成PPCom。

### 集成 Web SDK
集成Web sdk之前你应该在PPConsole创建一个客服团队，然后在团队设置-基本信息栏获取团队uuid(下文的app_uuid），之后可以选择**嵌入代码**或者**加载文件**两种方式进行Web集成。

#### 1. 嵌入代码
PPConsole的**团队设置-应用集成**栏目提供了最简版本的嵌入代码。要在某一个网页中集成PPCom，只需要复制嵌入代码并将其插入到网页html文件的**body**标签之中即可。

最简版的嵌入代码示例如下，你可以参考下文的 **配置和API** 修改window.ppSettings对象。如果你想要调用其他的SDK接口，请使用下文的**加载文件**方式集成PPCom。

```html
<script>
window.ppSettings = {
    // replace app_uuid
    app_uuid:'my-app-uuid'
};
(function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
</script>
```

#### 2. 加载文件
使用直接加载Javascript脚本文件的方法集成PPCom，能确保你调用任何接口之前PPCom SDK已经加载完毕。

方法很简单，只需要将下列代码插入到html文件的**head**标签里。然后就可以在你的js源码里调用PPCom SDK接口，具体接口请参考下文的 **配置和API**。

```html
<script src="https://ppmessage.com/ppcom/assets/pp-library.min.js" type="text/javascript"></script>
```

### 使用Web SDK
网站上集成PPCom Web SDK后，你可能在以下情景下调用Web SDK接口。

* **用户打开网站，但是尚未登录**

  用户在浏览网站，但是没有登录，此时你想在网站显示PPCom，让该用户作为一个匿名用户和客服对话。
  
  ```javascript
  // boot & show PPCom
  PP.boot({
    app_uuid: 'your-app-uuid'
  });
  ```
  
* **用户登录**
 
  用户登录后，你需要重新启动PPCom，让用户作为一个登录用户和客服对话。
  
  ```javascript
  // boot ppcom
  PP.boot({
    app_uuid: 'your-app-uuid',
    user_email: 'test@test.com',
    user_name: 'test',
    user_icon: 'http://xxx/test/icon.png',
    language: 'en'
  });
  ```

* **修改用户信息**

  当登录用户修改了自身信息后，你需要告诉PPCom用户信息已更新。
  
  ```javascript
  // update ppcom user info
  PP.update({
    app_uuid: 'your-app-uuid',
    user_email: 'test@test.com',
    user_name: 'test123',
    user_icon: 'http://xxx/test/icon.png',
    language: 'zh'
  });
  ```
 
* **用户登出**

  用户退出登录后，让用户成为一个匿名用户，需要重新启动PPCom。
  
  ```javascript
    // boot ppcom
    PP.boot({
      app_uuid: 'your-app-uuid'
    });
  ```
  

### Web SDK 接口

- 配置选项
  
  在调用`PP.boot`或`PP.update`时传入参数和window.ppSettings格式一样。如果调用时不传入参数，会以window.ppSetting作为替代参数。
  
  在`window.ppSettings`中进行配置，自定义PPCom的显示图标，如下所示：

  ```javascript
  window.ppSettings = {
	//app_uuid，必填字段
	app_uuid: "xxxxxx",
	
    //第三方用户email，可选字段，不填的话，将会以匿名用户身份收发信息
	user_email: "somebody.web@ppmessage.cn",
    //用户姓名，可选字段，在客服端会显示此处填写的用户姓名
    user_name: "张三",
    //用户头像，可选字段，在客服端会显示此处填写的用户头像
    user_icon: "http://xxxx.com/avatar.png",
	//语言配置，可选字段，zh-CN:"中文"，en:"英文", 默认为中文
	language: "zh-CN",
  };
  ```

- 启动`PPCom`

  ```javascript
  PP.boot({
    app_uuid: app_uuid
  }, function(isSucess, errorCode) {
    //回调函数
  });
  ```

- 显示`PPCom`消息面板

  ```javascript
/**
 * @description 显示 PPCom
 * @return 无返回值
 */
PP.show();
```

- 隐藏`PPCom`消息面板

  ```javascript
/**
 * @description 隐藏 PPCom
 * @return 无返回值
 */
PP.dismiss();
```

- 更新`PPCom`

  ```javascript
/**
 * @description 更新 PPCom
 * @return 无返回值
 */
PP.update({
    app_uuid: app_uuid,
    user_email: xxx@qq.com
});
```

  **说明：**参数可选，不填写参数的话，则默认使用`window.ppSettings`来更新`PPCom`，当重新设置`window.ppSettings.user_email`的时候，必须调用此函数来更新`PPCom`

- 关闭`PPCom`

  ```javascript
PP.shutdown();
```

  **说明：**当用户注销的时候，可以调用此接口销毁用户数据，此接口将会移除掉`PPCom`。

### 错误码

当`window.ppSettings`的配置信息有误而导致`PPCom`无法正常显示的时候，`PPCom`会在浏览器的`console`中打印出相应的错误信息和错误码。

下面是所有可能出现的错误码所对应的错误描述信息。

Error Code(错误码) | Error description(错误描述)
----------------- | -------------------------------
10000             | appUUID 填写有误
10001             | 找不到 user_email 对应的用户，可能未注册或者邮箱填写有误
10002             | PPCom 暂时还无法运行在 IE9 或以下版本中
10003             | 服务不可用
10004             | user_email 不是正确的邮箱的格式
