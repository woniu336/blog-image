

# Github图床使用

方法1：Jsdelivr镜像站 [https://jsd.cdn.zzko.cn](https://jsd.cdn.zzko.cn/)  （公益）

方法2：通过`Cloudflare Workers`实现反代

即使镜像站点跑路了，Cloudflare还在，速度慢点

以上方法都要配合PicGo或者PicList使用，本人使用的是PicList

配合图床工具: [PicList](https://github.com/Kuingsmile/PicList)


`PicList` 是一款基于`PicGo` 深度二次开发,云储存/图床管理和文件上传客户端工具


完美兼容PicGo


官网: https://piclist.cn


### 1.通过Cloudflare Workers实现反代

```java
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="raw.githubusercontent.com";  //反代github域名
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```

具体教程网上很多，需要你在Cloudflare有域名

### 2.配合PicList



请替换为你自己的`仓库名` 以及分支，准备好`token`

反代图

![](https://github.leshans.eu.org/woniu336/blog-image/main/img/2023-12-07_212014.png)

下图为镜像站

![](https://jsd.cdn.zzko.cn/gh/woniu336/blog-image@main/img/2023-12-07_212014.png)

> - 仓库名: `woniu336/blog-image`

> - 分支: `main`

> - 存储路径: `img/`   

> - 自定义域名1(镜像站) :  

https://jsd.cdn.zzko.cn/gh/woniu336/blog-image@main 

> - 自定义域名2(CF反代)
: https://github.leshans.eu.org/woniu336/blog-image/main  

> - 自定义域名格式: https://cdn.jsdelivr.net/gh/用户名/仓库名@分支  

图片测试:

![](https://github.leshans.eu.org/woniu336/blog-image/main/img/202310061243776.jpg)



