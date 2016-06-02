# Electron PPKefu

PPKefu是一个[electron](http://electron.atom.io/)项目, 支持`Mac, Mac App Store, windows 64bit/32bit, Linux`。

#### 关于
进入`~/Documents/ppmessage/ppmessage/ppkefu/ppkefu`目录。
    
在此目录下，与`electron`相关的有以下三个文件:
    
    package.json,        定义打包electron安装包的各项设置
    www/package.json,    指定应用名字，版本，主文件名字
    www/main.js,         运行electron应用的主文件
    
#### 开发
进入`~/Documents/ppmessage/ppmessage/ppkefu/ppkefu`目录。

* 初始化`electron`

  安装`electron-prebuilt, electron-packager, electron-builder`。执行
 
 ``` 
 npm run set-up-electron
 ```
 
* 运行 electron
  
  在执行过`gulp`任务，生成`PPKefu`运行所需的`js, css`文件后，执行以下命令运行`electron`。
  ```
  npm run start
  ```  

* 生成安装包
    
    ```
    npm run dist
    ```
    更多信息请参考electron-builder的文档。
