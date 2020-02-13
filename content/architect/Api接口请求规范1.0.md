> URL规范：http://域名/服务名/业务模块名/业务操作名  

- 查看用户列表：http://www.pujr.com/football-user/user/list
- 查看某一个用户信息：http://www.pujr.com/football-user/user/show
- 增加用户：http://www.pujr.com/football-user/user/add
- 更新用户信息：http://www.pujr.com/football-user/user/update
- 删除用户：http://www.pujr.com/football-user/user/delete
- 查看用户的好友：http://www.pujr.com/football-user/user/friendsList  

> 通信机制规范

1、所有请求都采用POST方式请求，请求参数为application/x-www-form-urlencoded编码类型的发送，返回参数为JSON数据  

2、请求参数样式示例

Body参数名称 | Body参数值说明
---|---
sign | 客户端加签、服务端验签
token | 用户访问令牌
sn | 访问流水号
tt | 秒级时间戳，客户端需要与服务端对表
ver | 客户端版本号
cinfo | 客户端设备信息
userId | 用户唯一ID

- sign采用HmacSHA256生成，算法为sha256_HMAC(String message, String secret)，其中message为sn+tt+ver+cinfo，secret为token  
- 服务端同一流水号10分钟内只处理一次
- 客户端时间戳与服务端时间戳相差2分钟则返回链接失效错误
- 用户10分钟内超过5次请求规则错误则冻结账户


3、返回参数样式
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
    "code":-1,
    "msg":"请求失败",
}