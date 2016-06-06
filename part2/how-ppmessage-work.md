# PPMessage 如何工作

PPMessage客服平台包括PPConsole，PPKefu，PPCom，PPMessage服务器四部分。前三者属于客户端范畴，都连接着PPMessage服务器。

--------

#### PPKefu, PPConsole, PPCom 与 PPMessage服务器

    +--------------------+     1      +-----------------------+      2      +--------------------+
    |  Customer Client   +----------->+        Server         +------------>+   Service Client   |
    |                    |  message   |                       |   message   |                    |
    |     [PPCom]        +<-----------+      [PPMessage]      +<------------+      [PPKefu]      |
    +--------+-----------+     4      +--------+----+---------+      3      +----------+---------+
             ^                                 |    ^                                  ^
             |                                 |    |                                  |
           7 |                               5 |    | 6                              8 |
             |                                 |    |                                  |
             |                                 v    |                                  |
             |                        +--------+----+---------+                        |
             |                        |   Service Management  |                        |
             +------------------------+                       +------------------------+
                                      |      [PPConsole]      |
                                      +-----------------------+


1. 网站用户通过 PPCom 发送消息，PPMessage 服务器接受消息并进行处理。

2. 服务器给客服推送消息，客服通过 PPKefu 接收消息。

3. 客服通过 PPKefu 发送消息，PPMessage 服务器接收消息并进行处理。

4. 服务器给网站用户推送消息，用户通过 PPCOM 接收消息。

5. 客服管理员登录PPConsole后， 从服务器加载与其账号相关的信息。

6. 客服管理员通过 PPConsole 进行管理团队，修改配置等操作后，保存相应信息到服务器。

7. 客服管理员通过PPConsole，获取在第三方网站部署PPCom所需的代码，设置PPCom显示样式、默认行为。

8. 客服管理员通过PPConsole，打开并自动登录PPKefu。
