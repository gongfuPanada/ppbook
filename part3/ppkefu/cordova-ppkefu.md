# Cordova PPKefu

PPKefu是一个[Cordova](https://cordova.apache.org/)项目，支持android, ios平台

### 准备工作
首先安装nodejs, 请参考[nodejs官网](https://nodejs.org/)的介绍安装。然后用npm 安装cordova, ionic

    sudo npm install -g cordova
    sudo npm install -g ionic
    
### 初始化
进入ppkefu目录

    cd ~/Documents/ppmessage/ppmessage/ppkefu/ppkefu
    
1. 打开package.json, 找到cordovaPlugins中的phonegap-plugin-push

        {
          "variables": {
              "SENDER_ID": "878558045932"
          },
          "locator": "phonegap-plugin-push",
          "id": "phonegap-plugin-push"
        },
    
    将SENDER_ID改为你的gcm sender id。有关gcm, 请参考[google cloud message](https://developers.google.com/cloud-messaging/)。
    如果你不想使用gcm推送服务，SENDER_ID可以随意填写（非空即可）。
    
2. 使用ionic恢复plugins和platforms

        ionic state restore
    
3. 使用ionic 运行andorid, ios

    现在可以使用cordova 或 ionic 命令

        ionic run android
        ionic build android

    对于iOS，首先
        ionic prepare ios
        open platforms/ios/PPMessage.xcodeproj
    
    然后用 Xcode 运行PPKefu。