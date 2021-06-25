
## 概述

浏览器SDK(Software Development Kit)位于客户端，负责守护客户端与服务端之间的通信，以及对客户端的身份识别。UI可通过调用SDK提供的函数，与服务端进行交互。下文将具体阐述SDK函数的设计。


## SDK函数

### 获取验证码

```js
sdk.sendVerCode()
```
