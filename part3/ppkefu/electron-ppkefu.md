# Electron PPKefu

PPKefu是一个[Electron](http://electron.atom.io/)项目, 支持Mac, Mac App Store, windows 64bit/32bit, Linux

### 说明
进入PPKefu目录
    
    cd ~/Documents/ppmessage/ppmessage/ppkefu/ppkefu
    
与Electron相关的主要三个文件:
    
    package.json,        定义打包electron应用， 安装程序的npm scripts
    www/package.json,    定义electron应用名字，版本，主文件名字
    www/main.js,         electron运行的主文件
    
运行 electron

    npm run dev  或者 npm run start
    
生成安装包，在Mac执行

    npm build:osx
    
在windows下，需要先安装NSIS 2.x, 并把NSIS的主目录加入到环境变量中，然后执行
    
    npm build:win32
    
    npm build: win64
    
更多信息请参考 package.json
