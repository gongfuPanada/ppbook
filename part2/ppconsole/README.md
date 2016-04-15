# PPConsole

### PPConsole 是什么？

PPConsole 是 PPMessage 的客服管理系统，提供注册账号、管理团队，部署PPCom代码，打开PPKefu等功能。


### 核心功能

    [PPConsole快速向导](quick-guide.md)


### 数据总览
数据总览提供当前客服团队下，有关PPCom用户，客服，以及用户和客服之间消息的信息，包括：

    1. 今日使用PPCom用户的人数
    2. 昨日使用PPCom用户的人数
    3. 使用PPCom用户的总人数
    4. 所有消息数目
    5. 今日PPCom用户人数，客服人数，消息数目的分时走势图
    5. 过去30天PPCom用户人数，客服人数，消息数目的每日走势图


### 历史消息
历史消息提供当前客服团队下，所有PPCom用户的对话和消息记录。


### 团队设置-基本信息
开发第三方PPConsole和PPKefu应用所需要的信息，包括:

    app_uuid: string
    ppkefu_api_key: string
    ppkefu_api_secret: string
    ppconsole_api_key: string
    ppconsole_api_secret: string
    
### 团队设置-PPCom界面
PPCom的设置选项，包括欢迎信息，是否自动弹出，按钮颜色

### 团队设置-消息推送
？？?

### 团队设置-客服
可在此添加、删除客服，添加的客服不是管理员，登录PPConsole的时候不会进入设置页面，而是直接登录到PPKefu。

### 团队设置-客服组
客服组不同于客服团队。一个客服团队里可能存在多个客服组，每个客服组里存在0到多个客服。
你可在此添加、删除客服组，将客服分配到某个客服组。当前一个客服只能链接到一个客服组。

### 团队设置-应用集成
提供部署PPCom的代码，以及预览PPCom部署效果的网址。

### 账户设置
可设置账号显示名称，修改登录密码。
