# 阿里云对象存储(OSS)部署前端项目并使用自动脚本上传。

## 配置 阿里云对象存储(OSS)

首先登陆阿里云oss控制台，点击创建一个bucket。

![1569852346504](http://img.flura.cn/1569852346504.png)



根据自己的需求选择参数。

![1569852446019](http://img.flura.cn/1569852446019.png)



然后就创建了一个bucket。

![1569852577526](http://img.flura.cn/1569852577526.png)



为bucket配置域名，在上图中，将阿里云外网访问Bucket域名记录下来。然后在DNS控制台添加记录解析。然后回到oss控制台，在**域名管理**选项 将你刚刚DNS解析的域名 绑定上去。这样就可以通过自己设置的二级域名访问到自己的项目了。

![Bucket域名](http://img.flura.cn/1569852876717.png)

![DNS控制台解析](C:\Users\32761\AppData\Roaming\Typora\typora-user-images\1569853154407.png)

![域名管理](http://img.flura.cn/1569853473577.png)

在**基础设置**找到静态页面 设置默认首页的文件名 一般都是index.html

![1569853929467](http://img.flura.cn/1569853929467.png)

就下来就只要将自己的打包出来的静态文件 通过deploy.js脚本上传到OSS上就行了



## 配置deploy.js

打开deploy.js将bucket,region填入。key，secret可能忘记(在刚开始使用阿里云的时候，阿里云会将这个发送给你，并提醒你保存)，可以在**用户信息管理** **安全信息管理**获取到自己的Access Key Secret(也可以在这里创建一个新的AccessKey)。

![1569854391813](http://img.flura.cn/1569854391813.png)



![用户信息管理界面](http://img.flura.cn/1569854935227.png)

这样再稍微配置下要部署的项目 就可以用这个脚本了。

## 使用

将deploy.js下载到你的项目根目录下。一般是webpack打包而成的单页面应用。页面打包生成dist文件夹目录，将dist文件夹上传到阿里云oss上。

在package.json中加入这个脚本命令，用来更快的执行部署命令。也可以手动node deploy.js执行部署脚本。

```
"scripts": {
  "deploy": "node deploy.js"
},
"devDependencies": {
  "ali-oss": "^6.1.1",  // 这是阿里云的oss依赖，也可以直接手动npm install ali-oss --save-dev
}
```

### 演示

在这里 我演示一个将ant-design-pro构建的项目打包上传到oss上。

![1569923829980](http://img.flura.cn/1569923829980.png)

然后就可以访问到了(记得一定要在oss控制台设置index.html为首页)

![1569928381648](http://img.flura.cn/1569928381648.png)