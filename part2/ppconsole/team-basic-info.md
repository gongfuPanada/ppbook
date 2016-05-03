# 团队基本信息

团队基本信息界面展示集成PPCom，开发第三方PPKefu和第三方PPConsole所需要的信息。

---------

#### PPCom

集成PPCom时，你需要获取客服团队的`app_uuid`，也就是**团队基本信息**里的 `Team UUID`。`app_uuid`将PPCom和你的客服团队关联起来。
    
#### 第三方PPKefu

如果你想开发自己的客服端软件（第三方PPKefu），你需要获取客服团队的`PPKefu api_key`和`PPKefu api_secret`。

PPMessage系统支持OAuth 2.0验证框架，你需要使用`api_key`和`api_secret`从PPMessage服务器获取一个`access_token`，之后就可以用这个`access_token`调用PPMessage服务器的API。

具体开发方法参见[第三方软件开发](../third-party-app.md)

#### 第三方PPConsole

与第三方PPKefu类似，只是获取的`api_key`和`api_secret`是客服团队的`PPConsole api_key`和`PPConsole api_secret`。

具体开发方法参见[第三方软件开发](../third-party-app.md)
