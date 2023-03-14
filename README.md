# 高校体育自动签到

## 简介

> 众所周知，让社恐在体育馆里打半个小时球是不可能的。

高校体育自动签到助手。

仅供学习用途，多运动有益身心健康 : )

请求的签名方法使用了 [FengLi666](https://github.com/FengLi666/sports)的方法。


## 使用方法

1. 配置文件

    在工作目录下创建一个 config.json , 其中包含你的账号与签到点信息。

    一个配置好的 config.json 应该看起来像这样：

    ```JSON
    {
        "userInfo": {
            "useUtoken": true,
            "phone": "11451419198",
            "password": "myPassword",
            "utoken": "1234567890abcdef1234567890abcdef"
        },
        "spotInfo": {
            "major": 11451,
            "minor": 41919,
            "uuid": "4284A66A-EA9A-4EE2-A861-AFAA7AEC95BD"
        },
        "autoSign": false
    }
    ```

    ### 登录方式

    以下两种方式选择一种即可

    1. 使用`utoken`登录：将抓包得到的utoken(应为32位的16进制字符串)填入`utoken`字段，并将`useUtoken`字段置为true即可。使用这种时登录方式，无需填写`phone`和`password`字段，并且可以免除在APP上重复登陆的情况

    2. 使用手机号和密码登录。其中，`phone`和`password`字段为高校体育账号的手机号和密码。这些信息只会被发送到高校体育服务器。

    ### 场地信息

    `spotInfo`中的`major`、`minor`、`uuid`字段为签到点信息。这三个值只能通过到签到点现场，在扫描签到信号的时候抓包获取。

    `autoSign`字段为布尔值，代表是否需要在签到前进行二次确认来防止在可签到时间段外意外签到。

2. 运行
    
    这个工具需要Nodejs环境来运行，所以请先安装Nodejs环境~（iOS推荐用下下节的快捷指令）

    安装完后点页面上的Code按钮，选Download zip，下载好后解压

    要运行这个工具，你首先需要在刚刚解压的文件夹下的打开终端，执行下面的指令来安装所需要的库。
    ```
        npm install
    ```
    
    安装完后运行下面的指令即可。
    ```
        node ./index.js
    ```

## 抓包方法

目前市面上有许多抓包软件，这里推荐iOS使用Stream软件来进行抓包，安卓可以使用HttpCanary。两款软件安装完后都需要先配置才能解密https请求，具体方法请在网上搜索。

Stream的使用教程可以参考[这个视频](https://www.bilibili.com/video/BV1Ea411g7Wq/?t=00m18s)的0:18~2:16

**安卓注意**：新版的高校体育会对ssl证书进行验证，导致抓包失败，可以通过下载老版本（如2.4.8）来解决。

1. 安装上述的抓包软件

2. 到达签到地点，开始抓包

3. 在高校体育App里选择“场地签到”，等待App扫描到需要签到的场地

4. 停止抓包，在结果中找到"POST .../dataListByDevice/2"请求，utoken在http请求头中，场地信息在响应报文中。注意minor可能会有很多，选一个填入即可。

## 更新日志

v1.0: 首次发布

v1.1: bug修复

v1.2: 加入utoken登录方法

## 快捷指令

由于本人使用苹果全家桶，而之前的codeSandbox软件在某次更新后必须登录才能使用，非常麻烦，所以制作了一个快捷指令来简化操作，可以[在这里下载](https://www.icloud.com/shortcuts/ab967cd1ea074945add2e11ba5ec43aa)，仅支持utoken登录。导入后按照提示输入抓到的utoken和场地ibeacon信息即可
