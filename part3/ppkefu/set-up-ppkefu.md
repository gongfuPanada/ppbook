# 配置开发环境
进入PPKefu根目录

    cd ~/Documents/ppmessage/ppmessage/ppkefu/ppkefu

### 安装依赖

    bower install 
    npm install 
    
### 处理错误
如果 npm install 过程中出现 无法下载electron 的错误，你可选择以下两种处理方式：

* 不使用electron, 可以直接删掉package.json devDependencies 里有关electron的包，包括：
       
       "electron-packager": "6.0.2",
       "electron-builder": "2.1.1",
       "electron-prebuilt": "0.37.5"
       
* 使用electron，可以去[electron-release-page](https://github.com/electron/electron/releases)下载提示缺失的electron包，例如electron-v0.37.5-darwin-x64.zip，然后将下载的electron包放到~/.electron目录下。最后再次执行 npm install。
    
### 开发注意事宜
www目录下有所有的js, scss, html源代码, 开发过程中gulp 负责监听www/js, www/scss目录下的文件变化，
并实时生成合并、简化的js, css到www/build目录下。程序运行时使用的是www/build目录下的js, css, 以及
www/tempaltes下的html。

1. 首次运行，执行
   
        gulp

   这会在www/build目录下生成程序运行时所需的min.js, min.css等文件
       
2. 在编辑javascript源代码前，需要监听文件变化，实时合并所有js文件
    
        gulp watch
        
3. build.config.js里定义了所有需要监听的js文件，添加新js文件时需要更新build.config.js

4. 第一次运行gulp 任务时会生成app.config.json， 此文件定义了ppkefu连接服务器、开发者模式等选项。
    
   默认情况下，会根据PPMessage的配置文件生成app.config.json。你可以修改这个文件。如果想要恢复默认选项，
   只需要删除它，并重新运行gulp即可。

### 运行网页版PPKefu
确认PPMessage已经运行，并且在ppkefu目录下执行过gulp，打开浏览器，在地址栏输入

    http://localhost:8080/ppkefu

就可以看到PPKefu的登录页面。
