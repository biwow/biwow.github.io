## URL规范：http://域名/服务名/业务模块名/业务操作名
> 1、后端系统均采用服务化拆分，每个服务负责单一职责，前端获取不同的数据需要访问不同的服务。

1. 后台管理：exchange-manage
URL:http://www.ssth.com/exchange-manage
2. 债权管理：exchange-debt
URL:http://www.ssth.com/exchange-debt
3. 投资人/机构：exchange-account
URL:http://www.ssth.com/exchange-account
4. 内容管理：exchange-cms
URL:http://www.ssth.com/exchange-cms
5. 交易管理exchange-trading
URL:http://www.ssth.com/exchange-trading
6. 结算：exchange-settlement
URL:http://www.ssth.com/exchange-settlement
7. 第三方服务：common-vendor
URL:http://www.ssth.com/common-vendor

> 2、如业务请求接口需要添删改查，所以在对应业务模块的基础上加上后缀

- 查看用户列表：http://www.ssth.com/exchange-debt/user/list
- 查看某一个用户信息：http://www.ssth.com/exchange-debt/user/show
- 增加用户：http://www.ssth.com/exchange-debt/user/add
- 更新用户信息：http://www.ssth.com/exchange-debt/user/update
- 删除用户：http://www.ssth.com/exchange-debt/user/delete
- 查看用户的好友：http://www.ssth.com/exchange-debt/user/friendsList

## 通信机制规范
> 1、所有请求都采用POST方式请求，请求参数和返回参数均为JSON数据

> 2、请求参数样式
```
# sign：客户端加签、服务端验签
# params：系统参数，如增加token、流水号、时间戳、客户端版本号、客户端唯一标识等
# data：业务参数
{
    "sign":"",
    "params":"",
    "data":{
        "name":"ssth"
    }
}
```

> 3、返回参数样式
```
# code：状态码(字符串)，成功为0，失败为非零
# msg：状态描述，成功为空，失败不为空
# data：业务参数,成功时存在
# 成功返回：
{
    "code":"0",
    "msg":null,
    "data": {
        "name":"ssth"
    }
}
# 失败返回：
{
    "code":"ME10032",
    "msg":"后台服务访问错误",
}

```

> 4、身份验证，采用token的方式，Token 扩展性更强，也更安全

是否