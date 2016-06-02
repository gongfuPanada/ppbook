# 配置开发环境
进入PPKefu根目录

    cd ~/Documents/ppmessage/ppmessage/ppkefu/ppkefu

#### 安装依赖

    bower install 
    npm install 
    
#### 开发注意事宜
www目录下有所有的js, scss, html源代码, 开发过程中gulp 负责监听www/js, www/scss目录下的文件变化，
并实时生成合并、简化的js, css到www/build目录下。程序运行时使用的是www/build目录下的js, css, 以及
www/tempaltes下的html。

1. 首次运行，执行
   
        gulp

   这会在www/build目录下生成程序运行时所需的min.js, min.css等文件
       
2. 在编辑源代码前，需要监听文件变化，实时合并所有js, css文件
    
        gulp watch
        
3. config/build.config.js里定义了所有需要监听的js文件，添加新js文件时需要更新config/build.config.js

4. 运行gulp 任务时会重新生成config/app.config.json， 此文件定义了ppkefu连接服务器、开发者模式等选项。
    
   文件里的`overwrite`参数决定了是否每次运行gulp都更新此文件，默认每次都会更新，如果你不想的话，把`overwrite`的值改为`false`即可。

#### 运行网页版PPKefu
确认PPMessage已经运行，并且在ppkefu目录下执行过gulp，打开浏览器，在地址栏输入

    http://localhost:8080/ppkefu

就可以看到PPKefu的登录页面。
