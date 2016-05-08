# Electron PPKefu

PPKefu是一个[electron](http://electron.atom.io/)项目, 支持`Mac, Mac App Store, windows 64bit/32bit, Linux`。

### 关于
进入`~/Documents/ppmessage/ppmessage/ppkefu/ppkefu`目录。
    
在此目录下，与`electron`相关的有以下三个文件:
    
    package.json,        定义electron npm 依赖，指定打包应用时使用的electron版本
    www/package.json,    指定应用名字，版本，主文件名字
    www/main.js,         运行electron应用的主文件
    
### 开发
进入`~/Documents/ppmessage/ppmessage/ppkefu/ppkefu`目录。

* 初始化`electron`

  安装`electron-prebuilt, electron-packager, electron-builder`。执行
 
 ``` 
 npm run electron set-up
 ```
 
* 运行 electron
  
  在执行过`gulp`任务，生成`PPKefu`运行所需的`js, css`文件后，执行以下命令运行`electron`。
  ```
  npm run start
  ```  

* 生成安装包
  
  * `Mac`下，生成`.dmg`安装包，执行
  
    ```
    npm run electron build-osx
    ```

  * windows下，生成`.exe`安装包
    
    需要先安装`NSIS 2.x`, 并把`NSIS`的主目录加入到环境变量中，最后执行
    
    ```
    npm run electron build-win32
    
    npm run electron build-win64
    ```

* 要获取所有与electron 相关的命令信息，执行
  
  ```
  npm run electron
  ```
  
  这会给出：
  
  ```
  Usage:
  
  Enter ppkefu root directory, run this script via npm:  
    
    npm run electron [command]
  
  Commands:
  set-up                      Install electron package and save to package.json
  clean                       Clean electron dist directory
  clean-linux                 Clean electron linux dist directory
  clean-osx                   Clean electron osx dist directory
  clean-mas                   Clean electron mas dist directory (for Mac App Store)
  clean-win32                 Clean electron win32 dist directory
  clean-win64                 Clean electron win64 dist directory
  pack-linux                  Create electron linux package
  pack-osx                    Create electron osx package
  pack-mas                    Create electron mas package (for Mac App Store)
  pack-win32                  Create electron win32 package
  pack-win64                  Create electron win64 package
  build-osx                   Create electron osx installer
  build-mas                   Create electron mas installer (for Mac App Store)
  build-win32                 Create electron win32 installer
  build-win64                 Create electron win64 installer
```
