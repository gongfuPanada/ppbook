# 第三方PPKefu和第三方PPConsole

你可以使用PPMessage提供的API开发第三方PPKefu和PPConsole。

--------

#### 概述
当你在PPConsole上创建了客服团队之后，你可以在**团队基本信息**界面获取`app_uuid`， `PPKefu api_key`, `PPKefu api_secret`，`PPConsole api_key`，`PPConsole api_secret`。PPMessage支持OAuth 2.0验证框架，你需要使用`api_key`和`api_secret`从PPMessage服务器获取一个`access_token`，之后就可以用这个`access_token`调用PPMessage的某些API。

#### 验证过程
第三方PPKefu和PPConsole的验证过程是一样的。只是



