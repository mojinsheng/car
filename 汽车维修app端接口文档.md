# 汽车维修app端接口文档
## 目录
 1. [登陆验证机制](#login)
 - [用户注册](#login_register)
 - [司机端用户注册](#login_register_driver)
 - [登陆](#login_login)
 - [*发送用户登陆验证短信](#login_message_get)
 - [*用户短信登陆（自带注册）](#login_message_post)
 - [*发送司机登陆验证短信](#login_message_driver_get)
 - [*司机短信登陆（自带注册）](#login_message_driver_post)
 - [刷新token](#login_refresh)
 2. [个人中心](#user)
  - [用户信息](#user_user)
    * [查询自身信息](#user_user_get)
    * [修改自身信息](#user_user_put)
  - [车辆信息](#user_car)
    * [查询所有车辆信息](#user_car_list_get)
    * [添加车辆信息](#user_car_list_post)
    * [查询车辆信息](#user_car_get)
    * [修改车辆信息](#user_car_put)
    * [删除车辆信息](#user_car_delete)
  - [地址信息](#user_address)
    * [查询三级地址信息](#user_address_info_list_get)
    * [查询地址列表信息](#user_address_list_get)
    * [添加地址信息](#user_address_list_post)
    * [查询地址信息](#user_address_get)
    * [修改地址信息](#user_address_put)
    * [删除地址信息](#user_address_delete)
 3. [服务](#service)
  - [分类信息](#service_catalog)
    * [查询分类列表信息](#service_catalog_list_get)
    * [查询分类信息](#service_catalog_get)
  - [物品信息](#service_product)
    * [查询物品列表信息](#service_product_list_get)
    * [查询物品信息](#service_product_get)
  - [购物车信息](#service_ordercar)
    * [查询购物车物品列表信息](#service_ordercar_list_get)
    * [添加购物车物品信息](#service_ordercar_list_post)
    * [查询购物车物品信息](#service_ordercar_get)
    * [修改购物车物品信息](#service_ordercar_put)
    * [删除购物车物品信息](#service_ordercar_delete)
  - [订单信息](#service_order)
    * [查询订单列表信息](#service_order_list_get)
    * [生成订单](#service_order_list_post)
    * [查询订单信息](#service_order_get)
    * [删除订单信息](#service_order_delete)
    * [付款、完成订单信息](#service_order_method_post)
  - [违章记录信息](#service_rules)
    * [查询违章记录列表信息](#service_rules_list_get)
    * [查询违章记录信息](#service_rules_get)
  - [资讯分类信息](#service_newscatalog)
    * [查询资讯分类列表信息](#service_newscatalog_list_get)
    * [查询资讯分类信息](#service_newscatalog_get)
  - [资讯信息](#service_news)
    * [查询滚动资讯列表信息](#service_news_info_list_get)
    * [查询资讯列表信息](#service_news_list_get)
    * [查询资讯信息](#service_news_get)
 4. [维修厂](#maintain)
  - [汽修厂](#maintain_garage)
    * [查询汽修厂列表信息](#maintain_garage_list_get)
    * [查询汽修厂信息](#maintain_garage_get)
  - [机油](#maintain_oil)
    * [查询机油列表信息](#maintain_oil_list_get)
    * [查询机油信息](#maintain_oil_get)
  - [保养](#maintain_upkeep)
    * [查询保养列表信息](#maintain_upkeep_list_get)
    * [生成保养订单信息](#maintain_upkeep_list_post)
    * [查询保养信息](#maintain_upkeep_get)
    * [删除保养订单信息](#maintain_upkeep_delete)
    * [付款、评论保养订单信息](#maintain_upkeep_method_post)
  - [维修](#maintain_maintain)
    * [查询维修列表信息](#maintain_maintain_list_get)
    * [生成维修订单信息](#maintain_maintain_list_post)
    * [查询维修信息](#maintain_maintain_get)
    * [删除维修订单信息](#maintain_maintain_delete)
    * [付款、评论维修订单信息](#maintain_maintain_method_post)
 5. [年检](#survey)
  - [年检站信息](#survey_surveystation)
    * [查询年检站列表信息](#survey_surveystation_list_get)
    * [查询年检站信息](#survey_surveystation_get)
  - [套餐信息](#survey_combo)
    * [查询套餐列表信息](#survey_combo_list_get)
    * [查询套餐信息](#survey_combo_get)
  - [年检订单信息](#survey_survey)
    * [查询年检订单列表信息](#survey_survey_list_get)
    * [提交年检订单信息](#survey_survey_list_post)
    * [查询年检订单信息](#survey_survey_get)
    * [*删除年检订单信息](#survey_survey_delete)
    * [年检订单操作信息-查询费用、支付、确认还车](#survey_survey_method_post)
 6. [系统](#system)
  - [服务首页图片信息](#system_serviceimg_get)
  - [年检首页图片信息](#system_surveyimg_get) 
 7. [司机端](#driver)
  - [订单](#driver_order)
    * [查询订单列表信息](#driver_order_list_get)
    * [查询订单信息](#driver_order_get)
    * [抢单](#driver_order_grab_post)
    * [*听单](#driver_order_wait_post)
    * [取消订单](#driver_order_cancel_post)
    * [确认取车](#driver_order_get_post)
    * [开始年检](#driver_order_survey_post)
    * [年检已过](#driver_order_success_post)
    * [年检未过](#driver_order_fail_post)
    * [确认换车](#driver_order_return_post)
  - [账户](#driver_account)
    * [查询明细列表信息](#driver_account_list_get)
    * [查询明细信息](#driver_account_get)
    * [明细操作信息-提现](#driver_account_method_post)

```
所有的后台返回值，都以这样子的结构返回
```
|参数|类型|说明|备注|  
|---|---|---|---|  
|code|int|用户名|6-20,字母|  
|msg|char(20)|密码|6-20，字母、数字、符号|  
|data|object|json对象的数据|后面所有接口设计的都放在data里面返回|  
```
{
    'code':''
    'msg':
    'data':{}
}
```
or  

|参数|类型|说明|备注|  
|---|---|---|---|  
|code|int|用户名|6-20,字母|  
|msg|char(20)|密码|6-20，字母、数字、符号|  
|data|list|json对象的列表数据|后面所有接口设计的都放在data里面返回|  
```
{
    'code':
    'msg':
    'data':[]
}
```
|code|说明|  
|---|---|  
|100|成功|  
|200|失败|  
|300|登陆验证失败|  
|999|未开发|  

<h2 id="login">登陆验证机制</h2>

```
1.登陆成功获取user_id、token、expire
2.每次接口请求的时候，app端生成一个时间戳timestamp，使用token+timestamp进行md5，生成sign
3.然后每次请求都需要附带上user_id、timestamp、sign三个参数
4.token有时效，快过期前，请使用刷新接口获得新的token，过期没有更换的话，就只能重新登陆获取了
5.所有请求都带版本号，没带默认为0
```
|参数|类型|说明|备注|例子|  
|---|---|---|---|--|  
|user_id|int|用户id|登陆成功后返回|1|  
|timestamp|char(50)|时间戳|app自己生成|1|  
|sign|char(50)|签名|md5(token+timestamp)|asdadsa|  
|system|char(50)|系统|默认android|ios|  
|version|float|app版本|默认0|0.1|  

<h3 id="login_register">用户注册</h3>

url:/api/login/register/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|  
|password|char(20)|密码|6-20，字母、数字、符号|123456789qwer|  
|name|char(20)|昵称|无|张三|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h4 id="login_register_driver">司机端用户注册</h4>

url:/api/login/register_driver/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|  
|password|char(20)|密码|6-20，字母、数字、符号|123456789qwer|  
|name|char(20)|昵称|无|张三|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h3 id="login_login">登陆</h3>

url:/api/login/login/   
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|--|  
|phone|char(20)|电话号码|作为账号|12345678998|  
|password|char(20)|密码|6-20，字母、数字、符号|123456|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|user_id|int|用户id|无|  
|token|char(50)|凭证|无|  
|expire|datetime|有效时间|无|  
```
{
    'data':{
        'user_id':'1'
        'token':'sjkdhasjkhf123jga',
        'expire':'2018-07-08 12:23:34'
    }
}
```

<h3 id="login_message_get">发送用户登陆验证短信</h3>
无

<h3 id="login_message_driver_get">用户短信登陆（自带注册）</h3>
无

<h3 id="login_message_driver_post">司机短信登陆（自带注册）</h3>
无

<h3 id="login_refresh">刷新token</h3>

url:/api/login/refresh/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|user_id|int|用户id|无|  
|token|char(50)|凭证|无|  
|expire|datetime|有效时间|无|  
```
{
    'data':{
        'user_id':'1'
        'token':'sjkdhasjkhf123jga',
        'expire':'2018-07-08 12:23:34'
    }
}
```

<h2 id="user">个人中心</h2>

<h3 id="user_user">用户信息</h3>

<h4 id="user_user_get">查询自身信息</h4>

url:/api/user/user/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|    
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|phone|char(20)|电话号码|无|  
|name|char(10)|昵称|无|  
|pic_url|char(50)|照片url|/url,获取图片|  
|point|int|积分|无|  
|is_pass|bool|是否过审|无|  
```
{
    'data':{
        'id':1,
        'phone':'12345678998',
        'name':'admin',
        'pic':'/alsdfh.jpg',
        'point':'20',
        'is_pass':false
    }
}
```

<h4 id="user_user_put">修改自身信息</h4>

url:/api/user/user/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
|phone|char(20)|电话号码|作为账号|12345678998|  
|name|char(10)|昵称|无|admin|  
|pic|文件流|照片文件|无|(文件流，base64)|  

return:  

|参数|类型|说明|  
|---|---|---|  
```
{    
    'data':{}
}
```

<h3 id="user_car">车辆信息</h3>

<h4 id="user_car_list_get">查询所有车辆信息</h4>

url:/api/user/car/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|is_default|bool|是否为默认|无|true|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(50)|照片url|/url,获取图片|  
|brand|char(100)|品牌|无|  
|code|char(10)|车牌号码|无|  
|engine|char(100)|发动机|无|  
|buy_time|date|购车时间|无|  
|mileage|float|里程|无|  
|is_default|bool|是否默认|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'pic_url':'/alsdfh.jpg',
        'brand':'玛萨拉蒂',
        'code':'粤A24351',
        'engine':'TX21',
        'buy_time':'2018-03-20',
        'mileage':'12',
        'is_default':false
    }]
}
```

<h4 id="user_car_list_post">添加车辆信息</h4>

url:/api/user/car/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|pic|文件流|照片文件|无|(文件流，base64)|  
|brand|char(100)|品牌|无|玛萨拉蒂|  
|code|char(10)|车牌号码|无|粤A24351|  
|engine|char(100)|发动机|无|TX21|  
|buy_time|date|购车时间|无|2018-03-20|  
|mileage|float|里程|无|12|  
|is_default|bool|是否默认|无|false|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':[]
}
```

<h4 id="user_car_get">查询车辆信息</h4>

url:/api/user/car/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(50)|照片url|/url,获取图片|  
|brand|char(100)|品牌|无|  
|code|char(10)|车牌号码|无|  
|engine|char(100)|发动机|无|  
|buy_time|date|购车时间|无|  
|mileage|float|里程|无|  
|is_default|bool|是否默认|无|  

```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'pic_url':'/alsdfh.jpg',
        'brand':'玛萨拉蒂',
        'code':'粤A24351',
        'engine':'TX21',
        'buy_time':'2018-03-20',
        'mileage':'12',
        'is_default':false
    }
}
```

<h4 id="user_car_put">修改车辆信息</h4>

url:/api/user/car/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
|pic|文件流|照片文件|无|(文件流，base64)|  
|brand|char(100)|品牌|无|玛萨拉蒂|  
|code|char(10)|车牌号码|无|粤A24351|  
|engine|char(100)|发动机|无|TX21|  
|buy_time|date|购车时间|无|2018-03-20|  
|mileage|float|里程|无|12|  
|is_default|bool|是否默认|无|false|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="user_car_delete">删除车辆信息</h4>

url:/api/user/car_delete/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="user_address">地址信息</h3>

<h4 id="user_address_info_list_get">查询三级地址信息</h4>

url:/api/user/address_info/   
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|p_id|int|id|查询id下的所有下级节点，0为根结点|0|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|p_id|int|父id|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'北京市',
        'p_id':1
    }]
}
```

<h4 id="user_address_info_get">查询三级地址信息</h4>

url:/api/user/addressinfo/   
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|p_id|int|父id|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'北京市',
        'p_id':1
    }
}
```

<h4 id="user_address_list_get">查询地址列表信息</h4>

url:/api/user/address/   
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|is_default|bool|是否为默认|无|true|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|收货人姓名|无|  
|phone|char(15)|联系电话|无|  
|node1|object|第一级地址|查看三级地址信息|  
|node2|object|第二级地址|查看三级地址信息|  
|node3|object|第三级地址|查看三级地址信息|  
|address|char(100)|收货地址|无|  
|is_default|bool|是否默认|false|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'123456789984',
        'node1':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'北京市',
            'p_id':1
        },
        'node2':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'北京市',
            'p_id':1
        },
        'node3':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'北京市',
            'p_id':1
        },
        'address':'广州市越秀区xxx',
        'is_default':false
    }]
}
```

<h4 id="user_address_list_post">添加地址信息</h4>

url:/api/user/address/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|name|char(10)|收货人姓名|无|张三|  
|phone|char(15)|联系电话|无|123456789984|  
|node1|int|第一级地址|无|1|  
|node2|int|第二级地址|无|2|  
|node3|int|第三级地址|无|3|  
|address|char(100)|收货地址|无|广州市越秀区xxx|  
|is_default|bool|是否默认|无|false|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="user_address_get">查询地址信息</h4>

url:/api/user/address/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|收货人姓名|无|  
|phone|char(15)|联系电话|无|  
|node1|object|第一级地址|查看三级地址信息|  
|node2|object|第二级地址|查看三级地址信息|  
|node3|object|第三级地址|查看三级地址信息|  
|address|char(100)|收货地址|无|  
|is_default|bool|是否默认|false|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'123456789984',
        'node1':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'北京市',
            'p_id':1
        },
        'node2':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'北京市',
            'p_id':1
        },
        'node3':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'北京市',
            'p_id':1
        },
        'address':'广州市越秀区xxx',
        'is_default':false
    }
}
```

<h4 id="user_address_put">修改地址信息</h4>

url:/api/user/address/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
|name|char(10)|收货人姓名|无|张三|  
|phone|char(15)|联系电话|无|123456789984|  
|node1|int|第一级地址|无|1|  
|node2|int|第二级地址|无|2|  
|node3|int|第三级地址|无|3|  
|address|char(100)|收货地址|无|广州市越秀区xxx|  
|is_default|bool|是否默认|无|false|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="user_address_delete">删除地址信息</h4>

url:/api/user/address_delete/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h2 id="service">服务</h2>

<h3 id="service_catalog">分类信息</h3>

<h4 id="service_catalog_list_get">查询分类列表信息</h4>

url:/api/service/catalog/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|type|int|类型|0:商城，1:保险|0|  
|p_id|int|父id|根节点id为0|0|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|p_id|int|父id|0为根目录|  
|type|int|类型|无|  
|pic_url|char(100)|图标|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'过滤系统',
        'p_id':0,
        'type':0,
        'pic_url':'/asd.hpg'
    }]
}
```

<h4 id="service_catalog_get">查询分类信息</h4>

url:/api/service/catalog/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|p_id|int|父id|0为根目录|  
|type|int|类型|无|  
|pic_url|char(100)|图标|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'过滤系统',
        'p_id':0,
        'type':0,
        'pic_url':'/asd.hpg',
    }
}
```

<h3 id="service_product">物品信息</h3>

<h4 id="service_product_list_get">查询物品列表信息</h4>

url:/api/service/product/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|catalog_id|int|分类id|默认为0|1|  
|price_order|int|价格排序|0：无，1:从低到高，2:从高到低|0|  
|sale_order|int|销量排序|0：无，1:从低到高，2:从高到低|0|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|pic_url|char(100)|封面照url|无|  
|price|float|价格|无|  
|special_price|float|特价|无|  
|param|text|参数信息|无|  
|type|text|车型信息|无|  
|catalog|object|分类|查看分类查询接口|  
|amount|int|库存|无|  
|sale|int|销量|无|  
|pic_url_list|list|细节展示图片url列表|图片都放在这个文件夹下|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'轮胎',
        'pic_url':'/asd.hpg',
        'price':1200,
        'special_price':1200,
        'param':'顶配',
        'type':'顶配',
        'catalog':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'过滤系统',
            'p_id':0
        },
        'amount':666,
        'sale':666,
        'pic_url_list':['/asd.hpg','/fasda.jpg']
    }]
}
```

<h4 id="service_product_get">查询物品信息</h4>

url:/api/service/product/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
```
{
}
```
return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|pic_url|char(100)|封面照url|无|  
|price|float|价格|无|  
|special_price|float|特价|无|  
|param|text|参数信息|无|  
|type|text|车型信息|无|  
|catalog|object|分类|查看分类查询接口|  
|amount|int|库存|无|  
|sale|int|销量|无|  
|pic_url_list|list|细节展示图片url列表|图片都放在这个文件夹下|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'轮胎',
        'pic_url':'/asd.hpg',
        'price':1200,
        'special_price':1200,
        'param':'顶配',
        'type':'顶配',
        'catalog':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'过滤系统',
            'p_id':0
        },
        'amount':666,
        'sale':666,
        'pic_url_list':['/asd.hpg','/fasda.jpg']
    }
}
```

<h3 id="service_ordercar">购物车信息</h3>

<h4 id="service_ordercar_list_get">查询购物车物品列表信息</h4>

url:/api/service/ordercar/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|product|object|物品|查看物品接口|  
|amount|int|数量|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'product':
        {
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'pic_url':'/asd.hpg',
            'price':1200,
            'special_price':1200,
            'param':'顶配',
            'type':'顶配',
            'catalog':{
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'过滤系统',
                'p_id':0
            },
            'amount':666,
            'pic_url_list':['/asd.hpg','/fasda.jpg']
        },
        'amount':666
    }]
}
```

<h4 id="service_ordercar_list_post">添加购物车物品信息</h4>

url:/api/service/ordercar/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|product_id|int|物品id|无|1|  
|amount|int|数量|会在这个商品已有的基础上添加amount个，可以添加负数，最终结果只能为0|123456789984|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_ordercar_get">查询购物车物品信息</h4>

url:/api/service/ordercar/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|product|object|物品|查看物品接口|  
|amount|int|数量|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'product':
        {
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'pic_url':'/asd.hpg',
            'price':1200,
            'special_price':1200,
            'param':'顶配',
            'type':'顶配',
            'catalog':{
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'过滤系统',
                'p_id':0
            },
            'amount':666,
            'pic_url_list':['/asd.hpg','/fasda.jpg']
        },
        'amount':666
    }
}
```

<h4 id="service_ordercar_put">修改购物车物品信息</h4>

url:/api/service/ordercar/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|    
|amount|int|数量|直接修改数量|123456789984|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_ordercar_delete">删除购物车物品信息</h4>

url:/api/service/ordercar_delete/   
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|支持使用,来拼接多个id，实现批量删除|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="service_order">订单信息</h3>

<h4 id="service_order_list_get">查询订单列表信息</h4>

url:/api/service/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|status|int|状态|-1:全部，0:待付款，1:待发货，2:待收货，3:已完成|1|  
|is_comment|bool|是否评论|无|true|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单编号|无|  
|name|char(10)|收货人姓名|来源于所选地址|  
|phone|char(15)|联系电话|来源于所选地址|  
|city|char(50)|省市区|来源于所选地址|  
|address|char(100)|收货地址|来源于所选地址|  
|status|int|状态|0:待付款，1:待发货，2:待收货，3:已完成|  
|is_delete|int|删除状态，0:未删除，1:已删除|无|  
|is_comment|int|评价状态，0:未删除，1:已删除|无|  
|logistics_info|text|物流信息|无|  
|all_price|float|小计金额|无|  
|point_price|float|积分兑换|无|  
|now_price|float|实际付款|无|  
|cost_point|int|花费积分|无|  
|order_time|datetime|下单时间|无|  
|wait_time|datetime|付款时间|无|  
|send_time|datetime|发货时间|无|  
|receive_time|datetime|收货时间|无|  
|confirm_time|datetime|确认时间|无|  
|orderproduct_set|list|物品列表|无|  

orderproduct_set:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|product|object|物品|查询物品信息|  
|amount|int|数量|无|  
|price|float|价格|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'182641729647164',
        'name':'张三',
        'phone':'12345678998',
        'city':'广州市',
        'address':'广州市越秀区xxx',
        'status':0,
        'is_delete':0,
        'is_comment':0,
        'logistics_info':'asdasd',
        'all_price':300,
        'point_price':20,
        'now_price':280,
        'cost_point':280,
        'order_time':'2018-07-08 12:23:34',
        'wait_time':'2018-07-08 12:23:34',
        'send_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'orderproduct_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            {
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'轮胎',
                'pic_url':'/asd.hpg',
                'price':1200,
                'special_price':1200,
                'param':'顶配',
                'type':'顶配',
                'catalog':{
                    'id':1,
                    'create_time':'2018-07-08 12:23:34',
                    'update_time':'2018-07-08 12:23:34',
                    'name':'过滤系统',
                    'p_id':0
                },
                'amount':666,
                'sale':666,
                'pic_url_list':['/asd.hpg','/fasda.jpg']
            },
            'amount':1,
            'price':1
        }]
    }]
}
```

<h4 id="service_order_list_post">生成订单</h4>

url:/api/service/order/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|address_id|int|地址id|无|1|
|order_car_list|char(200)|购物车id列表|使用,拼接|1,2,3,4,5,6|

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_order_get">查询订单信息</h4>

url:/api/service/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单编号|无|  
|name|char(10)|收货人姓名|来源于所选地址|  
|phone|char(15)|联系电话|来源于所选地址|  
|city|char(50)|省市区|来源于所选地址|  
|address|char(100)|收货地址|来源于所选地址|  
|status|int|状态|0:待付款，1:待发货，2:待收货，3:已完成|  
|is_delete|int|删除状态，0:未删除，1:已删除|无|  
|is_comment|int|评价状态，0:未删除，1:已删除|无|  
|logistics_info|text|物流信息|无|  
|all_price|float|小计金额|无|  
|point_price|float|积分兑换|无|  
|now_price|float|实际付款|无|  
|cost_point|int|花费积分|无|  
|order_time|datetime|下单时间|无|  
|wait_time|datetime|付款时间|无|  
|send_time|datetime|发货时间|无|  
|receive_time|datetime|收货时间|无|  
|confirm_time|datetime|确认时间|无|  
|orderproduct_set|list|物品列表|无|  

orderproduct_set:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|product|object|物品|查询物品信息|  
|amount|int|数量|无|  
|price|float|价格|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'182641729647164',
        'name':'张三',
        'phone':'12345678998',
        'city':'广州市',
        'address':'广州市越秀区xxx',
        'status':0,
        'is_delete':0,
        'is_comment':0,
        'logistics_info':'asdasd',
        'all_price':300,
        'point_price':20,
        'now_price':280,
        'cost_point':280,
        'order_time':'2018-07-08 12:23:34',
        'wait_time':'2018-07-08 12:23:34',
        'send_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'orderproduct_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'product':
            {
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'轮胎',
                'pic_url':'/asd.hpg',
                'price':1200,
                'special_price':1200,
                'param':'顶配',
                'type':'顶配',
                'catalog':{
                    'id':1,
                    'create_time':'2018-07-08 12:23:34',
                    'update_time':'2018-07-08 12:23:34',
                    'name':'过滤系统',
                    'p_id':0
                },
                'amount':666,
                'sale':666,
                'pic_url_list':['/asd.hpg','/fasda.jpg']
            },
            'amount':1,
            'price':1
        }]
    }
}
```

<h4 id="service_order_method_post">付款、完成、评论订单信息</h4>

url:/api/service/order_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
|method|char(20)|操作|pay:付款，finish：完成，comment:评论|pay|  
|score|int|评分|大于等于0，小于等于5，当method为comment的时候需要|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_order_delete">删除订单信息</h4>

url:/api/service/order_delete/   
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="service_rules">违章记录信息</h3>

<h4 id="service_rules_list_get">查询违章记录列表信息</h4>

url:/api/service/rules/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|car_brand|char(100)|车辆品牌|无|  
|amount|int|违章次数|无|  
|score|int|扣分|无|  
|price|float|罚款|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'car_brand':'玛萨拉蒂',
        'amount':1,
        'score':1,
        'price':200
    }]
}
```

<h4 id="service_rules_get">查询违章记录信息</h4>

url:/api/service/rules/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|car_brand|char(100)|车辆品牌|无|  
|amount|int|违章次数|无|  
|score|int|扣分|无|  
|price|float|罚款|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'car_brand':'玛萨拉蒂',
        'amount':1,
        'score':1,
        'price':200
    }
}
```

<h3 id="service_newscatalog">资讯分类信息</h3>

<h4 id="service_newscatalog_list_get">查询资讯分类列表信息</h4>

url:/api/service/newscatalog/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|新闻资讯|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'新闻资讯'
    }]
}
```

<h4 id="service_newscatalog_get">查询资讯分类信息</h4>

url:/api/service/newscatalog/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|新闻资讯|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'新闻资讯'
    }
}
```

<h3 id="service_news">资讯信息</h3>

<h4 id="service_news_info_list_get">查询滚动资讯列表信息</h4>

url:/api/service/newsinfo/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|    

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|catalog|object|分类|查询资讯分类信息|  
|title|char(100)|标题|无|  
|content|text|内容|无|  
|pic_url|char(50)|封面url|无|  
|pic_url_list|list|图片url列表|图片都放在这个文件夹下|  
|is_bar|bool|是否是滚动资讯|会被显示在滚动区|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'catalog':
        {
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'新闻资讯'
        },
        'title':'被抢劫了',
        'content':'没钱了',
        'pic_url':'asdla.jpg',
        'pic_url_list':['/asd.hpg','/fasda.jpg'],
        'is_bar':true
    }]
}
```

<h4 id="service_news_list_get">查询资讯列表信息</h4>

url:/api/service/news/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|news_catalog_id|int|分类id|无|0|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|news_catalog|object|分类|查询资讯分类信息|  
|title|char(100)|标题|无|  
|content|text|内容|无|  
|pic_url|char(50)|封面url|无|  
|pic_url_list|list|图片url列表|图片都放在这个文件夹下|  
|is_bar|bool|是否是滚动资讯|会被显示在滚动区|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'news_catalog':
        {
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'新闻资讯'
        },
        'title':'被抢劫了',
        'content':'没钱了',
        'pic_url':'asdla.jpg',
        'pic_url_list':['/asd.hpg','/fasda.jpg'],
        'is_bar':true
    }]
}
```

<h4 id="service_news_get">查询资讯信息</h4>

url:/api/service/news/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|news_catalog|object|分类|查询资讯分类信息|  
|title|char(100)|标题|无|  
|content|text|内容|无|  
|pic_url|char(50)|封面url|无|  
|pic_url_list|list|图片url列表|图片都放在这个文件夹下|  
|is_bar|bool|是否是滚动资讯|会被显示在滚动区|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'news_catalog':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'新闻资讯'
        },
        'title':'被抢劫了',
        'content':'没钱了',
        'pic_url':'asdla.jpg',
        'pic_url_list':['/asd.hpg','/fasda.jpg'],
        'is_bar':true
    }
}
```

<h2 id="maintain">维修厂</h2>

<h3 id="maintain_garage">汽修厂</h3>

<h4 id="maintain_garage_list_get">查询汽修厂列表信息</h4>

url:/api/maintain/garage/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|name|char(50)|汽修厂名称|无|天河|  
|orderby|char(100)|排序规则|all、distance、popular|popular|  
|longitude|float|经度|必填|23|  
|latitude|float|纬度|必填|123|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|user_name|char(50)|负责人名称|无|  
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
|mobile_phone|char(20)|手机号码|无|  
|phone|char(20)|固定电话|无|   
|filter_price|float|过滤格|保养使用|  
|popular|int|人气|无|  
|pic_url|char(50)|封面url|无|  
|distance|float|距离|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'1',
        'user_name':'1',
        'longitude':223,
        'latitude':322,
        'address':'广州越秀区',
        'mobile_phone':'12345678998',
        'phone':'020-8888888',
        'filter_price':88,
        'popular':1,
        'pic_url':'asdla.jpg',
        'distance':10
    }]
}
```

<h4 id="maintain_garage_get">查询汽修厂信息</h4>

url:/api/maintain/garage/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|user_name|char(50)|负责人名称|无|  
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
|mobile_phone|char(20)|手机号码|无|  
|phone|char(20)|固定电话|无|   
|filter_price|float|过滤格|保养使用|  
|popular|int|人气|无|  
|pic_url|char(50)|封面url|无|  
|distance|float|距离|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'1',
        'user_name':'1',
        'longitude':223,
        'latitude':322,
        'address':'广州越秀区',
        'mobile_phone':'12345678998',
        'phone':'020-8888888',
        'filter_price':88,
        'popular':1,
        'pic_url':'asdla.jpg',
        'distance':10
    }
}
```

<h3 id="maintain_oil">机油</h3>

<h4 id="maintain_oil_list_get">查询机油列表信息</h4>

url:/api/maintain/oil/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|garage_id|int|汽修厂id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|L|int|升|无|  
|price|float|原价|无|  
|new_price|float|特价|无|  
|pic_url|char(50)|封面url|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'没油',
        'L':2,
        'price':1,
        'new_price':1,
        'pic_url':'asdla.jpg'
    }]
}
```

<h4 id="maintain_oil_get">查询机油信息</h4>

url:/api/maintain/oil/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|L|int|升|无|  
|price|float|原价|无|  
|new_price|float|特价|无|  
|pic_url|char(50)|封面url|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'没油',
        'L':2,
        'price':1,
        'new_price':1,
        'pic_url':'asdla.jpg'
    }]
}
```

<h3 id="maintain_upkeep">保养</h3>

<h4 id="maintain_upkeep_list_get">查询保养列表信息</h4>

url:/api/maintain/upkeep/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|phone|char(20)|电话号码|无|  
|longitude|float|经度|无|104|  
|latitude|float|纬度|无|23|  
|address|char(100)|地址|无|广州天河区|  
|subscribe_time|datetime|预约时间|无|  
|filter_price|float|过滤格|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:未支付，1:等待服务，2:服务中，3:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|pay_time|datetime|付款时间|无|  
|service_time|datetime|服务时间|无|  
|comment_time|datetime|评论时间|无|  
|over_time|datetime|完成时间|无|   
|service_item|char(100)|服务项目|无|  
|service_materials|text|服务材料|无|  
|deal_id|char(100)|交易单号|无|  
|order_id|char(100)|订单单号|无|  
|oil_name|char(50)|机油名称|无|  
|oil_L|int|升|无|  
|oil_price|float|原价|无|  
|oil_new_price|float|特价|无|  
|car_brand|char(100)|车辆品牌|无|玛萨拉蒂|  
|car_code|char(10)|车牌号码|无|粤A24351|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'garage':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'1',
            'user_name':'1',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'mobile_phone':'12345678998',
            'phone':'020-8888888',
            'oil_block':70,
            'work_price':88
        },
        'name':'张三',
        'phone':'12345678998',
        'longitude':123,
        'latitude':23,
        'address':'广州市越秀区',
        'subscribe_time':'2018-07-08 12:23:34',
        'filter_price':1,
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'service_item':'装轮胎',
        'service_materials':'轮胎',
        'deal_id':'182731725',
        'order_id':'8927918238271',
        'oil_name':'没油',
        'oil_L':2,
        'oil_price':1,
        'oil_new_price':1,
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A24351'
    }]
}
```

<h4 id="maintain_upkeep_list_post">生成保养订单信息</h4>

url:/api/maintain/upkeep/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|garage_id|int|汽修厂id|无|1|  
|car_id|int|汽车id|无|1|  
|name|char(20)|联系人|无|张三|  
|phone|char(20)|电话号码|无|12345678909|  
|subscribe_time|datetime|预约时间|无|2018-07-08 12:23:34|  
|longitude|float|经度|无|1|  
|latitude|float|纬度|无|1|  
|address|char(100)|地址|无|广州市越秀区|  
|oil_id|int|机油id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h4 id="maintain_upkeep_get">查询保养信息</h4>

url:/api/maintain/upkeep/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|phone|char(20)|电话号码|无|  
|longitude|float|经度|无|104|  
|latitude|float|纬度|无|23|  
|address|char(100)|地址|无|广州天河区|  
|subscribe_time|datetime|预约时间|无|  
|filter_price|float|过滤格|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:未支付，1:等待服务，2:服务中，3:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|pay_time|datetime|付款时间|无|  
|service_time|datetime|服务时间|无|  
|comment_time|datetime|评论时间|无|  
|over_time|datetime|完成时间|无|   
|service_item|char(100)|服务项目|无|  
|service_materials|text|服务材料|无|  
|deal_id|char(100)|交易单号|无|  
|order_id|char(100)|订单单号|无|  
|oil_name|char(50)|机油名称|无|  
|oil_L|int|升|无|  
|oil_price|float|原价|无|  
|oil_new_price|float|特价|无|  
|car_brand|char(100)|车辆品牌|无|玛萨拉蒂|  
|car_code|char(10)|车牌号码|无|粤A24351|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'garage':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'1',
            'user_name':'1',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'mobile_phone':'12345678998',
            'phone':'020-8888888',
            'oil_block':70,
            'work_price':88
        },
        'name':'张三',
        'phone':'12345678998',
        'longitude':123,
        'latitude':23,
        'address':'广州市越秀区',
        'subscribe_time':'2018-07-08 12:23:34',
        'filter_price':1,
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'service_item':'装轮胎',
        'service_materials':'轮胎',
        'deal_id':'182731725',
        'order_id':'8927918238271',
        'oil_name':'没油',
        'oil_L':2,
        'oil_price':1,
        'oil_new_price':1,
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A24351'
    }
}
```

<h4 id="maintain_upkeep_delete">删除保养订单信息</h4>

url:/api/maintain/upkeep/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="maintain_upkeep_method_post">付款、评论保养订单信息</h4>

url:/api/maintain/upkeep_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
|method|char(20)|操作|pay:付款，comment:评论|comment|  
|score|int|评分|大于等于0，小于等于5，当method为comment的时候需要|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="maintain_maintain">维修</h3>

<h4 id="maintain_maintain_list_get">查询维修列表信息</h4>

url:/api/maintain/maintain/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|phone|char(20)|电话号码|无|  
|longitude|float|经度|无|104|  
|latitude|float|纬度|无|23|  
|address|char(100)|地址|无|广州天河区|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|pic_url_list|list|图片列表|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:未支付，1:等待服务，2:服务中，3:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|pay_time|datetime|付款时间|无|  
|service_time|datetime|服务时间|无|  
|comment_time|datetime|评论时间|无|  
|over_time|datetime|完成时间|无|  
|car_code|char(10)|车牌|无|  
|car_type|char(100)|车型|无|  
|service_item|char(100)|服务项目|无|  
|service_materials|text|服务材料|无|  
|deal_id|char(10)|交易单号|无|  
|order_id|char(10)|订单单号|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'garage':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'1',
            'user_name':'1',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'mobile_phone':'12345678998',
            'phone':'020-8888888',
            'oil_block':70,
            'work_price':88
        },
        'name':'张三',
        'phone':'粤A23452',
        'longitude':'玛萨拉蒂',
        'latitude':'广州市越秀区',
        'address':'12345678998',
        'car_type':'12345678998',
        'subscribe_time':'2018-07-08 12:23:34',
        'content':'修理',
        'pic_url_list':['/asda.jpg'],
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'car_code':'粤A88888',
        'service_item':'装轮胎',
        'service_materials':'轮胎',
        'deal_id':'182731725',
        'order_id':'8927918238271'
    }]
}
```

<h4 id="maintain_maintain_list_post">生成维修订单信息</h4>

url:/api/maintain/maintain/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|garage_id|int|汽修厂id|无|1|  
|name|char(20)|名称|无|张三|  
|phone|char(20)|电话号码|无|12345678998|  
|longitude|float|经度|无|104|  
|latitude|float|纬度|无|23|  
|address|char(100)|地址|无|广州天河区|  
|subscribe_time|datetime|预约时间|无|2018-07-08 12:23:34|  
|content|text|内容|无|修理|  
|number|int|数量|多少个文件|1|  
|pic1|文件流|图片|编号从1开始|(文件流)|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h4 id="maintain_maintain_get">查询维修信息</h4>

url:/api/maintain/maintain/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|phone|char(20)|电话号码|无|  
|longitude|float|经度|无|104|  
|latitude|float|纬度|无|23|  
|address|char(100)|地址|无|广州天河区|  
|car_type|char(100)|车型|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|pic_url_list|list|图片列表|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:未支付，1:等待服务，2:服务中，3:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|pay_time|datetime|付款时间|无|  
|service_time|datetime|服务时间|无|  
|comment_time|datetime|评论时间|无|  
|over_time|datetime|完成时间|无|  
|car_code|char(10)|车牌|无|  
|service_item|char(100)|服务项目|无|  
|service_materials|text|服务材料|无|  
|deal_id|char(10)|交易单号|无|  
|order_id|char(10)|订单单号|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'garage':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'1',
            'user_name':'1',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'mobile_phone':'12345678998',
            'phone':'020-8888888',
            'oil_block':70,
            'work_price':88
        },
        'name':'张三',
        'phone':'粤A23452',
        'longitude':'玛萨拉蒂',
        'latitude':'广州市越秀区',
        'address':'12345678998',
        'car_type':'12345678998',
        'subscribe_time':'2018-07-08 12:23:34',
        'content':'修理',
        'pic_url_list':['/asda.jpg'],
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'car_code':'粤A88888',
        'service_item':'装轮胎',
        'service_materials':'轮胎',
        'deal_id':'182731725',
        'order_id':'8927918238271'
    }
}
```

<h4 id="maintain_maintain_delete">删除维修订单信息</h4>

url:/api/maintain/maintain_delete/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="maintain_maintain_method_post">付款、评论维修订单信息</h4>

url:/api/maintain/maintain_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   
|method|char(20)|操作|pay:付款，comment:评论|comment|  
|score|int|评分|大于等于0，小于等于5，当method微comment的时候需要|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h2 id="survey">年检</h2>

<h3 id="survey_surveystation">年检站信息</h3>

<h4 id="survey_surveystation_list_get">查询年检站列表信息</h4>

url:/api/survey/surveystation/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
|price|float|价格|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三年检站',
        'longitude':223,
        'latitude':322,
        'address':'广州越秀区',
        'price':1
    }]
}
```

<h4 id="service_surveystation_get">查询年检站信息</h4>

url:/api/survey/surveystation/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
|price|float|价格|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三年检站',
        'longitude':223,
        'latitude':322,
        'address':'广州越秀区',
        'price':1
    }
}
```

<h3 id="survey_combo">套餐信息</h3>

<h4 id="survey_combo_list_get">查询套餐列表信息</h4>

url:/api/survey/combo/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|detail|char(100)|套餐详情|无|  
|comboitem_set|list|套餐内容|无|

comboitem_set:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|名称|无|  
|price|float|价格|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'a套餐',
        'detail':'不要钱',
        'comboitem_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'price':200
        }]
    }]
}
```

<h4 id="survey_combo_get">查询套餐信息</h4>

url:/api/survey/combo/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|detail|char(100)|套餐详情|无|  
|comboitem_set|list|套餐内容|无|  

comboitem_set:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|名称|无|  
|price|float|价格|无|  

```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'a套餐',
        'detail':'不要钱',
        'comboitem_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'price':200
        }]
    }
}
```

<h3 id="survey_survey">年检订单信息</h3>

<h4 id="survey_survey_list_get">查询年检订单列表信息</h4>

url:/api/survey/survey/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|  

'''
代驾取车：0:已发布，1:已接单，2:已取车
开始年检：3.到达年检，4.年检结束，5.等待支付，
检完还车：6.到达还车，7.已还车，8.已完成
代驾：0-1-2-3-4-5-6-7-8
自驾：3-5-8
'''

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:小型蓝牌，1：七座以下|  
|surveystation|object|年检站|查询年检站信息|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|order_address|char(100)|交接地点|无|  
|subscribe_time|datetime|预约日期|无|  
|is_self|bool|是否自驾|无|  
|combo|object|套餐对象|查看套餐接口|  
|surveycomboitem_set|list|套餐项列表|查看套餐接口|  
|base_price|float|基础费用|无|  
|combo_price|float|套餐费用|无|  
|survey_price|float|年检费用|无|  
|total_price|float|总计费用|无|  
|state|int|状态|0:已发布，1:已接单，2:已取车，3.到达年检，4.年检结束，5.等待支付，6.到达还车，7.已还车，8.已完成，9.已取消|  
|is_success|bool|年检是否成功|无|  
|drive_user_id|int|接单用户id|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|pic_get_confirm1_url|char(50)|取车图片-检车确认1照片url|/url,获取图片|  
|pic_get_confirm2_url|char(50)|取车图片-检车确认2照片url|/url,获取图片|  
|pic_get_car1_url|char(50)|取车图片-车身拍照1照片url|/url,获取图片|  
|pic_get_car2_url|char(50)|取车图片-车身拍照2照片url|/url,获取图片|  
|pic_get_car3_url|char(50)|取车图片-车身拍照3照片url|/url,获取图片|  
|pic_get_car4_url|char(50)|取车图片-车身拍照4照片url|/url,获取图片|  
|pic_get_car5_url|char(50)|取车图片-车身拍照5照片url|/url,获取图片|  
|pic_get_car6_url|char(50)|取车图片-车身拍照6照片url|/url,获取图片|  
|pic_survey_upload1_url|char(50)|年检已过-上传照片1照片url|/url,获取图片|  
|pic_survey_upload2_url|char(50)|年检已过-上传照片2照片url|/url,获取图片|  
|pic_survey_lamp1_url|char(50)|年检未过-车灯照片1照片url|/url,获取图片|  
|pic_survey_lamp2_url|char(50)|年检未过-车灯照片2照片url|/url,获取图片|  
|pic_survey_exhaust1_url|char(50)|年检未过-排气照片1照片url|/url,获取图片|  
|pic_survey_exhaust2_url|char(50)|年检未过-排气照片2照片url|/url,获取图片|  
|pic_survey_appearance1_url|char(50)|年检未过-外观照片1照片url|/url,获取图片|  
|pic_survey_appearance2_url|char(50)|年检未过-外观照片2照片url|/url,获取图片|  
|pic_return_confirm1_url|char(50)|还车图片-检车确认1照片url|/url,获取图片|  
|pic_greturn_confirm2_url|char(50)|还车图片-检车确认2照片url|/url,获取图片|  
|pic_return_car1_url|char(50)|还车图片-车身拍照1照片url|/url,获取图片|  
|pic_return_car2_url|char(50)|还车图片-车身拍照2照片url|/url,获取图片|  
|pic_return_car3_url|char(50)|还车图片-车身拍照3照片url|/url,获取图片|  
|pic_return_car4_url|char(50)|还车图片-车身拍照4照片url|/url,获取图片|  
|pic_return_car5_url|char(50)|还车图片-车身拍照5照片url|/url,获取图片|  
|pic_return_car6_url|char(50)|还车图片-车身拍照6照片url|/url,获取图片|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':1,
        'surveystation':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'张三年检站',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'price':1
        },
        'order_longitude':23,
        'order_latitude':123,
        'order_address':'广州白云区',
        'subscribe_time':'2018-07-08 12:23:34',
        'is_self':true,
        'combo':{

        },
        'surveycomboitem_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'price':200
        }],
        'base_price':1,
        'combo_price':1,
        'survey_price':1,
        'total_price':1,
        'state':1,
        'is_success':true,
        'drive_user_id':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'pic_get_confirm1_url':'/aklsdjalk.jpg',
        'pic_get_confirm2_url':'/aklsdjalk.jpg',
        'pic_get_car1_url':'/aklsdjalk.jpg',
        'pic_get_car2_url':'/aklsdjalk.jpg',
        'pic_get_car3_url':'/aklsdjalk.jpg',
        'pic_get_car4_url':'/aklsdjalk.jpg',
        'pic_get_car5_url':'/aklsdjalk.jpg',
        'pic_get_car6_url':'/aklsdjalk.jpg',
        'pic_survey_upload1_url':'/aklsdjalk.jpg',
        'pic_survey_upload2_url':'/aklsdjalk.jpg',
        'pic_survey_lamp1_url':'/aklsdjalk.jpg',
        'pic_survey_lamp2_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust1_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust2_url':'/aklsdjalk.jpg',
        'pic_survey_appearance1_url':'/aklsdjalk.jpg',
        'pic_survey_appearance2_url':'/aklsdjalk.jpg',
        'pic_return_confirm2_url':'/aklsdjalk.jpg',
        'pic_greturn_confirm2_url':'/aklsdjalk.jpg',
        'pic_return_car1_url':'/aklsdjalk.jpg',
        'pic_return_car2_url':'/aklsdjalk.jpg',
        'pic_return_car3_url':'/aklsdjalk.jpg',
        'pic_return_car4_url':'/aklsdjalk.jpg',
        'pic_return_car5_url':'/aklsdjalk.jpg',
        'pic_return_car6_url':'/aklsdjalk.jpg',
    }]
}
```

<h4 id="survey_survey_list_post">提交年检订单信息</h4>

url:/api/survey/survey/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|name|char(20)|联系人|无|张三|  
|phone|char(20)|联系人电话|无|12345678998|  
|car_name|char(20)|车主姓名|无|张三|  
|car_brand|char(20)|品牌型号|无|玛萨拉蒂|  
|car_code|char(20)|车牌|无|粤A23452|  
|car_type|int|车量类型|0:小型蓝牌，1：七座以下|  
|surveystation_id|int|年检站id|无|1|  
|order_longitude|float|交接地点经度|无|233|  
|order_latitude|float|交接地点纬度|无|322|  
|order_address|char(100)|交接地点|无|广州白云区|  
|subscribe_time|datetime|预约日期|13点前表示上午，13点后表示下午|2018-07-08 12:23:34|  
|is_self|bool|是否自驾|无|false|  
|combo_id|int|套餐id|无|1|  
|comboitem_list|char(100)|套餐选项id|使用,拼接|1,2|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h4 id="survey_survey_get">查询年检订单信息</h4>

url:/api/survey/survey/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:小型蓝牌，1：七座以下|  
|surveystation|object|年检站|查询年检站信息|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|order_address|char(100)|交接地点|无|  
|subscribe_time|datetime|预约日期|无|  
|is_self|bool|是否自驾|无|  
|combo|object|套餐对象|查看套餐接口|  
|surveycomboitem_set|list|套餐项列表|查看套餐接口|  
|base_price|float|基础费用|无|  
|combo_price|float|套餐费用|无|  
|survey_price|float|年检费用|无|  
|total_price|float|总计费用|无|  
|state|int|状态|0:已发布，1:已接单，2:已取车，3.到达年检，4.年检结束，5.等待支付，6.到达还车，7.已还车，8.已完成，9.已取消|  
|is_success|bool|年检是否成功|无|  
|drive_user_id|int|接单用户id|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|pic_get_confirm1_url|char(50)|取车图片-检车确认1照片url|/url,获取图片|  
|pic_get_confirm2_url|char(50)|取车图片-检车确认2照片url|/url,获取图片|  
|pic_get_car1_url|char(50)|取车图片-车身拍照1照片url|/url,获取图片|  
|pic_get_car2_url|char(50)|取车图片-车身拍照2照片url|/url,获取图片|  
|pic_get_car3_url|char(50)|取车图片-车身拍照3照片url|/url,获取图片|  
|pic_get_car4_url|char(50)|取车图片-车身拍照4照片url|/url,获取图片|  
|pic_get_car5_url|char(50)|取车图片-车身拍照5照片url|/url,获取图片|  
|pic_get_car6_url|char(50)|取车图片-车身拍照6照片url|/url,获取图片|  
|pic_survey_upload1_url|char(50)|年检已过-上传照片1照片url|/url,获取图片|  
|pic_survey_upload2_url|char(50)|年检已过-上传照片2照片url|/url,获取图片|  
|pic_survey_lamp1_url|char(50)|年检未过-车灯照片1照片url|/url,获取图片|  
|pic_survey_lamp2_url|char(50)|年检未过-车灯照片2照片url|/url,获取图片|  
|pic_survey_exhaust1_url|char(50)|年检未过-排气照片1照片url|/url,获取图片|  
|pic_survey_exhaust2_url|char(50)|年检未过-排气照片2照片url|/url,获取图片|  
|pic_survey_appearance1_url|char(50)|年检未过-外观照片1照片url|/url,获取图片|  
|pic_survey_appearance2_url|char(50)|年检未过-外观照片2照片url|/url,获取图片|  
|pic_return_confirm2_url|char(50)|还车图片-检车确认1照片url|/url,获取图片|  
|pic_greturn_confirm2_url|char(50)|还车图片-检车确认2照片url|/url,获取图片|  
|pic_return_car1_url|char(50)|还车图片-车身拍照1照片url|/url,获取图片|  
|pic_return_car2_url|char(50)|还车图片-车身拍照2照片url|/url,获取图片|  
|pic_return_car3_url|char(50)|还车图片-车身拍照3照片url|/url,获取图片|  
|pic_return_car4_url|char(50)|还车图片-车身拍照4照片url|/url,获取图片|  
|pic_return_car5_url|char(50)|还车图片-车身拍照5照片url|/url,获取图片|  
|pic_return_car6_url|char(50)|还车图片-车身拍照6照片url|/url,获取图片|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':1,
        'surveystation':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'张三年检站',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'price':1
        },
        'order_longitude':23,
        'order_latitude':123,
        'order_address':'广州白云区',
        'subscribe_time':'2018-07-08 12:23:34',
        'is_self':true,
        'combo':{

        },
        'surveycomboitem_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'price':200
        }],
        'base_price':1,
        'combo_price':1,
        'survey_price':1,
        'total_price':1,
        'state':1,
        'is_success':true,
        'drive_user_id':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'pic_get_confirm1_url':'/aklsdjalk.jpg',
        'pic_get_confirm2_url':'/aklsdjalk.jpg',
        'pic_get_car1_url':'/aklsdjalk.jpg',
        'pic_get_car2_url':'/aklsdjalk.jpg',
        'pic_get_car3_url':'/aklsdjalk.jpg',
        'pic_get_car4_url':'/aklsdjalk.jpg',
        'pic_get_car5_url':'/aklsdjalk.jpg',
        'pic_get_car6_url':'/aklsdjalk.jpg',
        'pic_survey_upload1_url':'/aklsdjalk.jpg',
        'pic_survey_upload2_url':'/aklsdjalk.jpg',
        'pic_survey_lamp1_url':'/aklsdjalk.jpg',
        'pic_survey_lamp2_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust1_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust2_url':'/aklsdjalk.jpg',
        'pic_survey_appearance1_url':'/aklsdjalk.jpg',
        'pic_survey_appearance2_url':'/aklsdjalk.jpg',
        'pic_return_confirm2_url':'/aklsdjalk.jpg',
        'pic_greturn_confirm2_url':'/aklsdjalk.jpg',
        'pic_return_car1_url':'/aklsdjalk.jpg',
        'pic_return_car2_url':'/aklsdjalk.jpg',
        'pic_return_car3_url':'/aklsdjalk.jpg',
        'pic_return_car4_url':'/aklsdjalk.jpg',
        'pic_return_car5_url':'/aklsdjalk.jpg',
        'pic_return_car6_url':'/aklsdjalk.jpg',
    }
}
```

<h4 id="survey_survey_delete">删除年检订单信息</h4>

url:/api/survey/survey_delete/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="survey_survey_method_post">年检订单操作信息-查询费用、支付、确认还车、自驾完成</h4>

url:/api/survey/survey_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|查询费用不需要添加id|1|   
|method|char(20)|操作|get:查询费用，pay:支付（自驾代驾），return:确认还车（代驾），survey：到达年检（自驾）|get|  
|longitude|float|经度|无|123|  
|latitude|float|纬度|无|23|  
|surveystation_id|int|年检站id|无|1|  
|combo_id|int|套餐id|无|1|  
|comboitem_list|char(100)|套餐选项id|使用,拼接|1,2|  

return:  

```
如果是查询费用，data里面才会有结构返回
1.参数中有年检站参数，会计算年检费用
2.存在年检站参数、经纬度、套餐id，会计算基础费用
3.存在套餐id、套餐项id列表，会计算套餐费用
```

|参数|类型|说明|备注|  
|---|---|---|---|  
|base_price|float|基础费用|无|  
|combo_price|float|套餐费用|无|  
|survey_price|float|年检费用|无|  
|total_price|float|总计费用|无|  
```
{
    'data':{
        'base_price':1,
        'combo_price':1
        'survey_price':1
        'combo_price':1
    }
}
```

<h2 id="system">系统</h2>

<h3 id="system_serviceimg_get">服务首页图片信息</h3>

url:/api/system/serviceimg/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|pic_url_list|char(100)|轮播图片列表|无|  

```
{
    'data':{
        'pic_url':'/asd.hpg',
        'pic_url_list':['/asd.hpg']
    }
}
```

<h3 id="survey_img_get">年检首页图片信息</h3>

url:/api/system/surveyimg/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|pic_url_list|char(100)|轮播图片列表|无|  

```
{
    'data':{
        'pic_url':'/asd.hpg',
        'pic_url_list':['/asd.hpg']
    }
}
```

<h2 id="driver">司机端</h2>

<h3 id="driver_order">订单</h3>

<h4 id="driver_order_list_get">查询订单列表信息</h4>

url:/api/driver/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|type|char(100)|类型|order：可以接的单，driver：已接订单|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:小型蓝牌，1：七座以下|  
|surveystation|object|年检站|查询年检站信息|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|order_address|char(100)|交接地点|无|  
|subscribe_time|datetime|预约日期|无|  
|is_self|bool|是否自驾|无|  
|combo|object|套餐对象|查看套餐接口|  
|surveycomboitem_set|list|套餐项列表|查看套餐接口|  
|base_price|float|基础费用|无|  
|combo_price|float|套餐费用|无|  
|survey_price|float|年检费用|无|  
|total_price|float|总计费用|无|  
|state|int|状态|0:已发布，1:已接单，2:已取车，3.到达年检，4.年检结束，5.到达还车，6.已还车，7.已完成，8.已取消|  
|is_success|bool|年检是否成功|无|  
|drive_user_id|int|接单用户id|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|pic_get_confirm1_url|char(50)|取车图片-检车确认1照片url|/url,获取图片|  
|pic_get_confirm2_url|char(50)|取车图片-检车确认2照片url|/url,获取图片|  
|pic_get_car1_url|char(50)|取车图片-车身拍照1照片url|/url,获取图片|  
|pic_get_car2_url|char(50)|取车图片-车身拍照2照片url|/url,获取图片|  
|pic_get_car3_url|char(50)|取车图片-车身拍照3照片url|/url,获取图片|  
|pic_get_car4_url|char(50)|取车图片-车身拍照4照片url|/url,获取图片|  
|pic_get_car5_url|char(50)|取车图片-车身拍照5照片url|/url,获取图片|  
|pic_get_car6_url|char(50)|取车图片-车身拍照6照片url|/url,获取图片|  
|pic_survey_upload1_url|char(50)|年检已过-上传照片1照片url|/url,获取图片|  
|pic_survey_upload2_url|char(50)|年检已过-上传照片2照片url|/url,获取图片|  
|pic_survey_lamp1_url|char(50)|年检未过-车灯照片1照片url|/url,获取图片|  
|pic_survey_lamp2_url|char(50)|年检未过-车灯照片2照片url|/url,获取图片|  
|pic_survey_exhaust1_url|char(50)|年检未过-排气照片1照片url|/url,获取图片|  
|pic_survey_exhaust2_url|char(50)|年检未过-排气照片2照片url|/url,获取图片|  
|pic_survey_appearance1_url|char(50)|年检未过-外观照片1照片url|/url,获取图片|  
|pic_survey_appearance2_url|char(50)|年检未过-外观照片2照片url|/url,获取图片|  
|pic_return_confirm2_url|char(50)|还车图片-检车确认1照片url|/url,获取图片|  
|pic_greturn_confirm2_url|char(50)|还车图片-检车确认2照片url|/url,获取图片|  
|pic_return_car1_url|char(50)|还车图片-车身拍照1照片url|/url,获取图片|  
|pic_return_car2_url|char(50)|还车图片-车身拍照2照片url|/url,获取图片|  
|pic_return_car3_url|char(50)|还车图片-车身拍照3照片url|/url,获取图片|  
|pic_return_car4_url|char(50)|还车图片-车身拍照4照片url|/url,获取图片|  
|pic_return_car5_url|char(50)|还车图片-车身拍照5照片url|/url,获取图片|  
|pic_return_car6_url|char(50)|还车图片-车身拍照6照片url|/url,获取图片|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':1,
        'surveystation':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'张三年检站',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'price':1
        },
        'order_longitude':23,
        'order_latitude':123,
        'order_address':'广州白云区',
        'subscribe_time':'2018-07-08 12:23:34',
        'is_self':true,
        'combo':{

        },
        'surveycomboitem_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'price':200
        }],
        'base_price':1,
        'combo_price':1,
        'survey_price':1,
        'total_price':1,
        'state':1,
        'is_success':true,
        'drive_user_id':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'pic_get_confirm1_url':'/aklsdjalk.jpg',
        'pic_get_confirm2_url':'/aklsdjalk.jpg',
        'pic_get_car1_url':'/aklsdjalk.jpg',
        'pic_get_car2_url':'/aklsdjalk.jpg',
        'pic_get_car3_url':'/aklsdjalk.jpg',
        'pic_get_car4_url':'/aklsdjalk.jpg',
        'pic_get_car5_url':'/aklsdjalk.jpg',
        'pic_get_car6_url':'/aklsdjalk.jpg',
        'pic_survey_upload1_url':'/aklsdjalk.jpg',
        'pic_survey_upload2_url':'/aklsdjalk.jpg',
        'pic_survey_lamp1_url':'/aklsdjalk.jpg',
        'pic_survey_lamp2_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust1_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust2_url':'/aklsdjalk.jpg',
        'pic_survey_appearance1_url':'/aklsdjalk.jpg',
        'pic_survey_appearance2_url':'/aklsdjalk.jpg',
        'pic_return_confirm2_url':'/aklsdjalk.jpg',
        'pic_greturn_confirm2_url':'/aklsdjalk.jpg',
        'pic_return_car1_url':'/aklsdjalk.jpg',
        'pic_return_car2_url':'/aklsdjalk.jpg',
        'pic_return_car3_url':'/aklsdjalk.jpg',
        'pic_return_car4_url':'/aklsdjalk.jpg',
        'pic_return_car5_url':'/aklsdjalk.jpg',
        'pic_return_car6_url':'/aklsdjalk.jpg',
    }]
}
```

<h4 id="driver_order_get">查询订单信息</h4>

url:/api/driver/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:小型蓝牌，1：七座以下|  
|surveystation|object|年检站|查询年检站信息|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|order_address|char(100)|交接地点|无|  
|subscribe_time|datetime|预约日期|无|  
|is_self|bool|是否自驾|无|  
|combo|object|套餐对象|查看套餐接口|  
|surveycomboitem_set|list|套餐项列表|查看套餐接口|  
|base_price|float|基础费用|无|  
|combo_price|float|套餐费用|无|  
|survey_price|float|年检费用|无|  
|total_price|float|总计费用|无|  
|state|int|状态|0:已发布，1:已接单，2:已取车，3.到达年检，4.年检结束，5.到达还车，6.已还车，7.已完成，8.已取消|  
|is_success|bool|年检是否成功|无|  
|drive_user_id|int|接单用户id|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|pic_get_confirm1_url|char(50)|取车图片-检车确认1照片url|/url,获取图片|  
|pic_get_confirm2_url|char(50)|取车图片-检车确认2照片url|/url,获取图片|  
|pic_get_car1_url|char(50)|取车图片-车身拍照1照片url|/url,获取图片|  
|pic_get_car2_url|char(50)|取车图片-车身拍照2照片url|/url,获取图片|  
|pic_get_car3_url|char(50)|取车图片-车身拍照3照片url|/url,获取图片|  
|pic_get_car4_url|char(50)|取车图片-车身拍照4照片url|/url,获取图片|  
|pic_get_car5_url|char(50)|取车图片-车身拍照5照片url|/url,获取图片|  
|pic_get_car6_url|char(50)|取车图片-车身拍照6照片url|/url,获取图片|  
|pic_survey_upload1_url|char(50)|年检已过-上传照片1照片url|/url,获取图片|  
|pic_survey_upload2_url|char(50)|年检已过-上传照片2照片url|/url,获取图片|  
|pic_survey_lamp1_url|char(50)|年检未过-车灯照片1照片url|/url,获取图片|  
|pic_survey_lamp2_url|char(50)|年检未过-车灯照片2照片url|/url,获取图片|  
|pic_survey_exhaust1_url|char(50)|年检未过-排气照片1照片url|/url,获取图片|  
|pic_survey_exhaust2_url|char(50)|年检未过-排气照片2照片url|/url,获取图片|  
|pic_survey_appearance1_url|char(50)|年检未过-外观照片1照片url|/url,获取图片|  
|pic_survey_appearance2_url|char(50)|年检未过-外观照片2照片url|/url,获取图片|  
|pic_return_confirm2_url|char(50)|还车图片-检车确认1照片url|/url,获取图片|  
|pic_greturn_confirm2_url|char(50)|还车图片-检车确认2照片url|/url,获取图片|  
|pic_return_car1_url|char(50)|还车图片-车身拍照1照片url|/url,获取图片|  
|pic_return_car2_url|char(50)|还车图片-车身拍照2照片url|/url,获取图片|  
|pic_return_car3_url|char(50)|还车图片-车身拍照3照片url|/url,获取图片|  
|pic_return_car4_url|char(50)|还车图片-车身拍照4照片url|/url,获取图片|  
|pic_return_car5_url|char(50)|还车图片-车身拍照5照片url|/url,获取图片|  
|pic_return_car6_url|char(50)|还车图片-车身拍照6照片url|/url,获取图片|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':1,
        'surveystation':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'张三年检站',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区',
            'price':1
        },
        'order_longitude':23,
        'order_latitude':123,
        'order_address':'广州白云区',
        'subscribe_time':'2018-07-08 12:23:34',
        'is_self':true,
        'combo':{

        },
        'surveycomboitem_set':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'轮胎',
            'price':200
        }],
        'base_price':1,
        'combo_price':1,
        'survey_price':1,
        'total_price':1,
        'state':1,
        'is_success':true,
        'drive_user_id':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'pic_get_confirm1_url':'/aklsdjalk.jpg',
        'pic_get_confirm2_url':'/aklsdjalk.jpg',
        'pic_get_car1_url':'/aklsdjalk.jpg',
        'pic_get_car2_url':'/aklsdjalk.jpg',
        'pic_get_car3_url':'/aklsdjalk.jpg',
        'pic_get_car4_url':'/aklsdjalk.jpg',
        'pic_get_car5_url':'/aklsdjalk.jpg',
        'pic_get_car6_url':'/aklsdjalk.jpg',
        'pic_survey_upload1_url':'/aklsdjalk.jpg',
        'pic_survey_upload2_url':'/aklsdjalk.jpg',
        'pic_survey_lamp1_url':'/aklsdjalk.jpg',
        'pic_survey_lamp2_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust1_url':'/aklsdjalk.jpg',
        'pic_survey_exhaust2_url':'/aklsdjalk.jpg',
        'pic_survey_appearance1_url':'/aklsdjalk.jpg',
        'pic_survey_appearance2_url':'/aklsdjalk.jpg',
        'pic_return_confirm2_url':'/aklsdjalk.jpg',
        'pic_greturn_confirm2_url':'/aklsdjalk.jpg',
        'pic_return_car1_url':'/aklsdjalk.jpg',
        'pic_return_car2_url':'/aklsdjalk.jpg',
        'pic_return_car3_url':'/aklsdjalk.jpg',
        'pic_return_car4_url':'/aklsdjalk.jpg',
        'pic_return_car5_url':'/aklsdjalk.jpg',
        'pic_return_car6_url':'/aklsdjalk.jpg',
    }
}
```

<h4 id="driver_order_grab_post">抢单</h4>

url:/api/driver/order_grab/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_wait_post">听单</h4>
<h4 id="driver_order_cancel_post">取消订单</h4>

url:/api/driver/order_cancel/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_get_post">确认取车</h4>

url:/api/driver/order_get/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  
|pic_get_confirm1|文件流|取车图片-检车确认1照片|无|(文件流，base64)|  
|pic_get_confirm2|文件流|取车图片-检车确认2照片|无|(文件流，base64)|  
|pic_get_car1|文件流|取车图片-车身拍照1照片|无|(文件流，base64)|  
|pic_get_car2|文件流)|取车图片-车身拍照2照片|无|(文件流，base64)|  
|pic_get_car3|文件流|取车图片-车身拍照3照片|无|(文件流，base64)|  
|pic_get_car4|文件流|取车图片-车身拍照4照片|无|(文件流，base64)|  
|pic_get_car5|文件流|取车图片-车身拍照5照片|无|(文件流，base64)|  
|pic_get_car6|文件流|取车图片-车身拍照6照片|无|(文件流，base64)|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_survey_post">开始年检</h4>

url:/api/driver/order_survey/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_success_post">年检已过</h4>

url:/api/driver/order_success/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  
|pic_survey_upload1|文件流|年检已过-上传照片1照片|无|(文件流，base64)|  
|pic_survey_upload2|文件流|年检已过-上传照片2照片|无|(文件流，base64)|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_fail_post">年检未过</h4>

url:/api/driver/order_fail/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  
|pic_survey_lamp1|文件流|年检未过-车灯照片1照片|无|(文件流，base64)|  
|pic_survey_lamp2|文件流|年检未过-车灯照片2照片|无|(文件流，base64)|  
|pic_survey_exhaust1|文件流|年检未过-排气照片2照片|无|(文件流，base64)|  
|pic_survey_exhaust2|文件流|年检未过-排气照片2照片|无|(文件流，base64)|  
|pic_survey_appearance1|文件流|年检未过-外观照片2照片|无|(文件流，base64)|  
|pic_survey_appearance2|文件流|年检未过-外观照片2照片|无|(文件流，base64)|  


return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_return_post">确认换车</h4>

url:/api/driver/order_return/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  
|pic_return_confirm2|文件流|还车图片-检车确认1照片|无|(文件流，base64)|  
|pic_greturn_confirm2|文件流|还车图片-检车确认2照片|无|(文件流，base64)|  
|pic_return_car1|文件流|还车图片-车身拍照1照片|无|(文件流，base64)|  
|pic_return_car2|文件流|还车图片-车身拍照2照片|无|(文件流，base64)|  
|pic_return_car3|文件流|还车图片-车身拍照3照片|无|(文件流，base64)|  
|pic_return_car4|文件流|还车图片-车身拍照4照片|无|(文件流，base64)|  
|pic_return_car5|文件流|还车图片-车身拍照5照片|无|(文件流，base64)|  
|pic_return_car6|文件流|还车图片-车身拍照6照片|无|(文件流，base64)|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```


<h3 id="driver_account">账户</h3>

<h4 id="driver_account_list_get">查询明细列表信息</h4>

url:/api/driver/account/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_time|datetime|时间|无|  
|start_address|char(100)|出发地点|无|  
|end_address|char(100)|到达地点|无|  
|method|char(100)|行为|0：提现，1：收入|  
|via|char(100)|提现途径|alipay,weixin|  
|cost|float|费用|无|  
|survey|objects|年检订单|查看年检信息,如果是提现的话，这里为空|

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_time':'2018-07-08 12:23:34',
        'start_address':'广州白玉区',
        'end_address':'广州天河区',
        'method':1,
        'via':'',
        'cost':123,
        'survey':{}
    }]
}
```

<h4 id="driver_account_get">查询明细信息</h4>

url:/api/driver/account/  
method:get  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_time|datetime|时间|无|  
|start_address|char(100)|出发地点|无|  
|end_address|char(100)|到达地点|无|  
|method|char(100)|行为|0：提现，1：收入|  
|via|char(100)|提现途径|alipay,weixin|  
|cost|float|费用|无|  
|survey|objects|年检订单|查看年检信息,如果是提现的话，这里为空|  

```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_time':'2018-07-08 12:23:34',
        'start_address':'广州白玉区',
        'end_address':'广州天河区',
        'method':1,
        'via':'',
        'cost':123,
        'survey':{}
    }
}
```

<h4 id="driver_account_method_post">明细操作信息-提现</h4>

url:/api/driver/account/  
method:post  
param:   

|参数|类型|说明|备注|例子|  
|---|---|---|---|---|  
|id|int|id|无|1|  
|money|float|提现金额|无|1|  
|via|char(100)|体现途径|alipay,weixin|weixin|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```
