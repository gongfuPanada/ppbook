## PPCom iOS SDK 集成使用说明：

### 界面

#### iOS SDK 包含三个界面：

- 会话列表界面
- 聊天界面
- 会话成员界面

#### 会话列表界面

会话列表界面对应的是`PPConversationsViewController`，与当前用户所对应的所有会话都会显示在这个`Controller`中。点击会话列表中的任一`Conversation`，就可以打开此会话对应的聊天界面，进行聊天。此界面也是`SDK`的入口界面。

#### 聊天界面

聊天界面对应的是`PPMessagesViewController`，用户可以在手机上通过此界面与客服进行对话沟通。

#### 会话成员界面

在聊天界面中，点击右上角的`Group`按钮，将会显示当前正在聊天的`Conversation`的所有成员界面。即`PPGroupMembersViewController`。在此界面中，展示了当前会话下的所有成员信息，用户可以点击任一客服人员，选择单独与其进行对话咨询。

### 集成

#### 第一步 从官网下载`PPComLib.framework`和`PPComLib.bundle`
  [下载 PPCom iOS SDK]()
  
#### 第二步 导入到项目中

直接拖动`PPComLib.framework`和`PPComLib.bundle`到你的项目中去，松开鼠标之后，`XCode`会提示你设置一些拷贝信息，这个时候勾选上`Copy items if needed`前面的复选框，以确保真正的拷贝到了你的项目中去。

#### 第三步 导入动态链接库

添加动态链接库`libicucore.dylib`或`libicucore.tbd`到你的项目中。在`TARGETS-General`面板中，点击最下面的`+`号，在弹出的对话框按钮中搜索`libicucore.dylib`或`libicucore.tbd`，然后点击`Add`将其添加至你的项目中。

#### 第四步 修改项目编译参数

在项目的`TARGETS-Build Settings`设置中找到`Other Linker Flags`选项，然后将其值添加如下参数`-ObjC -all_load`，以确保能够编译通过。

#### 第五步 引入头文件

```obj-c
#import <PPComLib/PPComLib.h>
```
    
#### 第五步 继承`PPConversationsViewController`，并初始化

```obj-c
// FeedbackMessagesViewController.h 文件
#import <PPComLib/PPComLib.h>
    
@interface FeedbackMessagesViewController : PPConversationsViewController
@end
    
// FeedbackMessagesViewController.m 文件
#import FeedbackMessagesViewController.h
    
@implementation FeedbackMessagesViewController ()
    
- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear:animated];
        
    self.title = @"会话列表";
    self.appUUID = `从官网申请到的APP_UUID`;
        
    [self initialize]; // 匿名用户初始化
    [self initializeWithUserEmail:USER_EMAIL] // 具名用户初始化，二者只能选其一
}
    
@end
```

### 小结

至此，iOS SDK 的集成与使用，已经全部介绍完毕。在集成过程中，如果有任何不明白的地方，您可以参考附件中提供的`PPComDemo`项目来进行配置，或者可以访问我们的[官网](https://www.ppmessage.com)咨询客服。