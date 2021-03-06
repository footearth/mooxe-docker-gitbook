# Json web token (jwt) 介绍

JSON网络令牌（JWT） 是一种 URL安全的 数据传输 方式。

JWT 约定了必须使用 压缩编码 并 经过 JSON WEB Signature（JWS） 数字签名的 JSON对象。 IETF

* 由 Auth0 团队创建的关于 jwt 的站点 http://jwt.io/
* 标准 http://tools.ietf.org/html/rfc7519

## jwt token 的组成

![](https://kjur.github.io/jsjws/jws_generate.png)
![](http://qqucg.com/wp-content/uploads/2015/03/toptal-blog-image-1426676395222-1.jpeg)

## node 下应用举例

最简使用的方式，只使用简单加密的签名验签

由于 jwt token 的数据域是可以直接反解出来的，
所以 数据域 中只存放 索引信息，如 user_id

### 签发 token

```coffeescript
jwt = require 'jsonwebtoken'

token_seed = 'example'
user_id = '000001'
orderToken = (user_id) ->
  jwt.sign
    id: user_id
  , token_seed
```

### 验证 token
```coffeescript
decodedToken = (token) ->
  jwt.verify token
  , token_seed

checkToken = (token) ->
  {id} = decodedToken token
  id
```

### 更安全的做法

* token_seed 可以是动态的，一次性的
* 也可以使用其他加密方式 -- TODO

### 其他解决方案

* [apache-shiro](http://shiro.apache.org/)
  * [这里有一份为完成的翻译稿](https://github.com/waylau/apache-shiro-1.2.x-reference)

----

## 参考资料

* [NodeJS Crypto RS-SHA256 and JWT Bearer](http://stackoverflow.com/questions/20790821/nodejs-crypto-rs-sha256-and-jwt-bearer)
* [Token-Based Authentication With AngularJS & NodeJS](http://code.tutsplus.com/tutorials/token-based-authentication-with-angularjs-nodejs--cms-22543)
* [基于Token的认证和基于声明的标识](http://codelife.me/blog/2014/03/26/token-based-authentication-and-claims-based-identity/)
* [Json Web Tokens: Introduction](http://angular-tips.com/blog/2014/05/json-web-tokens-introduction/)
* [Using JSON Web Tokens with Node.js](http://www.sitepoint.com/using-json-web-tokens-node-js/)
  * [【翻译】在Nodejs中使用JSON WEB Tokens](https://cnodejs.org/topic/53c652bfc9507b404446ee40)
* [使用JSON Web令牌无Cookie验证：一个Larvel和AngularJS案例](http://qqucg.com/211.html)
* [jsjws](http://kjur.github.io/jsjws/index.html#demo)

### Auth0

* 官方: https://auth0.com/
* 桔子: http://itjuzi.com/company/13738

* [Auth0 Webtasks：Auth0的沙盒解决方案](http://www.infoq.com/cn/news/2015/03/auth0-webtasks)
* [Auth0 融资 240 万美元，帮助开发者整合 Facebook 等身份平台](http://techcrunch.cn/2014/09/18/auth0-raises-2-4m-to-help-developers-plug-into-identity-platforms-like-facebook/)
