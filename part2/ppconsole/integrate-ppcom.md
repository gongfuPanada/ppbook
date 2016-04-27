# 集成 PPCom

集成PPCom界面提供了集成PPCom的嵌入代码，以及预览PPCom的网址。

------

#### 集成 PPCom

这里介绍的是通过Web端嵌入代码的方式集成PPCom，关于集成PPCom的完整介绍见[PPCom](../ppcom/web-sdk.md)。

嵌入代码格式如下，window.ppSettings对象中的app_uuid指的是客服团队的UUID。你可以在**团队基本信息**找到团队UUID。

```html
<script> 
  window.ppSettings = {app_uuid:'cd0cb63d-0b7f-11e6-a37b-ac87a30c6610'};
  (function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
</script>
```

集成PPCom界面已经给出了这段嵌入代码，你需要复制这段代码，然后把代码粘贴到你的网页html文件的**body**标签之间。类似这样：

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- your-code -->
  </head>
  <body>
    <!-- your-code -->
    <script> 
      window.ppSettings = {app_uuid:'cd0cb63d-0b7f-11e6-a37b-ac87a30c6610'};
      (function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
    </script>
  </body>
</html>
```

之后再打开这个网页，PPCom聊天图标就会出现在网页右下角。


#### 预览PPCom

预览PPCom概念：当你点击`预览PPCom`按钮时，浏览器会打开生成一个临时网页，这个网页上集成了PPCom（用到的app_uuid是你的客服团队UUID），你可以在这个网页上使用PPCom。

在往你自己的网站上集成PPCom之前，你可以通过预览PPCom来测试PPCom的功能。
