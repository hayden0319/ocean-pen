<div align="center">
  <h1 align="center">OCEAN PEN</h1>
  <p> 一个全功能的AI 让人眼前一亮的商业版GPT源码。</p>

  [体验地址](https://0oai.com) · [演示图片](./photo.md)  · [微信加群](./docs/images/qrcode.png)



  <img src="https://github.com/hayden0319/ocean-pen/blob/main/photo/%E6%88%AA%E5%B1%8F2024-01-13%2019.01.16.png" />
 
</div>

## 功能概览

现有功能：
1. 登陆注册方式：邮箱+手机号码（登陆 / 注册等等）
2. 支付：虎皮椒支付
3. 存储：腾讯云存储，图床
4. 绘画画廊：用户绘图公开展示（私有绘图不展示）
5. MJ绘画：直连mj，mj的版本，niji的版本，尺寸 图生图 参考图权重，混乱程度，风格化程度，画质，纹理平铺，混图，图生文 平移(Pan) / 扩图(Zoom) / 变幻(Vary) / 区域重绘 / Seed值获取，Midjourney绘画API、WSS、CDN反向代理支持，绘画账号池（无限量）：每个账号同时支持单独的并发线程设定，线程隔离，绘图服务关闭 + 队列数量实时查看
6. AI写真
7. 套餐积分：对话积分，绘画积分分开，套餐有限期（会员制）
8. 二级分销：好友邀请获得对应奖励，包含防止恶意自己邀请自己机制检测
9. ChatGPT：GPT-3.5、4.0所有对话模型，自定义代理、ApiHost，自定义OKHttpClient，自定义多ApiKey（账号池），支持当key异常（失效、过期、封禁）时，自定义动态处理key，支持多种Tokens计算方式，自定义Key失效后处理策略，Key全部失效告警配置，ChatGPT流式输出，function call功能（简单明了就是插件：知心天气，联网模式，ip查询等等），附加图片的ChatCompletion（就是上传一张图片会给你解析），Dall-e-3生成图片，文本转语音TTS，Speech To Text（智能语音交互）
10. PDF解析
11. 思维导图
12. TTS智能语音交互
13. SD绘画：提示词，反向提示词，SD大模型选择，LoRA模型选择，提示词相关性，采样迭代步数，尺寸比例，生成数量，随机数种子
14. 页面中英繁切换（适合海外用户）

## 技术栈
- 前端：VUE3
- 后端：Java
- 数据：MySQL5.7 + redis
## 开始使用

- 运行环境：Linux
- 域名（三个域名：用户端，管理端）
- 服务器：最低2h2g即可支持
- 对话模型的api密钥
- mj会员订阅账户
- 其他：短信，邮件，支付，图床或者存储桶

## 部署
一.服务器部署以及宝塔安装
1.先准备好一台服务器（国内或者香港以及国外的，建议香港），服务器装centos的系统
2.准备好三个域名（1.用户端，2.管理端，3.MJ的jar包连接后台管理的jar包的域名），可以用二级的域名，部署之前记得发给授权商
3.开始装宝塔
装宝塔的地址https://www.bt.cn/new/download.html
宝塔装好了
要装好以下的应用：
nginx1.2.0
MySQL5.7
Java一键部署
redis7.0

二、开始系统的部署
## 部署

### 一. 服务器部署以及宝塔安装

1. 准备一台服务器（国内、香港或国外的，建议香港），服务器安装CentOS系统。
2. 准备三个域名：
   - 用户端
   - 管理端
   - MJ的jar包连接后台管理的jar包的域名
   
   可以使用二级域名，部署前请发给授权商。
3. 安装宝塔，使用以下地址：[宝塔官网](https://www.bt.cn/new/download.html)。
   
   安装完成后，确保以下应用已安装：
   - Nginx 1.2.0
   - MySQL 5.7
   - Java（一键部署）
   - Redis 7.0

### 二. 系统部署

#### 第一步：安装Java

Java版本：17.0.8。

#### 第二步：添加数据库

数据库名称：`aimpact`。

用户名和密码都设置为：`aimpact`。

#### 第三步：导入数据库文件

数据库文件包含在每次的全量包中，现在导入。

#### 第四步：创建Java项目

1. 在宝塔的文件管理中创建一个名为`oceanpen`的文件夹。
2. 创建好之后，上传后端的压缩包。

#### 第五步：创建Java项目

1. 创建项目前先在宝塔的安全中放开两个端口：`8624`和`8080`（服务器也需放开这两个端口）。
2. 创建Java项目`aimpact`，选择项目路径为上传的`/aimpact/aimpact-java-1.0.0.jar`文件，项目端口改为`8624`，然后提交创建项目。
3. 创建Java项目`midjourney`，选择项目路径为上传的`/midjourney/midjourney-proxy-pilot-3.6.0.jar`文件，项目端口改为`8080`，然后提交。
4. 在`midjourney`的Java项目中添加授权的MJ域名。

Java项目创建完成。

#### 第六步：添加PHP

1. 添加用户端，选择纯静态。
2. 添加管理端，同样选择纯静态。
3. 创建完成后，上传对应域名的前端包到网站根目录。
4. 添加用户端包，创建`public`文件夹，并上传用户端前端包。
5. 添加管理端包，同样创建`public`文件夹，并上传管理端前端包。
6. 设置用户端网站目录指向创建的`public`文件夹，运行目录指向解压的`pc`文件夹。
7. 修改配置文件，添加以下内容：

```nginx
location / {
    try_files $uri $uri/ /index.html?$query_string;
}
location /api/ {
    proxy_pass http://localhost:8624/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_read_timeout 86400s;   
    proxy_send_timeout 86400s;
    proxy_buffering off;
}
location /voice/ {           
    root /www/uploads/likeadmin-java/voice/;       
    rewrite ^/voice/(.*)$ /$1 break;   
}
location /PDF/ {           
    root /www/uploads/likeadmin-java/PDF/;       
    rewrite ^/PDF/(.*)$ /$1 break;   
}
```

8. SSL设置可以先跳过，按照方法是可申请的。

9. 设置管理端，网站目录指向`public`文件夹，运行目录指向`admin`文件夹。
10. 修改配置文件，添加以下内容：

```nginx
location / {
    try_files $uri $uri/ /index.html?$query_string;
}
location /api/ {
    proxy_pass http://localhost:8624/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_read_timeout 86400s;   
    proxy_send_timeout 86400s;
    proxy_buffering off;
}
location /mj/ {
    proxy_pass http://localhost:8080/mj/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_read_timeout 86400s;   
    proxy_send_timeout 86400s;
    proxy_buffering off;
}
```

#### 第七步：配置PDF及语音TTS服务

在服务器`www`目录下创建`uploads/likeadmin-java`两个文件夹并赋予`777`权限。

以上为部署指南，确保按照步骤操作，确保服务器与域名正常设置。

### 访问

**项目访问**

- 对话端 访问 授权的主域名 进入对话页面
- 管理端 访问 授权的管理后台域名 进入管理页

管理员账号密码为配置项设置的 默认账号密码为 `aimpact` ``


## 版本计划
1. （更新中）SD绘画：咒语解析（选择图片，解析结果），以图生图，controlnet，tagcomplete（提示词补全功能）
2. 视频转视频：视频转绘
3. 企业知识库：训练AI机器人
4. （更新中）AI虚拟模特
5. （更新中）提示词商店
6. （更新中）易支付
7. （更新中）个人公众号登陆（无须认证）
8. 智能抠图
9. 黑白图像上色
10. AI图像修复


## 价格

- 域名在线授权
- 域名授权无限更换！
- 软妹币1800 免费修改



## 疑难解答

常见问题汇总：[点击查看](./docs/FAQ.md)

## 微信交流群
<img src="https://qr.haydenstudio.hk/console/upload/IMG_0122_9053.png" width="300" />



