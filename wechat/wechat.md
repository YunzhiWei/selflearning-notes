# 参考文章

* [](https://cnodejs.org/topic/555fec114eb040084cfe5d15)

* [OAuth2.0实战之微信授权篇_慕课手记](https://www.imooc.com/article/17696)

* [wechat-api Documentation](http://doxmate.cool/node-webot/wechat-api/index.html#index_%E4%BA%A4%E6%B5%81%E7%BE%A4)


# 微信公众平台设置

[微信公众平台](https://mp.weixin.qq.com)

## 设置 ==> 公众号设置

### 功能设置

* 设置JS接口安全域名

[domainurl]

* 设置网页授权域名

[domainurl]

* 下载 MP_verify_xxxxxxx.txt

> 下载到 `/[project folder]/public`
> 确保微信相关设置和代码的 setting/config 设置一致

* 设置服务器路由

```
app.use(express.static(path.join(__dirname, 'public')));
```

## 开发 ==> 基本配置

* 开发者ID（AppID）
* 开发者密码（AppSecret）
* IP 白名单
* 服务器地址（URL）
* 令牌（Token）
* 消息加解密方式

> 确保项目的 setting 目录中的 appid、appsecret、url、token 的配置正确（真正部署到生产环境时，这些信息需要删除，并保存到服务器的环境变量中）
> 确保服务器的 IP 地址在白名单之内：58.37.109.51
> 消息加解密方式根据不同情况正确选择
> 服务器地址（URL）需要能够正确解析并响应微信服务器的验证请求
> 服务器地址（URL）举例：`http://www.[domainname].com/wechat/token/check`
> 每次修改服务器配置，如果一切配置无误，则修改成功，配置生效，否则，无法完成修改（这也能够在一定程度上验证，微信服务器和代码的匹配）

## 开发 ==> 接口权限

* 未获得的接口

> 微信小店
> 设备功能

* 网页授权

> 与 __设置 ==> 公众号设置__ 是同一个配置页面

# 微信支付 | 商户平台

[微信支付商户平台](https://pay.weixin.qq.com)

## 账户中心

* 操作证书：在本机安装操作证书

* 商户信息：微信支付商户号（mchId）

* API 安全：API 密钥，设置 API 密钥（partnerKey）

## 产品中心

* 开发配置 -> 支付配置：公众号支付（authcheck）；扫码支付（notifyUrl）；
* APPID 授权管理：绑定授权（appId）

# 微信 Web 开发者工具

> 直接输入 URL，检查浏览器调试信息输出

# 开发环境 与 生产环境

切换 开发环境 与 生产环境 的时候，经常需要修改的微信配置包括：

公众号：

* 设置 ==> 公众号设置 ==> 功能设置 ==> 网页授权域名
* 开发 ==> 基本配置 ==> 服务器配置 ==> 服务器地址（URL）

商铺：

* 产品中心 ==> 开发配置 ==> 支付配置 ==> 扫码回调链接
