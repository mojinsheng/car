# 汽车维修app端接口文档
## 目录
 1. [登陆验证机制](#login)
 - [登陆](#login_login)
 - [刷新token](#login_refresh)
 2. [个人中心](#user)
 - [用户信息](#user_user)
    * [用户注册](#user_user_list_post)
    * [司机端用户注册](#user_user_driver_list_post)
    * [查询自身信息](#user_user_get)
    * [修改自身信息](#user_user_put)
 - [车辆信息](#user_car)
    * [查询所有车辆信息](#user_car_list_get)
    * [添加车辆信息](#user_car_list_post)
    * [查询车辆信息](#user_car_get)
    * [修改车辆信息](#user_car_put)
    * [删除车辆信息](#user_car_delete)
 - [地址信息](#user_address)
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
    * [查询资讯列表信息](#service_news_list_get)
    * [查询资讯信息](#service_news_get)
 4. [维修厂](#maintain)
  - [汽修厂](#maintain_garage)
    * [查询汽修厂列表信息](#maintain_garage_list_get)
    * [查询汽修厂信息](#maintain_garage_get)
  - [机油](#maintain_oil)
    * [查询机油列表信息](#maintain_oil_list_get)
  - [保养](#maintain_upkeep)
    * [查询保养列表信息](#maintain_upkeep_list_get)
    * [生成保养订单信息](#maintain_upkeep_list_post)
    * [查询保养信息](#maintain_upkeep_get)
    * [删除保养订单信息](#maintain_upkeep_delete)
    * [付款、评价保养订单信息](#maintain_upkeep_method_post)
  - [维修](#maintain_maintain)
    * [查询维修列表信息](#maintain_maintain_list_get)
    * [生成维修订单信息](#maintain_maintain_list_post)
    * [查询维修信息](#maintain_maintain_get)
    * [删除维修订单信息](#maintain_maintain_delete)
    * [付款、完成、评论维修订单信息](#maintain_maintain_method_post)
 5. [年检](#survey)
  - [年检站信息](#survey_surveystation)
    * [查询年检站列表信息](#survey_surveystation_list_get)
    * [查询年检站信息](#survey_surveystation_get)
 - [年检订单信息](#survey_survey)
    * [查询年检订单列表信息](#survey_survey_list_get)
    * [提交年检订单信息](#survey_survey_list_post)
    * [查询年检订单信息](#survey_survey_get)
    * [删除年检订单信息](#survey_survey_delete)
    * [年检订单操作信息-确定还车、抢单、确定取车、年检完成、申请还车](#survey_survey_method_post)
    * [听单信息](#survey_surveywait_post)

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
|999|未开发|  

```
url中的<id>表示信息的主键id  
```

<h2 id="login">登陆验证机制</h2>

```
1.登陆成功获取user_id、token、expire
2.每次接口请求的时候，app端生成一个时间戳timestamp，使用token+timestamp进行md5，生成sign
3.然后每次请求都需要附带上user_id、timestamp、sign三个参数
4.token有时效，快过期前，请使用刷新接口获得新的token，过期没有更换的话，就只能重新登陆获取了
5.所有请求都带版本号，没带默认为0
```
|参数|类型|说明|备注|  
|---|---|---|---|  
|user_id|int|用户id|登陆成功后返回|  
|timestamp|char(50)|时间戳|app自己生成|  
|sign|char(50)|签名|md5(token+timestamp)|  
|version|char(50)|版本|默认0|  

<h3 id="login_login">登陆</h3>

url:/api/login/login/   
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|  
|password|char(20)|密码|6-20，字母、数字、符号|  
```
{
    'phone':'12345678998',
    'password':'123456'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|user_id|int|用户id|无|  
|token|char(50)|凭证|无|  
|expire|int|有效时间|单位：秒|  
```
{
    'data':{
        'user_id':'1'
        'token':'sjkdhasjkhf123jga',
        'expire':1800
    }
}
```

<h3 id="login_refresh">刷新token</h3>

url:/api/login/refresh/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|user_id|int|用户id|无|  
|token|char(50)|凭证|无|  
|expire|int|有效时间|单位：秒|  
```
{
    'data':{
        'user_id':'1'
        'token':'sjkdhasjkhf123jga',
        'expire':1800
    }
}
```

<h2 id="user">个人中心</h2>

<h3 id="user_user">用户信息</h3>

<h4 id="user_user_list_post">用户注册</h3>

url:/api/user/user/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|  
|password|char(20)|密码|6-20，字母、数字、符号|  
|name|char(20)|昵称|无|  
```
{
    'phone':'12345678998',
    'password':'123456789qwer+',
    'name':'张三'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h4 id="user_user_driver_list_post">司机端用户注册</h3>

url:/api/user/user_driver/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|  
|password|char(20)|密码|6-20，字母、数字、符号|  
|name|char(20)|昵称|无|  
```
{
    'phone':'12345678998',
    'password':'123456789qwer+',
    'name':'张三'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h4 id="user_user_get">查询自身信息</h3>

url:/api/user/user/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|phone|char(20)|电话号码|无|  
|name|char(10)|昵称|无|  
|pic_url|char(50)|照片url|http://host:port/url/,获取图片|  
|point|int|积分|无|  
```
{
    'data':{
        'id':1,
        'phone':'12345678998',
        'name':'admin',
        'pic':'/alsdfh.jpg',
        'point':'20'
    }
}
```

<h4 id="user_user_put">修改自身信息</h3>

url:/api/user/user/<id:int>/  
method:put  
dataType:multipart/from-data
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(10)|昵称|无|  
|pic|文件流|照片文件|无|  
```
{
    'name':'admin',
    'pic':(文件流)
}
```
return:
|参数|类型|说明|  
|---|---|---|  
```
{    
    'data':{}
}
```

<h3 id="user_car">车辆信息</h3>

<h4 id="user_car_list_get">查询所有车辆信息</h3>

url:/api/user/car/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|brand|char(20)|品牌|无|  
|buy_time|datetime|购车时间|无|  
|code|char(10)|车牌号码|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'brand':'玛萨拉蒂',
        'buy_time':'2018-03-20 12:23:34',
        'code':'粤A24351'
    }]
}
```

<h4 id="user_car_list_post">添加车辆信息</h3>

url:/api/user/car/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|brand|char(20)|品牌|无|  
|buy_time|datetime|购车时间|无|  
|code|char(10)|车牌号码|无|  
```
{
    'brand':'玛萨拉蒂',
    'buy_time':'2018-03-20 12:23:34',
    'code':'粤A24351'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':[]
}
```

<h4 id="user_car_get">查询车辆信息</h3>

url:/api/user/car/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|brand|char(20)|品牌|无|  
|buy_time|datetime|购车时间|无|  
|code|char(10)|车牌号码|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'brand':'玛萨拉蒂',
        'buy_time':'2018-03-20 12:23:34',
        'code':'粤A24351'
    }
}
```

<h4 id="user_car_put">修改车辆信息</h3>

url:/api/user/car/<id:int>/  
method:put  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|brand|char(20)|品牌|无|  
|buy_time|datetime|购车时间|无|  
|code|char(10)|车牌号码|无|  
```
{
    'brand':'玛萨拉蒂',
    'buy_time':'2018-03-20 12:23:34',
    'code':'粤A24351'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="user_car_delete">删除车辆信息</h3>

url:/api/user/car/<id:int>/  
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="user_address">地址信息</h3>

<h4 id="user_address_list_get">查询地址列表信息</h3>

url:/api/user/address/   
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|name|char(10)|收货人姓名|无|  
|phone|char(15)|联系电话|无|  
|city|char(50)|省市区|无|  
|address|char(100)|收货地址|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'123456789984',
        'city':'广州市'
        'address':'广州市越秀区xxx'
    }]
}
```

<h4 id="user_address_list_post">添加地址信息</h3>

url:/api/user/address/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(10)|收货人姓名|无|  
|phone|char(15)|联系电话|无|  
|city|char(50)|省市区|无|  
|address|char(100)|收货地址|无|  
```
{
    'name':'张三',
    'phone':'123456789984',
    'city':'广州市'
    'address':'广州市越秀区xxx'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="user_address_get">查询地址信息</h3>

url:/api/user/address/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|name|char(10)|收货人姓名|无|  
|phone|char(15)|联系电话|无|  
|city|char(50)|省市区|无|  
|address|char(100)|收货地址|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'123456789984',
        'city':'广州市'
        'address':'广州市越秀区xxx'
    }
}
```

<h4 id="user_address_put">修改地址信息</h3>

url:/api/user/address/<id:int>/  
method:put  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(10)|收货人姓名|无|  
|phone|char(15)|联系电话|无|  
|city|char(50)|省市区|无|  
|address|char(100)|收货地址|无|  
```
{
    'name':'张三',
    'phone':'123456789984',
    'city':'广州市'
    'address':'广州市越秀区xxx'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="user_address_delete">删除地址信息</h3>

url:/api/user/address/<id:int>/  
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
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

<h4 id="service_catalog_list_get">查询分类列表信息</h3>

url:/api/service/catalog/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|type|int|类型|可选，0:正常，1:保险|  
```
{
    'type':0
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|p_id|int|父id|0为根目录|  
|type|int|类型|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'过滤系统',
        'p_id':0,
        'type':0
    }]
}
```

<h4 id="service_catalog_get">查询分类信息</h3>

url:/api/service/catalog/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
```
{
    'id':1
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|p_id|int|父id|0为根目录|  
|type|int|类型|无|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'过滤系统',
        'p_id':0,
        'type':0
    }
}
```

<h3 id="service_product">物品信息</h3>

<h4 id="service_product_list_get">查询物品列表信息</h3>

url:/api/service/product/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|catalog_id|int|分类id|可选|  
```
{
    'catalog_id':1
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|price|float|价格|无|  
|special_price|float|特价|无|  
|param|text|参数信息|无|  
|type|text|车型信息|无|  
|catalog|object|分类|查看分类查询接口|  
|amount|int|库存|无|  
|pic_url_list|list|图片url列表|图片都放在这个文件夹下|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'轮胎',
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
    }]
}
```

<h4 id="service_product_get">查询物品信息</h3>

url:/api/service/product/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|price|float|价格|无|  
|special_price|float|特价|无|  
|param|text|参数信息|无|  
|type|text|车型信息|无|  
|catalog|object|分类|查看分类查询接口|  
|amount|int|库存|无|  
|pic_url_list|list|图片url列表|图片都放在这个文件夹下|  
```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'轮胎',
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
    }
}
```

<h3 id="service_ordercar">购物车信息</h3>

<h4 id="service_ordercar_list_get">查询购物车物品列表信息</h3>

url:/api/service/ordercar/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
        }
        'amount':666
    }]
}
```

<h4 id="service_ordercar_list_post">添加购物车物品信息</h3>

url:/api/service/ordercar/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|product_id|int|物品id|无|  
|amount|int|数量|无|  
```
{
    'product_id':1,
    'amount':'123456789984'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_ordercar_get">查询购物车物品信息</h3>

url:/api/service/ordercar/<id::int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
        }
        'amount':666
    }]
}
```

<h4 id="service_ordercar_put">修改购物车物品信息</h3>

url:/api/service/ordercar/<id:int>/  
method:put  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|product_id|int|物品id|无|  
|amount|int|数量|无|  
```
{
    'product_id':1,
    'amount':'123456789984'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_ordercar_delete">删除购物车物品信息</h3>

url:/api/service/ordercar/<id:int>/   
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="service_order">订单信息</h3>

<h4 id="service_order_list_post">查询订单列表信息</h3>

url:/api/service/order/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|收货人姓名|来源于所选地址|  
|phone|char(15)|联系电话|来源于所选地址|  
|city|char(50)|省市区|来源于所选地址|  
|address|char(100)|收货地址|来源于所选地址|  
|status|int|状态|0:未下单，1:已删除，2:待付款，2:待发货，3:待收货，4:已完成|  
|order_time|datetime|下单时间|无|  
|wait_time|datetime|付款时间|无|  
|send_time|datetime|发货时间|无|  
|receive_time|datetime|收货时间|无|  
|confirm_time|datetime|确认时间|无|  
|product_list|list|物品列表|无|  
product:
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
        'name':'张三',
        'phone':'12345678998',
        'city':'广州市',
        'address':'广州市越秀区xxx',
        'status':0,
        'order_time':'2018-07-08 12:23:34',
        'wait_time':'2018-07-08 12:23:34',
        'send_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'product_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'product':
            {
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'轮胎',
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
            }
            'amount':1,
            'price':1
        }]
    }]
}
```

<h4 id="service_order_list_post">生成订单</h3>

url:/api/service/order/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_order_get">查询订单信息</h3>

url:/api/service/order/<id::int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|收货人姓名|来源于所选地址|  
|phone|char(15)|联系电话|来源于所选地址|  
|city|char(50)|省市区|来源于所选地址|  
|address|char(100)|收货地址|来源于所选地址|  
|status|int|状态|0:未下单，1:已删除，2:待付款，2:待发货，3:待收货，4:已完成|  
|order_time|datetime|下单时间|无|  
|wait_time|datetime|付款时间|无|  
|send_time|datetime|发货时间|无|  
|receive_time|datetime|收货时间|无|  
|confirm_time|datetime|确认时间|无|  
|product_list|list|物品列表|无|  
product:
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
        'name':'张三',
        'phone':'12345678998',
        'city':'广州市',
        'address':'广州市越秀区xxx',
        'status':0,
        'order_time':'2018-07-08 12:23:34',
        'wait_time':'2018-07-08 12:23:34',
        'send_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'product_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'product':
            {
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'轮胎',
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
            }
            'amount':1,
            'price':1
        }]
    }
}
```

<h4 id="service_order_method_post">付款、完成订单信息</h3>

url:/api/service/order_method/<id:int>/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|method|char(20)|操作|pay:付款，finish:完成|  
```
{
    'method':'pay',
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_order_delete">删除订单信息</h3>

url:/api/service/order/<id:int>/   
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="service_rules">违章记录信息</h3>

<h4 id="service_rules_list_get">查询违章记录列表信息</h3>

url:/api/service/rules/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|code|char(10)|车牌|无|  
|content|text|违章内容|无|  
|score|int|扣分|无|  
|price|float|罚款|无|  
|time|datetime|时间|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'code':'粤A23452',
        'content':'违停',
        'score':1,
        'price':200,
        'time':'2018-07-02 12:23:34'
    }]
}
```

<h4 id="service_rules_get">查询违章记录信息</h3>

url:/api/service/rules/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|code|char(10)|车牌|无|  
|content|text|违章内容|无|  
|score|int|扣分|无|  
|price|float|罚款|无|  
|time|datetime|时间|无|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'code':'粤A23452',
        'content':'违停',
        'score':1,
        'price':200,
        'time':'2018-07-02 12:23:34'
    }]
}
```

<h3 id="service_newscatalog">资讯分类信息</h3>

<h4 id="service_newscatalog_list_get">查询资讯分类列表信息</h3>

url:/api/service/newscatalog/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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

<h4 id="service_newscatalog_get">查询资讯分类信息</h3>

url:/api/service/newscatalog/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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

<h4 id="service_news_list_get">查询资讯列表信息</h3>

url:/api/service/news/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|catalog_id|int|分类id|可选|  
```
{
    'catalog_id':0
}
```
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
        'pic_url_list':['/asd.hpg','/fasda.jpg']
    }]
}
```

<h4 id="service_news_get">查询资讯信息</h3>

url:/api/service/news/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|catalog|object|分类|查询资讯分类信息|  
|title|char(100)|标题|无|  
|content|text|内容|无|  
|pic_url|char(50)|封面url|无|  
|pic_url_list|list|图片url列表|图片都放在这个文件夹下|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'catalog':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'新闻资讯'
        },
        'title':'被抢劫了',
        'content':'没钱了',
        'pic_url':'asdla.jpg',
        'pic_url_list':['/asd.hpg','/fasda.jpg']
    }]
}
```

<h2 id="maintain">维修厂</h2>

<h3 id="maintain_garage">汽修厂</h3>

<h4 id="maintain_garage_list_get">查询汽修厂列表信息</h3>

url:/api/maintain/garage/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|user_name|char(50)|负责人名称|无|  
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
|mobile_phone|char(20)|手机号码|无|  
|phone|char(20)|固定电话|无|  
|oil_block|float|机油格价格|保养使用|  
|work_price|float|工时费|保养使用|  
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
        'oil_block':70,
        'work_price':88
    }]
}
```

<h4 id="maintain_garage_get">查询汽修厂信息</h3>

url:/api/maintain/garage/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|user_name|char(50)|负责人名称|无|  
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
|mobile_phone|char(20)|手机号码|无|  
|phone|char(20)|固定电话|无|  
|oil_block|float|机油格价格|保养使用|  
|work_price|float|工时费|保养使用|  
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
        'oil_block':70,
        'work_price':88
    }
}
```

<h3 id="maintain_oil">机油</h3>

<h4 id="maintain_oil_list_get">查询机油列表信息</h3>

url:/api/maintain/oil/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|garage_id|int|汽修厂id|必选|  
```
{
    'garage_id':1
}
```
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
        'new_price':1
    }]
}
```

<h3 id="maintain_upkeep">保养</h3>

<h4 id="maintain_upkeep_list_get">查询保养列表信息</h3>

url:/api/maintain/upkeep/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|car_code|char(10)|车牌|无|  
|car_brand|char(20)|车型|无|  
|address|char(100)|地址|无|  
|phone|char(20)|电话号码|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|order_time|datetime|下单时间|无|  
|price|float|价格|无|  
|oil_block|float|机油格价格|保养使用|  
|work_price|float|工时费|保养使用|  
|state|int|状态|0:等待|  
|score|int|评分|大于等于0，小于等于5|  
|over_time|datetime|结束时间|无|  
|comment_time|datetime|评价时间|无|  
|upkeepoil_list|list|机油|无|  
upkeepoil_list:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|1|自增|  
|create_time|datetime|创建时间|2018-07-08 12:23:34|无|  
|update_time|datetime|修改时间|2018-07-08 12:23:34|无|  
|oil|object|机油|查询机油列表信息|  
|price|float|原价|无|  
|special_price|float|特价|无|  
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
        'car_code':'粤A23452',
        'car_brand':'玛萨拉蒂',
        'address':'广州市越秀区',
        'phone':'12345678998',
        'subscribe_time':'2018-07-08 12:23:34',
        'content':'修理',
        'order_time':'2018-07-08 12:23:34',
        'price':1,
        'oil_block':70,
        'work_price':88,
        'state':1,
        'score':1,
        'over_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'upkeepoil_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'oil':{
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'没油',
                'L':2,
                'price':1,
                'new_price':1
            },
            'price':1,
            'special_price':1,
        }]
    }]
}
```

<h4 id="maintain_upkeep_list_post">生成保养订单信息</h3>

url:/api/maintain/upkeep/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|garage_id|int|汽修厂id|无|  
|name|char(20)|名称|无|  
|car_code|char(10)|车牌|无|  
|car_brand|char(20)|车型|无|  
|address|char(100)|地址|无|  
|phone|char(20)|电话号码|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|oil_list|list|机油|无|  
oil_list:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|1|自增|  
```
{
    'garage_id':1,
    'name':'张三',
    'car_code':'粤A23452',
    'car_brand':'玛萨拉蒂',
    'address':'广州市越秀区',
    'phone':'12345678998',
    'subscribe_time':'2018-07-08 12:23:34',
    'content':'修理',
    'oil_list':[{
        'id':1
    }]
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h4 id="maintain_upkeep_get">查询保养信息</h3>

url:/api/maintain/upkeep/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|car_code|char(10)|车牌|无|  
|car_brand|char(20)|车型|无|  
|address|char(100)|地址|无|  
|phone|char(20)|电话号码|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|order_time|datetime|下单时间|无|  
|price|float|价格|无|  
|oil_block|float|机油格价格|保养使用|  
|work_price|float|工时费|保养使用|  
|state|int|状态|0:等待|  
|score|int|评分|大于等于0，小于等于5|  
|over_time|datetime|结束时间|无|  
|comment_time|datetime|评价时间|无|  
|upkeepoil_list|list|机油|无|  
upkeepoil_list:
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|1|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|oil|object|机油|查询机油列表信息|  
|price|float|原价|无|  
|special_price|float|特价|无|  
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
        'car_code':'粤A23452',
        'car_brand':'玛萨拉蒂',
        'address':'广州市越秀区',
        'phone':'12345678998',
        'subscribe_time':'2018-07-08 12:23:34',
        'content':'修理',
        'order_time':'2018-07-08 12:23:34',
        'price':1,
        'oil_block':70,
        'work_price':88,
        'state':1,
        'score':1,
        'over_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'upkeepoil_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'oil':{
                'id':1,
                'create_time':'2018-07-08 12:23:34',
                'update_time':'2018-07-08 12:23:34',
                'name':'没油',
                'L':2,
                'price':1,
                'new_price':1
            },
            'price':1,
            'special_price':1,
        }]
    }
}
```

<h4 id="maintain_upkeep_delete">删除保养订单信息</h3>

url:/api/maintain/upkeep/<id:int>/  
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="maintain_upkeep_method_post">付款、评价保养订单信息</h3>

url:/api/maintain/upkeep_method/<id:int>/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|method|char(20)|操作|pay:付款，comment:评论|  
|score|int|评分|大于等于0，小于等于5|  
```
{
    'method':'comment',
    'score':1
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h3 id="maintain_maintain">维修</h3>

<h4 id="maintain_maintain_list_get">查询维修列表信息</h3>

url:/api/maintain/maintain/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|car_code|char(10)|车牌|无|  
|car_brand|char(20)|车型|无|  
|address|char(100)|地址|无|  
|phone|char(20)|电话号码|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|order_time|datetime|下单时间|无|  
|price|float|价格|无|  
|receive_time|datetime|接单时间|无|  
|state|int|状态|0:等待接单，1:等待付款，2:等待服务，3:待评价，4:已完成，5:失败|  
|score|int|评分|大于等于0，小于等于5|  
|pay_time|datetime|付款时间|无|  
|service_time|datetime|服务时间|无|  
|over_time|datetime|完成时间|无|  
|pic_url_list|list|图片列表|无|  
pic_url_list
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  
|state|int|状态|0:等待接单，1:等待付款，2:等待服务，3:待评价，4:已完成，5:失败|  
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
        'car_code':'粤A23452',
        'car_brand':'玛萨拉蒂',
        'address':'广州市越秀区',
        'phone':'12345678998',
        'subscribe_time':'2018-07-08 12:23:34',
        'content':'修理',
        'order_time':'2018-07-08 12:23:34',
        'price':1,
        'receive_time':70,
        'state':1,
        'score':1,
        'pay_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'pic_url_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'pic_url':'/aklsdjalk.jpg',
            'note':'无图',
            'state':1
        }]
    }]
}
```

<h4 id="maintain_maintain_list_post">生成维修订单信息</h3>

url:/api/maintain/maintain/  
method:post  
dataType:multipart/from-data  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|garage_id|int|汽修厂id|无|  
|name|char(20)|名称|无|  
|car_code|char(10)|车牌|无|  
|car_brand|char(20)|车型|无|  
|address|char(100)|地址|无|  
|phone|char(20)|电话号码|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|pic1|文件流|图片|编号从1开始|  
|note1|char(100)|备注|编号从1开始|  
```
{
    'garage_id':1,
    'name':'张三',
    'car_code':'粤A23452',
    'car_brand':'玛萨拉蒂',
    'address':'广州市越秀区',
    'phone':'12345678998',
    'subscribe_time':'2018-07-08 12:23:34',
    'content':'修理',
    'pic1':(文件流),
    'note1':'无图'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h4 id="maintain_maintain_get">查询维修信息</h3>

url:/api/maintain/maintain/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|garage|object|汽修厂|查询汽修厂信息|  
|name|char(20)|名称|无|  
|car_code|char(10)|车牌|无|  
|car_brand|char(20)|车型|无|  
|address|char(100)|地址|无|  
|phone|char(20)|电话号码|无|  
|subscribe_time|datetime|预约时间|无|  
|content|text|内容|无|  
|order_time|datetime|下单时间|无|  
|price|float|价格|无|  
|receive_time|datetime|接单时间|无|  
|state|int|状态|0:等待接单，1:等待付款，2:等待服务，3:待评价，4:已完成，5:失败|  
|score|int|评分|大于等于0，小于等于5|  
|pay_time|datetime|付款时间|无|  
|service_time|datetime|服务时间|无|  
|over_time|datetime|完成时间|无|  
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
        'car_code':'粤A23452',
        'car_brand':'玛萨拉蒂',
        'address':'广州市越秀区',
        'phone':'12345678998',
        'subscribe_time':'2018-07-08 12:23:34',
        'content':'修理',
        'order_time':'2018-07-08 12:23:34',
        'price':1,
        'receive_time':'2018-07-08 12:23:34',
        'state':1,
        'score':1,
        'pay_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'pic_url_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'pic_url':'/aklsdjalk.jpg',
            'note':'无图',
            'state':1
        }]
    }
}
```

<h4 id="maintain_maintain_delete">删除维修订单信息</h3>

url:/api/maintain/maintain/<id:int>/  
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="maintain_maintain_method_post">付款、完成、评论维修订单信息</h3>

url:/api/maintain/maintain_method/<id:int>/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|method|char(20)|操作|pay:付款，finish:完成，comment:评论|  
|score|int|评分|大于等于0，小于等于5|  
```
{
    'method':'comment',
    'score':1
}
```
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

<h4 id="survey_surveystation_list_get">查询年检站列表信息</h3>

url:/api/survey/surveystation/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
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
        'address':'广州越秀区'
    }]
}
```

<h4 id="service_surveystation_get">查询年检站信息</h3>

url:/api/survey/surveystation/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|longitude|float|经度|无|  
|latitude|float|纬度|无|  
|address|char(100)|地址|无|  
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
        'address':'广州越秀区'
    }]
}
```

<h3 id="survey_survey">年检订单信息</h3>

<h4 id="survey_survey_list_get">查询年检订单列表信息</h3>

url:/api/survey/survey/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|  
|pic_IDcard_url|char(50)|身份证正面照|无|  
|pic_drive_front_url|char(50)|行驶证主页照|无|  
|pic_drive_front_url|char(50)|行驶证副页照|无|  
|car_name|char(20)|车主姓名|无|  
|id_card|char(20)|身份证|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:两人|  
|use_type|int|使用性质|0:非营利，1:营利|  
|surveystation|object|年检站|查询年检站信息|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|subscribe_time|datetime|预约日期|13点前表示上午，13点后表示下午|  
|price|float|年检费用|无|  
|total_price|float|总费用|无|  
|state|int|状态|0:已提交，1:已接单，2:已取车，3.已年检，4.已还车，5.已完成，6.失败|  
|drive_user_id|int|用户id|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|take_time|datetime|取车时间|无|  
|survey_time|datetime|年检时间|无|  
|back_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|surveycost_list|list|费用列表|无|  
|pic_url_list|list|图片列表|无|  
surveycost_list
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|1|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(100)|费用名称|无|  
|price|float|费用|无|  
pic_url_list
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(100)|图片|无|  
|note|char(100)|备注|无|  
|state|int|状态|0:已提交，1:已接单，2:已取车，3.已年检，4.已还车，5.已完成，6.失败|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'12345678998',
        'pic_IDcard_url':'/kdhaskdjflhas.jpg',
        'pic_drive_front_url':'/kdhaskdjflhas.jpg',
        'pic_drive_front_url':'/kdhaskdjflhas.jpg',
        'car_name':'张三',
        'id_card':'198236817268',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':1,
        'use_type':1,
        'surveystation':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'张三年检站',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区'
        },
        'order_longitude':223,
        'order_latitude':322,
        'subscribe_time':'2018-07-08 12:23:34',
        'price':1,
        'total_price':1,
        'state':1,
        'drive_user_id':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'take_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'back_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'surveycost_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'材料费',
            'price':12
        }]
        'pic_url_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'pic_url':'/aklsdjalk.jpg',
            'note':'无图',
            'state':1
        }]
    }]
}
```

<h4 id="survey_survey_list_post">提交年检订单信息</h3>

url:/api/survey/survey/  
method:post  
dataType:multipart/from-data  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|  
|pic_IDcard|文件流|身份证正面照|无|  
|pic_drive_front|文件流|行驶证主页照|无|  
|pic_drive_front|文件流|行驶证副页照|无|  
|car_name|char(20)|车主姓名|无|  
|id_card|char(20)|身份证|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:两人|  
|use_type|int|使用性质|0:非营利，1:营利|  
|urveystation_id|int|年检站id|无|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|subscribe_time|datetime|预约日期|13点前表示上午，13点后表示下午|  
```
{
    'name':'张三',
    'phone':'12345678998',
    'pic_IDcard':(文件流),
    'pic_drive_front':(文件流),
    'pic_drive_front':(文件流),
    'car_name':'张三',
    'id_card':'198236817268',
    'car_brand':'玛萨拉蒂',
    'car_code':'粤A23452',
    'car_type':1,
    'use_type':1,
    'urveystation_id':1,
    'order_longitude':223,
    'order_latitude':322,
    'subscribe_time':'2018-07-08 12:23:34'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```


<h4 id="survey_survey_get">查询年检订单信息</h3>

url:/api/survey/survey/<id:int>/  
method:get  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
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
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|  
|pic_IDcard_url|char(50)|身份证正面照|无|  
|pic_drive_front_url|char(50)|行驶证主页照|无|  
|pic_drive_front_url|char(50)|行驶证副页照|无|  
|car_name|char(20)|车主姓名|无|  
|id_card|char(20)|身份证|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|int|车量类型|0:两人|  
|use_type|int|使用性质|0:非营利，1:营利|  
|surveystation|object|年检站|查询年检站信息|  
|order_longitude|float|交接地点经度|无|  
|order_latitude|float|交接地点纬度|无|  
|subscribe_time|datetime|预约日期|13点前表示上午，13点后表示下午|  
|price|float|年检费用|无|  
|total_price|float|总费用|无|  
|state|int|状态|0:已提交，1:已接单，2:已取车，3.已年检，4.已还车，5.已完成，6.失败|  
|drive_user_id|int|用户id|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|take_time|datetime|取车时间|无|  
|survey_time|datetime|年检时间|无|  
|back_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|surveycost_list|list|费用列表|无|  
|pic_url_list|list|图片列表|无|  
surveycost_list
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|1|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(100)|费用名称|无|  
|price|float|费用|无|  
pic_url_list
|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(100)|图片|无|  
|note|char(100)|备注|无|  
|state|int|状态|0:已提交，1:已接单，2:已取车，3.已年检，4.已还车，5.已完成，6.失败|  
```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'张三',
        'phone':'12345678998',
        'pic_IDcard_url':'/kdhaskdjflhas.jpg',
        'pic_drive_front_url':'/kdhaskdjflhas.jpg',
        'pic_drive_front_url':'/kdhaskdjflhas.jpg',
        'car_name':'张三',
        'id_card':'198236817268',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':1,
        'use_type':1,
        'surveystation':{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'张三年检站',
            'longitude':223,
            'latitude':322,
            'address':'广州越秀区'
        },
        'order_longitude':223,
        'order_latitude':322,
        'subscribe_time':'2018-07-08 12:23:34',
        'price':1,
        'total_price':1,
        'state':1,
        'drive_user_id':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'take_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'back_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'surveycost_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'name':'材料费',
            'price':12
        }]
        'pic_url_list':[{
            'id':1,
            'create_time':'2018-07-08 12:23:34',
            'update_time':'2018-07-08 12:23:34',
            'pic_url':'/aklsdjalk.jpg',
            'note':'无图',
            'state':1
        }]
    }]
}
```

<h4 id="survey_survey_delete">删除年检订单信息</h3>

url:/api/survey/survey/<id:int>/  
method:delete  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="survey_survey_method_post">年检订单操作信息-确定还车、抢单、确定取车、年检、申请还车</h3>

url:/api/survey/survey_method/<id:int>/  
method:post  
dataType:multipart/from-data  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|method|char(20)|操作|finish:确定还车，grab:抢单，revice:确定取车，survey:年检，return:申请还车|  
|pic1|文件流|图片|编号从1开始|  
|note1|char(100)|备注|编号从1开始|  
|name1|char(100)|费用名称|编号从1开始|  
|price1|float|费用名称|编号从1开始|  
```
{
    'method':'finish',
    'pic1':(文件流),
    'note1':'无图',
    'name1':'维修费',
    'price1':12
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="survey_surveywait_post">听单信息</h3>

url:/api/survey/surveywait/  
method:post  
param:   
|参数|类型|说明|备注|  
|---|---|---|---|  
|method|char(20)|操作|start:开始，end:结束|  
```
{
    'method':'start'
}
```
return:
|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```
