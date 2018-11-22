# 汽车维修app端接口文档
## 目录
 1. [登陆验证机制](#login)
 - [用户注册](#login_register)
 - [司机端用户注册](#login_register_driver)
 - [用户重置密码](#login_reset)
 - [司机端重置密码](#login_reset_driver)
 - [用户发短信](#login_message)
 - [登陆](#login_login)
 - [刷新token](#login_refresh)
 - [退出](#login_exit)
 1. [个人中心](#user)
  - [用户信息](#user_user)
    * [查询自身信息](#user_user_get)
    * [修改自身信息](#user_user_put)
  - [车辆信息](#user_car)
    * [查询车辆二级地址信息](#user_caraddress_list_get)
    * [查询车辆品牌信息](#user_carbrand_list_get)
    * [查询车辆车型信息](#user_cartype_list_get)
    * [查询车辆款式信息](#user_carstyle_list_get)
    * [查询所有车辆信息](#user_car_list_get)
    * [添加车辆信息](#user_car_list_post)
    * [查询车辆信息](#user_car_get)
    * [修改车辆信息](#user_car_put)
    * [删除车辆信息](#user_car_delete)
  - [地址信息](#user_address)
    * [查询三级地址文件信息](#user_addressinfo_list_get)
    * [查询三级地址信息](#user_addressinfo_get)
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
    * [查询物品详情页面](#service_product_detail_get)
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
    * [查询交易状态、付款、完成、评论订单信息](#service_order_method_post)
    * [查询订单快递信息](#service_orderlogistics_get)
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
    * [查询资讯详情页面](#service_news_detail_get)
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
    * [查询交易状态、付款、完成、评论保养订单信息](#maintain_upkeep_method_post)
    * [查询保养售后列表信息](#maintain_upkeep_aftersales_list_get)
    * [生成保养售后订单信息](#maintain_upkeep_aftersales_list_post)
    * [查询保养售后信息](#maintain_upkeep_aftersales_get)
    * [完成保养售后订单信息](#maintain_upkeep_aftersales_method_post)
  - [维修](#maintain_maintain)
    * [查询维修列表信息](#maintain_maintain_list_get)
    * [生成维修订单信息](#maintain_maintain_list_post)
    * [查询维修信息](#maintain_maintain_get)
    * [删除维修订单信息](#maintain_maintain_delete)
    * [查询交易状态、修改维修项、付款、完成、评论维修订单信息](#maintain_maintain_method_post)
    * [查询维修售后列表信息](#maintain_maintain_aftersales_list_get)
    * [生成维修售后订单信息](#maintain_maintain_aftersales_list_post)
    * [查询维修售后信息](#maintain_maintain_aftersales_get)
    * [完成维修售后订单信息](#maintain_maintain_aftersales_method_post)
    * [极光推送维修订单接单信息](#maintain_maintain_jpush_order_get)
    * [极光推送维修订单下发清单信息](#maintain_maintain_jpush_item_get)
    * [极光推送维修订单完成信息](#maintain_maintain_jpush_finish_get)
  - [保养、维修订单列表信息](#maintain_list_get)  
  - [保养、维修售后列表信息](#maintain_aftersales_list_get)  
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
    * [自驾年检订单操作信息-取消、查询费用、支付、确认到达(完成订单)](#survey_survey_selfmethod_post)
    * [代驾年检订单操作信息-取消、查询费用、支付、失败支付、确认还车、评分](#survey_survey_behalfmethod_post)
    * [年检投诉](#survey_survey_feedback_post)
    * [自驾咨询电话](#survey_survey_phone_get)
    * [年检须知](#survey_survey_info_get)
    * [用户扣费标准](#survey_survey_usercancelinfo_get)
    * [极光推送年检订单接单信息](#survey_survey_jpush_grab_get)
 6. [系统](#system)
  - [服务首页图片信息](#system_serviceimg_get)
  - [年检首页图片信息](#system_surveyimg_get) 
  - [封面图片信息](#system_cover_get) 
  - [关于我们](#system_aboutus_get) 
  - [注册用户协议](#system_useragreement_get) 
 7. [司机端](#driver)
  - [订单](#driver_order)
    * [查询订单列表信息](#driver_order_list_get)
    * [查询订单信息](#driver_order_get)
    * [查询提交图片的类别名称信息](#driver_order_picname_get)
    * [查询年检检查项信息](#driver_order_surveyitem_get)
    * [抢单](#driver_order_grab_post)
    * [取消订单](#driver_order_cancel_post)
    * [确认取车](#driver_order_get_post)
    * [开始年检](#driver_order_survey_post)
    * [年检已过](#driver_order_success_post)
    * [年检未过](#driver_order_fail_post)
    * [到达还车](#driver_order_arrive_post)
    * [确认换车](#driver_order_return_post)
    * [查询订单列表信息-服务端推送](#ws_driver_order)
    * [听单-服务端推送](#ws_driver_listen)
    * [司机扣费标准](#driver_order_drivercancelinfo_get)
  - [账户](#driver_account)
    * [查询绑定的支付宝账号](#driver_account_alipay_get)
    * [获取绑定的支付宝账号信息](#driver_account_alipay_info_get)
    * [进行支付宝账号绑定](#driver_account_alipay_post)
    * [查询明细列表信息](#driver_account_list_get)
    * [查询明细信息](#driver_account_get)
    * [明细操作信息-提现](#driver_account_method_post)
    * [用户余额查询](#driver_balance_get)
    * [司机资料](#driver_driver_info_get)

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
6.目前不需要登陆的有：登陆模块（除了刷新token接口），服务模块中的分类信息、物品信息、资讯分类信息、资讯信息，年检模块中的自驾咨询电话、年检须知、用户扣费标准，系统模块
```
|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|user_id|int|用户id|登陆成功后返回|1|必填|  
|timestamp|char(50)|时间戳|app自己生成|1|必填|  
|sign|char(50)|签名|md5(token+timestamp)|asdadsa|必填|  
|system|char(50)|系统|android,ios|ios|必填|  
|app_type|char(50)|用户端类型|user,driver|user|必填|  
|version|char(50)|版本|xx.yyzz|1.0000|必填|  

<h3 id="login_register">用户注册</h3>

url:/api/login/register/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|必填|  
|name|char(20)|姓名|无|张三|必填|  
|password|char(20)|密码|6-20，字母、数字、符号|123456789qwer|必填|  
|message|char(10)|短信验证码|6位数字|123456|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|必填|  
|name|char(20)|姓名|无|张三|必填|  
|password|char(20)|密码|6-20，字母、数字、符号|123456789qwer|必填|  
|message|char(10)|短信验证码|6位数字|123456|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h3 id="login_reset">用户重置密码</h3>

url:/api/login/reset/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|必填|  
|password|char(20)|密码|6-20，字母、数字、符号|123456789qwer|必填|  
|message|char(10)|短信验证码|6位数字|123456|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h4 id="login_reset_driver">司机端重置密码</h4>

url:/api/login/reset_driver/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|必填|  
|password|char(20)|密码|6-20，字母、数字、符号|123456789qwer|必填|  
|message|char(10)|短信验证码|6位数字|123456|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    data:{}
}
```

<h3 id="login_message">用户发短信</h3>

url:/api/login/message/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|必填|  
|type|char(50)|类型|register：用户注册、reset：用户重置密码、register_driver：司机注册、reset_driver：司机重置密码|register|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|phone|char(20)|电话号码|作为账号|12345678998|必填|  
|password|char(20)|密码|6-20，字母、数字、符号|123456|必填|  

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

<h3 id="login_refresh">刷新token</h3>

url:/api/login/refresh/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

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

<h3 id="login_exit">退出</h3>

url:/api/login/exit/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{
    }
}
```

<h2 id="user">个人中心</h2>

<h3 id="user_user">用户信息</h3>

<h4 id="user_user_get">查询自身信息</h4>

url:/api/user/user/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|account|char(100)|帐号|无|  
|phone|char(20)|电话号码|无|  
|name|char(10)|昵称|无|  
|pic_url|char(50)|照片url|/url,获取图片|  
|point|int|积分|无|  
|score|int|司机评分|无|  
|is_pass|bool|是否过审|无|  
|is_driverinfo|int|0：未提交，1：正在审核，2：审核成功，3：审核失败|无|  
```
{
    'data':{
        'id':1,
        'account':'dasdasdas',
        'phone':'12345678998',
        'name':'admin',
        'pic':'/alsdfh.jpg',
        'point':20,
        'is_pass':false,
        'is_driverinfo':false
    }
}
```

<h4 id="user_user_put">修改自身信息</h4>

url:/api/user/user/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|phone|char(20)|电话号码|作为账号|12345678998|选填|  
|name|char(10)|昵称|无|admin|选填|  
|pic|文件流|照片文件|无|(文件流，base64)|选填|  

return:  

|参数|类型|说明|  
|---|---|---|  
```
{    
    'data':{}
}
```

<h3 id="user_car">车辆信息</h3>

<h4 id="user_caraddress_list_get">查询车辆二级地址信息</h4>

url:/api/user/caraddress/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|province|char(50)|名称|无|  
|carcity_set|list|城市对象列表|无|  

carcity_set:

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|city_name|char(50)|名称|无|  
|city_code|char(50)|代码|无|  

```
{
    'data':
    [{
        "id": 1,
        "province": "北京",
        "carcity_set": [
            {
                "id": 1,
                "city_name": "北京",
                "city_code": "BJ"
            }
        ]
    }]
}
```

<h4 id="user_carbrand_list_get">查询车辆品牌信息</h4>

url:/api/user/carbrand/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|A|list|A排序下的品牌对象列表|无|  
|B|list|B排序下的品牌对象列表|无|  
......

A:

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|name|char(100)|名称|无|  

```
{
    'data':
    {
        'A':[{
            'id':1
            'name':'阿斯顿马丁'
        }],
        'B':[],
        'C':[],
        ......
    }
}
```

<h4 id="user_cartype_list_get">查询车辆车型信息</h4>

url:/api/user/cartype/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|车辆品牌id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|name|char(100)|名称|无|  

```
{
    'data':
    [{
        'id':1
        'name':'阿斯顿马丁'
    }]
}
```

<h4 id="user_carstyle_list_get">查询车辆款式信息</h4>

url:/api/user/carstyle/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|车辆车型id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|name|char(100)|名称|无|  
|year|int|年份|无|  

```
{
    'data':
    [{
        'id':1
        'name':'阿斯顿马丁',
        'year':1234
    }]
}
```

<h4 id="user_car_list_get">查询所有车辆信息</h4>

url:/api/user/car/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|is_default|bool|是否为默认|无|true|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(50)|照片url|/url,获取图片|  
|brand_name|char(100)|品牌|无|  
|car_brand_id|int|品牌id|无|  
|car_type_id|int|车型id|无|  
|car_style_id|int|款式id|无|  
|code|char(10)|车牌号码|无|  
|engine|char(100)|发动机|无|  
|is_default|bool|是否默认|无|  
|city_code|char(100)|城市代码|无|  
|classsno|char(100)|车架号|无|  
|hpzl|char(5)|号牌类型|02:小型车，01:大型车,16:教练车|  
|province_code|char(100)|省代码|无|  
|city_name|char(100)|城市名称|无|  
|province_name|char(100)|省名称|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'pic_url':'/alsdfh.jpg',
        'brand_name':'玛萨拉蒂',
        'car_brand_id':'3',
        'car_type_id':'2',
        'car_style_id':'1',
        'code':'粤A24351',
        'engine':'TX21',
        'is_default':false,
        'city_code':'SH',
        'classsno':'121231',
        'hpzl':'02',
        'province_code':'SH',
        'city_name':'上海',
        'province_name':'上海'
    }]
}
```

<h4 id="user_car_list_post">添加车辆信息</h4>

url:/api/user/car/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|code|char(10)|车牌号码|无|粤A24351|必填|  
|pic|文件流|照片文件|无|(文件流，base64)|选填|  
|car_style|int|车辆款式|无|1|必填|  
|engine|char(100)|发动机|无|TX21|必填|  
|is_default|bool|是否默认|无|false|选填|  
|city_code|char(100)|城市代码|无|SH|必填|  
|classsno|char(100)|车架号|无|affa123fd|必填|  
|hpzl|char(5)|号牌类型|02:小型车，01:大型车,16:教练车|02|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|pic_url|char(50)|照片url|/url,获取图片|  
|brand_name|char(100)|品牌|无|  
|car_brand_id|int|品牌id|无|  
|car_type_id|int|车型id|无|  
|car_style_id|int|款式id|无|  
|code|char(10)|车牌号码|无|  
|engine|char(100)|发动机|无|  
|is_default|bool|是否默认|无|  
|city_code|char(100)|城市代码|无|  
|classsno|char(100)|车架号|无|  
|hpzl|char(5)|号牌类型|02:小型车，01:大型车,16:教练车|  
|province_code|char(100)|省代码|无|  
|city_name|char(100)|城市名称|无|  
|province_name|char(100)|省名称|无|  

```
{
    'data':
    {
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'pic_url':'/alsdfh.jpg',
        'brand_name':'玛萨拉蒂',
        'car_brand_id':'3',
        'car_type_id':'2',
        'car_style_id':'1',
        'code':'粤A24351',
        'engine':'TX21',
        'is_default':false,
        'city_code':'SH',
        'classsno':'121231',
        'hpzl':'02',
        'province_code':'SH',
        'city_name':'上海',
        'province_name':'上海'
    }
}
```

<h4 id="user_car_put">修改车辆信息</h4>

url:/api/user/car/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|code|char(10)|车牌号码|无|粤A24351|选填|  
|pic|文件流|照片文件|无|(文件流，base64)|选填|  
|car_style|int|车辆款式|无|1|选填|  
|engine|char(100)|发动机|无|TX21|选填|  
|is_default|bool|是否默认|无|false|选填|  
|city_code|char(100)|城市代码|无|SH|选填|  
|classsno|char(100)|车架号|无|affa123fd|选填|  
|hpzl|char(5)|号牌类型|02:小型车，01:大型车,16:教练车|02|选填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

url:/api/user/addressinfo/   
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(10)|收货人姓名|无|  
|children|list|三级地址|无|  
```
{
    'data':
    [{
        'id':1,
        'name':'北京市',
        'children':[{
            'id':1,
            'name':'北京市',
            'children':[{
            }]
        }]
    }]
}
```

<h4 id="user_address_list_get">查询地址列表信息</h4>

url:/api/user/address/   
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|is_default|bool|是否为默认|无|true|选填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|name|char(10)|收货人姓名|无|张三|必填|  
|phone|char(15)|联系电话|无|123456789984|必填|  
|node1|int|第一级地址|无|1|必填|  
|node2|int|第二级地址|无|2|必填|  
|node3|int|第三级地址|无|3|必填|  
|address|char(100)|收货地址|无|广州市越秀区xxx|必填|  
|is_default|bool|是否默认|无|false|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|name|char(10)|收货人姓名|无|张三|选填|  
|phone|char(15)|联系电话|无|123456789984|选填|  
|node1|int|第一级地址|无|1|选填|  
|node2|int|第二级地址|无|2|选填|  
|node3|int|第三级地址|无|3|选填|  
|address|char(100)|收货地址|无|广州市越秀区xxx|选填|  
|is_default|bool|是否默认|无|false|选填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|type|int|类型|0:商城，1:保险|0|必填|    
|p_id|int|父id|根节点id为0|0|必填|    

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|     

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|catalog_id|int|分类id|无|1|选填|    
|price_order|int|价格排序|1:从低到高，2:从高到低|1|选填|    
|sale_order|int|销量排序|1:从低到高，2:从高到低|2|选填|    

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
|number|char(100)|编号|无|  
|car_type|char(100)|适用车型|无|  
|specification|char(500)|规格|无|  
|brand|char(100)|品牌|无|  
|sort|char(100)|类别|无|  
|unit|char(100)|单位|无|  
|production|char(100)|产地|无|  
|category|char(100)|品类|无|  
|car_type_list|char(500)|车型|无|  
|detail_url|char(500)|详情页面url|无|  
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
        'number':'顶配',
        'car_type':'顶配',
        'specification':'顶配',
        'brand':'顶配',
        'sort':'顶配',
        'unit':'顶配',
        'production':'顶配',
        'category':'顶配',
        'car_type_list':'顶配',
        'detail_url':'/uashdjk/',
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
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
|number|char(100)|编号|无|  
|car_type|char(100)|适用车型|无|  
|specification|char(500)|规格|无|  
|brand|char(100)|品牌|无|  
|sort|char(100)|类别|无|  
|unit|char(100)|单位|无|  
|production|char(100)|产地|无|  
|category|char(100)|品类|无|  
|car_type_list|char(500)|车型|无|  
|detail_url|char(500)|详情页面url|无|  
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
        'number':'顶配',
        'car_type':'顶配',
        'specification':'顶配',
        'brand':'顶配',
        'sort':'顶配',
        'unit':'顶配',
        'production':'顶配',
        'category':'顶配',
        'car_type_list':'顶配',
        'detail_url':'/uashdjk/',
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

<h4 id="service_product_detail_get">查询物品详情页面</h4>

url:/api/service/product_detail/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
```
{
}
```
return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
页面信息
```

<h3 id="service_ordercar">购物车信息</h3>

<h4 id="service_ordercar_list_get">查询购物车物品列表信息</h4>

url:/api/service/ordercar/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

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
            'number':'顶配',
            'car_type':'顶配',
            'specification':'顶配',
            'brand':'顶配',
            'sort':'顶配',
            'unit':'顶配',
            'production':'顶配',
            'category':'顶配',
            'car_type_list':'顶配',
            'detail_url':'/uashdjk/',
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
        'amount':666
    }]
}
```

<h4 id="service_ordercar_list_post">添加购物车物品信息</h4>

url:/api/service/ordercar/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|product_id|int|物品id|无|1|必填|  
|amount|int|数量|会在这个商品已有的基础上添加amount个，可以添加负数，最终结果只能为0|123456789984|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

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
            'number':'顶配',
            'car_type':'顶配',
            'specification':'顶配',
            'brand':'顶配',
            'sort':'顶配',
            'unit':'顶配',
            'production':'顶配',
            'category':'顶配',
            'car_type_list':'顶配',
            'detail_url':'/uashdjk/',
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
        'amount':666
    }
}
```

<h4 id="service_ordercar_put">修改购物车物品信息</h4>

url:/api/service/ordercar/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|    
|amount|int|数量|直接修改数量|123456789984|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|支持使用,来拼接多个id，实现批量删除|1|必填|   

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|status|int|状态|-1:全部，0:待付款，1:待发货，2:待收货，3:已完成|1|必选填|  
|is_comment|bool|是否评论|无|true|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单编号|无|  
|name|char(10)|收货人姓名|来源于所选地址|  
|phone|char(15)|联系电话|来源于所选地址|  
|city|char(50)|省市区|来源于所选地址|  
|address|char(100)|收货地址|来源于所选地址|  
|status|int|状态|0:待付款，1:待发货，2:待收货，3:已完成|  
|is_delete|int|删除状态，0:未删除，1:已删除|无|  
|is_comment|int|评价状态，0:未删除，1:已删除|无|  
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
                'number':'顶配',
                'car_type':'顶配',
                'specification':'顶配',
                'brand':'顶配',
                'sort':'顶配',
                'unit':'顶配',
                'production':'顶配',
                'category':'顶配',
                'car_type_list':'顶配',
                'detail_url':'/uashdjk/',
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|address_id|int|地址id|无|1|必填|  
|order_car_list|char(200)|购物车id列表|使用,拼接|1,2,3,4,5,6|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  

```
{
    'data':{
        'id':1
    }
}
```

<h4 id="service_order_get">查询订单信息</h4>

url:/api/service/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|自增|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单编号|无|  
|name|char(10)|收货人姓名|来源于所选地址|  
|phone|char(15)|联系电话|来源于所选地址|  
|city|char(50)|省市区|来源于所选地址|  
|address|char(100)|收货地址|来源于所选地址|  
|status|int|状态|0:待付款，1:待发货，2:待收货，3:已完成|  
|is_delete|int|删除状态，0:未删除，1:已删除|无|  
|is_comment|int|评价状态，0:未删除，1:已删除|无|  
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
                'number':'顶配',
                'car_type':'顶配',
                'specification':'顶配',
                'brand':'顶配',
                'sort':'顶配',
                'unit':'顶配',
                'production':'顶配',
                'category':'顶配',
                'car_type_list':'顶配',
                'detail_url':'/uashdjk/',
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

<h4 id="service_order_delete">删除订单信息</h4>

url:/api/service/order_delete/   
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="service_order_method_post">查询交易状态、付款、完成、评论订单信息</h4>

url:/api/service/order_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
|method|char(20)|操作|order_status:查询交易状态，pay:付款，finish：完成，comment:评论|pay|必填|  
|score|int|评分|大于等于0，小于等于5，当method为comment的时候需要|1|选填|  
|order_method|char(100)|支付方式|alipay：支付宝，weixin：微信|alipay|pay的时候必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|status|int|状态|order_status返回,0未支付，1正在支付，2支付成功，3支付失败重新支付，4支付超时|  
|time|int|交易还剩多少秒|order_status返回|  
|to|char(100)|商家的名字|order_status返回|  
|order_code|char(100)|交易订单号|order_status返回|  
|price|float|交易金额|order_status返回|  
|params|char(1000)|交易码|用于手机端交易|  

```
{
    'data':{
        'status':0,
        'time':0,
        'to':0,
        'order_code':'asdqwdqw',
        'price':12
    }
}
```

<h4 id="service_orderlogistics_get">查询订单快递信息</h4>

url:/api/service/orderlogistics/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|time|char(100)|时间|无|  
|status|char(100)|内容|无|  

```
{
    'data':[{
        'time':'2015-10-20 10:24:04',
        'status':'顺丰速运 已收取快件'
    }]
}
```

<h3 id="service_rules">违章记录信息</h3>

<h4 id="service_rules_list_get">查询违章记录列表信息</h4>

url:/api/service/rules/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|car_brand|char(100)|车辆品牌|无|  
|car_code|char(100)|车牌号|无|  
|car_pic_url|char(100)|车辆图片|无|  
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
        'car_code':'粤A23456',
        'car_pic_url':'/asdw.jpg',
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|car_brand|char(100)|车辆品牌|无|  
|car_code|char(100)|车牌号|无| 
|car_pic_url|char(100)|车辆图片|无|  
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
        'car_code':'粤A23456',
        'car_pic_url':'/asdw.jpg',
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|    
|news_catalog_id|int|分类id|无|0|选填|  

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
|detail_url|char(500)|详情页面url|无|  

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
        'is_bar':true,
        'detail_url':'www.ajskdh.com/asdasda/'
    }]
}
```

<h4 id="service_news_list_get">查询资讯列表信息</h4>

url:/api/service/news/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|news_catalog_id|int|分类id|无|0|选填|  

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
|detail_url|char(500)|详情页面url|无|  
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
        'is_bar':true,
        'detail_url':'www.ajskdh.com/asdasda/'
    }]
}
```

<h4 id="service_news_get">查询资讯信息</h4>

url:/api/service/news/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

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
|detail_url|char(500)|详情页面url|无|  
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
        'is_bar':true,
        'detail_url':'www.ajskdh.com/asdasda/'
    }
}
```

<h4 id="service_news_detail_get">查询资讯详情页面</h4>

url:/api/service/news_detail/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
```
{
}
```
return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
页面信息
```

<h2 id="maintain">维修厂</h2>

<h3 id="maintain_garage">汽修厂</h3>

<h4 id="maintain_garage_list_get">查询汽修厂列表信息</h4>

url:/api/maintain/garage/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|name|char(50)|汽修厂名称|无|天河|选填|    
|orderby|char(100)|排序规则|all、distance、popular|popular|必填|    
|longitude|float|经度|必填|23|必填|    
|latitude|float|纬度|必填|123|必填|    

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
|score|float|评分|无|  
|pic_url|char(50)|封面url|无|  
|distance|float|距离|单位：km|  
|type|int|类型：0既可以维修又可以保养，1只维修，2只保养|无|  

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
        'score':1,
        'pic_url':'asdla.jpg',
        'distance':10,
        'type':0
    }]
}
```

<h4 id="maintain_garage_get">查询汽修厂信息</h4>

url:/api/maintain/garage/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

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
|score|int|评分|无|  
|pic_url|char(50)|封面url|无|  
|distance|float|距离|单位：km|  
|type|int|类型：0既可以维修又可以保养，1只维修，2只保养|无|  

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
        'score':1,
        'pic_url':'asdla.jpg',
        'distance':10,
        'type':0
    }
}
```

<h3 id="maintain_oil">机油</h3>

<h4 id="maintain_oil_list_get">查询机油列表信息</h4>

url:/api/maintain/oil/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|garage_id|int|汽修厂id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|必填|  

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

```
流程：  
用户提交订单->维修厂接单（系统自动完成）->用户付款->维修厂点击开始保养->维修厂填写保养报告->维修厂点击保养结束->用户确认完成订单->用户评价  
等待接单：用户提交订单，等待维修厂接单。  
未支付：维修厂接单，用户付款后，结束此状态，进入下一个状态。  
等待服务：用户付款以后进入此状态，然后维修厂点击开始保养，需要填写取车时间，结束此状态，进入下一个状态。  
服务中：当is_upkeep=0，则表示保养未完成，维修厂可以填写保养报告。当维修厂点击保养结束，is_upkeep=1，表示保养完成，用户则可以选择完成订单，结束此状态，进入下一个状态。  
已完成：用户已经确认完成订单，订单结束，可以开始评价，is_comment表示是否评价了。  
```

<h4 id="maintain_upkeep_list_get">查询保养列表信息</h4>

url:/api/maintain/upkeep/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|必填|  

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
|filter_price|float|过滤格|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:等待接单（不会出现，系统自动接单）1:未支付，2:等待服务，3:服务中，4:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|is_upkeep|bool|维修状态|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|start_order_time|datetime|接单时间|无|  
|pay_time|datetime|付款时间|无|  
|get_time|datetime|取车时间|无|  
|service_time|datetime|服务时间|无|  
|upkeep_time|datetime|完成服务时间|无|  
|over_time|datetime|完成时间|无|   
|comment_time|datetime|评论时间|无|  
|deal_id|char(100)|交易单号|无|  
|order_id|char(100)|订单单号|无|  
|car_brand|char(100)|车辆品牌|无|  
|car_code|char(10)|车牌号码|无|  
|order_name|char(10)|订单名称|无|  
|service_item|char(10)|服务项目|无|  
|order_type|char(10)|订单类型|无|  
|project_material|char(500)|项目材料|无|  
|upkeeppic_set|list|汽修站提交的图片与附加信息对象数组|无|  
|upkeepoil_set|list|机油对象数组|无|  

upkeeppic_set：

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

upkeepoil_set：

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|oil_name|char(50)|机油名称|无|  
|oil_L|int|升|无|  
|oil_amount|int|数量|无|  
|oil_price|float|原价|无|  
|oil_new_price|float|特价|无|  

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
            'filter_price':88,
            'popular':1,
            'score':1,
            'pic_url':'asdla.jpg',
            'distance':10,
            'type':0
        },
        'name':'张三',
        'phone':'12345678998',
        'longitude':123,
        'latitude':23,
        'address':'广州市越秀区',
        'filter_price':1,
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'is_upkeep':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'start_order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'upkeep_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'deal_id':'182731725',
        'order_id':'8927918238271',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A24351',
        'order_name':'xxxx保养服务',
        'service_item':'保养',
        'order_type':'保养',
        'project_material':'xxxxxxxx',
        'upkeeppic_set':[{
            'pic_url':'/asdfas.jpg',
            'note':'车钥匙'
        }],
        'upkeepoil_set':[{
            'id':1,
            'oil_name':'没油',
            'oil_L':2,
            'oil_amount':2,
            'oil_price':1,
            'oil_new_price':1,
        }]
    }]
}
```

<h4 id="maintain_upkeep_list_post">生成保养订单信息</h4>

url:/api/maintain/upkeep/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|garage_id|int|汽修厂id|无|1|必填|  
|car_id|int|汽车id|无|1|必填|  
|name|char(20)|联系人|无|张三|必填|  
|phone|char(20)|电话号码|无|12345678909|必填|  
|longitude|float|经度|无|1|必填|  
|latitude|float|纬度|无|1|必填|  
|address|char(100)|地址|无|广州市越秀区|必填|  
|number|int|数量|多少个机油、机油数量|1|必填|  
|oil_id_list|char(100)|机油id集合，用,连接|无|1,2|必填|  
|oil_amount_list|char(1000)|数量集合，用,连接|无|1,2|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  

```
{
    'data':{
        'id':1
    }
}
```


<h4 id="maintain_upkeep_get">查询保养信息</h4>

url:/api/maintain/upkeep/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

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
|filter_price|float|过滤格|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:等待接单（不会出现，系统自动接单）1:未支付，2:等待服务，3:服务中，4:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|is_upkeep|bool|维修状态|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|start_order_time|datetime|接单时间|无|  
|pay_time|datetime|付款时间|无|  
|get_time|datetime|取车时间|无|  
|service_time|datetime|服务时间|无|  
|upkeep_time|datetime|完成服务时间|无|  
|over_time|datetime|完成时间|无|   
|comment_time|datetime|评论时间|无|  
|deal_id|char(100)|交易单号|无|  
|order_id|char(100)|订单单号|无|  
|car_brand|char(100)|车辆品牌|无|  
|car_code|char(10)|车牌号码|无|  
|order_name|char(10)|订单名称|无|  
|service_item|char(10)|服务项目|无|  
|order_type|char(10)|订单类型|无|  
|project_material|char(500)|项目材料|无|  
|upkeeppic_set|list|汽修站提交的图片与附加信息对象数组|无|  
|upkeepoil_set|list|机油对象数组|无|  

upkeeppic_set：

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

upkeepoil_set：

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|oil_name|char(50)|机油名称|无|  
|oil_L|int|升|无|  
|oil_amount|int|数量|无|  
|oil_price|float|原价|无|  
|oil_new_price|float|特价|无|  

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
            'filter_price':88,
            'popular':1,
            'score':1,
            'pic_url':'asdla.jpg',
            'distance':10,
            'type':0
        },
        'name':'张三',
        'phone':'12345678998',
        'longitude':123,
        'latitude':23,
        'address':'广州市越秀区',
        'filter_price':1,
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'is_upkeep':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'start_order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'upkeep_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'deal_id':'182731725',
        'order_id':'8927918238271',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A24351',
        'order_name':'xxxx保养服务',
        'service_item':'保养',
        'order_type':'保养',
        'project_material':'xxxxxxxx',
        'upkeeppic_set':[{
            'pic_url':'/asdfas.jpg',
            'note':'车钥匙'
        }],
        'upkeepoil_set':[{
            'id':1,
            'oil_name':'没油',
            'oil_L':2,
            'oil_amount':2,
            'oil_price':1,
            'oil_new_price':1,
        }]
    }]
}
```

<h4 id="maintain_upkeep_delete">删除保养订单信息</h4>

url:/api/maintain/upkeep_delete/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="maintain_upkeep_method_post">查询交易状态、付款、完成、评论保养订单信息</h4>

url:/api/maintain/upkeep_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
|method|char(20)|操作|order_status:查询交易状态，pay:付款，finish:完成，comment:评论|comment|必填|  
|score|int|评分|大于等于0，小于等于5，当method为comment的时候需要|1|选填|  
|order_method|char(100)|支付方式|alipay：支付宝，weixin：微信|alipay|pay的时候必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|status|int|状态|order_status返回,0未支付，1正在支付，2支付成功，3支付失败重新支付，4支付超时|  
|time|int|交易还剩多少秒|order_status返回|  
|to|char(100)|商家的名字|order_status返回|  
|order_code|char(100)|交易订单号|order_status返回|  
|price|float|交易金额|order_status返回|  
|params|char(1000)|交易码|用于手机端交易|  

```
{
    'data':{
        'status':0,
        'time':0,
        'to':0,
        'order_code':'asdqwdqw',
        'price':10
    }
}
```

<h4 id="maintain_upkeep_aftersales_list_get">查询保养售后列表信息</h4>

url:/api/maintain/upkeep_aftersales/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|order_id|char(100)|订单单号|无|  
|car_code|char(100)|车辆号码|无|  
|car_type|char(100)|车辆型号|无|  
|create_time|datetime|申请时间|无|  
|state|int|状态|0:服务中，1:已完成|  
|pic_list|list|图片对象列表|无|  

pic

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

```
{
    'data':[{
        'id':1,
        'order_id':'qwdqwd',
        'car_code':'wqdwq',
        'car_type':'asdqwdqw',
        'create_time':'2018-03-03 12:34:56',
        'state':0,
        'pic_list':[{
            'pic_url':'dqwd',
            'note':'dqwd'
        }]
    }]
}
```

<h4 id="maintain_upkeep_aftersales_list_post">生成保养售后订单信息</h4>

url:/api/maintain/upkeep_aftersales/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|content|text|内容|无|萨达|选填|  
|number|int|数量|多少个文件、备注，二者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{

    }
}
```

<h4 id="maintain_upkeep_aftersales_get">查询保养售后信息</h4>

url:/api/maintain/upkeep_aftersales/  
method:get   
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|order_id|char(100)|订单单号|无|  
|car_code|char(100)|车辆号码|无|  
|car_type|char(100)|车辆型号|无|  
|create_time|datetime|申请时间|无|  
|state|int|状态|0:服务中，1:已完成|  
|pic_list|list|图片对象列表|无|  

pic

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

```
{
    'data':[{
        'id':1,
        'order_id':'qwdqwd',
        'car_code':'wqdwq',
        'car_type':'asdqwdqw',
        'create_time':'2018-03-03 12:34:56',
        'state':0,
        'pic_list':[{
            'pic_url':'dqwd',
            'note':'dqwd'
        }]
    }]
}
```

<h4 id="maintain_upkeep_aftersales_method_post">完成保养售后订单信息</h4>

url:/api/maintain/upkeep_aftersales_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
|method|char(20)|操作|finish:完成|finish|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{
    }
}
```

<h3 id="maintain_maintain">维修</h3>

```
流程：  
用户提交订单->维修厂接单->维修厂设定维修项->用户付款->维修厂点击开始维修->维修厂填写维修报告->维修厂点击维修结束->用户确认完成订单->用户评价  
等待接单：用户提交订单，等待维修厂接单。  
未支付：is_settings=0，此时用户还不能付款。维修厂设置维修项后，用户方可付款并选择维修项，结束此状态，进入下一个状态。  
等待服务：用户付款以后进入此状态，然后维修厂点击开始维修，需要填写取车时间，结束此状态，进入下一个状态。  
服务中：当is_maintain=0，则表示维修未完成，维修厂可以填写维修报告。当维修厂点击维修结束，is_maintain=1，表示维修完成，用户则可以选择完成订单，结束此状态，进入下一个状态。  
已完成：用户已经确认完成订单，订单结束，可以开始评价，is_comment表示是否评价了。  
```

<h4 id="maintain_maintain_list_get">查询维修列表信息</h4>

url:/api/maintain/maintain/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|必填|  

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
|content|text|内容|无|  
|pic_url_list|list|图片列表|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:等待接单，1:未支付，2:等待服务，3:服务中，4:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|is_maintain|bool|维修状态|无|  
|is_setting|bool|是否设置维修清单|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|start_order_time|datetime|接单时间|无|  
|pay_time|datetime|付款时间|无|  
|get_time|datetime|取车时间|无|  
|service_time|datetime|服务时间|无|  
|maintain_time|datetime|完成服务时间|无|  
|over_time|datetime|完成时间|无|  
|comment_time|datetime|评论时间|无|  
|car_code|char(10)|车牌|无|  
|car_type|char(100)|车型|无|  
|deal_id|char(10)|交易单号|无|  
|order_id|char(10)|订单单号|无|  
|order_name|char(10)|订单名称|无|  
|service_item|char(10)|服务项目|无|  
|order_type|char(10)|订单类型|无|  
|project_material|char(500)|项目材料|无|  
|maintainpic_set|list|汽修站提交的图片与附加信息对象数组|无|  
|maintainitem_set|list|汽修站给出的维修项信息对象数组|无|  
|maintainitem_set_now|list|用户选择的维修项信息对象数组|无|  

maintainpic_set:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

maintainitem_set

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|name|char(100)|图片url|无|  
|price|char(100)|备注|无|  

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
            'filter_price':88,
            'popular':1,
            'score':1,
            'pic_url':'asdla.jpg',
            'distance':10,
            'type':0
        },
        'name':'张三',
        'phone':'粤A23452',
        'longitude':'玛萨拉蒂',
        'latitude':'广州市越秀区',
        'address':'12345678998',
        'car_type':'12345678998',
        'content':'修理',
        'pic_url_list':['/asda.jpg'],
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'is_maintain':false,
        'is_setting':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'start_order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'maintain_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'car_code':'粤A88888',
        'deal_id':'182731725',
        'order_id':'8927918238271',
        'order_name':'xxxx维修服务',
        'service_item':'维修',
        'order_type':'维修',
        'project_material':'xxxxxxxx',
        'maintainpic_set':[{
            'pic_url':'/asdfas.jpg',
            'note':'车钥匙'
        }],
        'maintainpic_set':[{
            'id':12,
            'name':'车轮',
            'price':123
        }],
        'maintainitem_set_now':[{
            'id':12,
            'name':'车轮',
            'price':123
        }]
    }]
}
```

<h4 id="maintain_maintain_list_post">生成维修订单信息</h4>

url:/api/maintain/maintain/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|garage_id|int|汽修厂id|无|1|必填|  
|car_id|int|汽车id|无|1|必填|  
|name|char(20)|名称|无|张三|必填|  
|phone|char(20)|电话号码|无|12345678998|必填|  
|longitude|float|经度|无|104|必填|  
|latitude|float|纬度|无|23|必填|  
|address|char(100)|地址|无|广州天河区|必填|  
|content|text|内容|无|修理|必填|  
|number|int|数量|多少个文件|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  

```
{
    'data':{
        'id':1
    }
}
```


<h4 id="maintain_maintain_get">查询维修信息</h4>

url:/api/maintain/maintain/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

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
|content|text|内容|无|  
|pic_url_list|list|图片列表|无|  
|price|float|价格|无|  
|discounts|float|优惠卷|无|  
|now_price|float|实付款|无|  
|state|int|状态|0:等待接单，1:未支付，2:等待服务，3:服务中，4:已完成|  
|is_delete|bool|删除状态|无|  
|is_comment|bool|评论状态|无|  
|is_maintain|bool|维修状态|无|  
|is_setting|bool|是否设置维修清单|无|  
|score|int|评分|大于等于0，小于等于5|  
|order_time|datetime|下单时间|无|  
|start_order_time|datetime|接单时间|无|  
|pay_time|datetime|付款时间|无|  
|get_time|datetime|取车时间|无|  
|service_time|datetime|服务时间|无|  
|maintain_time|datetime|完成服务时间|无|  
|over_time|datetime|完成时间|无|  
|comment_time|datetime|评论时间|无|  
|car_code|char(10)|车牌|无|  
|car_type|char(100)|车型|无|  
|deal_id|char(10)|交易单号|无|  
|order_id|char(10)|订单单号|无|  
|order_name|char(10)|订单名称|无|  
|service_item|char(10)|服务项目|无|  
|order_type|char(10)|订单类型|无|  
|project_material|char(500)|项目材料|无|  
|maintainpic_set|list|汽修站提交的图片与附加信息对象数组|无|  
|maintainitem_set|list|汽修站给出的维修项信息对象数组|无|  
|maintainitem_set_now|list|用户选择的维修项信息对象数组|无|  

maintainpic_set:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

maintainitem_set

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|name|char(100)|图片url|无|  
|price|char(100)|备注|无|  

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
            'filter_price':88,
            'popular':1,
            'score':1,
            'pic_url':'asdla.jpg',
            'distance':10,
            'type':0
        },
        'name':'张三',
        'phone':'粤A23452',
        'longitude':'玛萨拉蒂',
        'latitude':'广州市越秀区',
        'address':'12345678998',
        'car_type':'12345678998',
        'content':'修理',
        'pic_url_list':['/asda.jpg'],
        'price':1,
        'discounts':1,
        'now_price':1,
        'state':1,
        'is_delete':true,
        'is_comment':false,
        'is_maintain':false,
        'is_setting':false,
        'score':1,
        'order_time':'2018-07-08 12:23:34',
        'start_order_time':'2018-07-08 12:23:34',
        'pay_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'service_time':'2018-07-08 12:23:34',
        'maintain_time':'2018-07-08 12:23:34',
        'over_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'car_code':'粤A88888',
        'deal_id':'182731725',
        'order_id':'8927918238271',
        'order_name':'xxxx维修服务',
        'service_item':'维修',
        'order_type':'维修',
        'project_material':'xxxxxxxx',
        'maintainpic_set':[{
            'pic_url':'/asdfas.jpg',
            'note':'车钥匙'
        }],
        'maintainpic_set':[{
            'id':12,
            'name':'车轮',
            'price':123
        }],
        'maintainitem_set_now':[{
            'id':12,
            'name':'车轮',
            'price':123
        }]
    }
}
```

<h4 id="maintain_maintain_delete">删除维修订单信息</h4>

url:/api/maintain/maintain_delete/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
```
{
    'data':{}
}
```

<h4 id="maintain_maintain_method_post">查询交易状态、修改维修项、付款、完成、评论维修订单信息</h4>

url:/api/maintain/maintain_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
|method|char(20)|操作|order_status:查询交易状态，item_list：修改维修项，pay:付款，finish:完成，comment:评论|comment|必填|  
|score|int|评分|大于等于0，小于等于5，当method微comment的时候需要|1|选填|  
|order_method|char(100)|支付方式|alipay：支付宝，weixin：微信|alipay|pay的时候必填|  
|item_list|char(100)|维修项列表字符串|用,拼接|1,2,3,4|item_list的时候必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|status|int|状态|order_status返回,0未支付，1正在支付，2支付成功，3支付失败重新支付，4支付超时|  
|time|int|交易还剩多少秒|order_status返回|  
|to|char(100)|商家的名字|order_status返回|  
|order_code|char(100)|交易订单号|order_status返回|  
|price|float|交易金额|order_status返回|  
|params|char(1000)|交易码|用于手机端交易|  

```
{
    'data':{
        'status':0,
        'time':0,
        'to':0,
        'order_code':'asdqwdqw',
        'price':10
    }
}
```


<h4 id="maintain_maintain_aftersales_list_get">查询维修售后列表信息</h4>

url:/api/maintain/maintain_aftersales/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|order_id|char(100)|订单单号|无|  
|car_code|char(100)|车辆号码|无|  
|car_type|char(100)|车辆型号|无|  
|create_time|datetime|申请时间|无|  
|state|int|状态|0:服务中，1:已完成|  
|pic_list|list|图片对象列表|无|  

pic:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

```
{
    'data':[{
        'id':1,
        'order_id':'qwdqwd',
        'car_code':'wqdwq',
        'car_type':'asdqwdqw',
        'create_time':'2018-03-03 12:34:56',
        'state':0,
        'pic_list':[{
            'pic_url':'dqwd',
            'note':'dqwd'
        }]
    }]
}
```

<h4 id="maintain_maintain_aftersales_list_post">生成维修售后订单信息</h4>

url:/api/maintain/maintain_aftersales/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|content|text|内容|无|萨达|选填|  
|number|int|数量|多少个文件、备注，二者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{

    }
}
```

<h4 id="maintain_maintain_aftersales_get">查询维修售后信息</h4>

url:/api/maintain/maintain_aftersales/  
method:get   
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|order_id|char(100)|订单单号|无|  
|car_code|char(100)|车辆号码|无|  
|car_type|char(100)|车辆型号|无|  
|create_time|datetime|申请时间|无|  
|state|int|状态|0:服务中，1:已完成|  
|pic_list|list|图片对象列表|无|  

pic:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

```
{
    'data':[{
        'id':1,
        'order_id':'qwdqwd',
        'car_code':'wqdwq',
        'car_type':'asdqwdqw',
        'create_time':'2018-03-03 12:34:56',
        'state':0,
        'pic_list':[{
            'pic_url':'dqwd',
            'note':'dqwd'
        }]
    }]
}
```

<h4 id="maintain_maintain_aftersales_method_post">完成维修售后订单信息</h4>

url:/api/maintain/maintain_aftersales_method/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
|method|char(20)|操作|finish:完成|finish|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{
    }
}
```

<h4 id="maintain_maintain_jpush_order_get">极光推送维修订单接单信息</h4>

手机端设置：登陆以后，把账号注册成别名，服务端面向别名发送信息

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|type|char(100)|类型|maintain_order|  
|data|objects|额外数据|无|  
|id|int|维修订单id|如果接单，则是订单id，反之为0|  
|state|bool|是否接单|无|  
|msg|char(100)|信息|无|  

```
{
    'data':{
        'type':'maintain_order',
        'data':{
            'id':0,
            'state':false,
            'msg':'失败'
        }
    }
}
```

<h4 id="maintain_maintain_jpush_item_get">极光推送维修订单下发清单信息</h4>

手机端设置：登陆以后，把账号注册成别名，服务端面向别名发送信息

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|type|char(100)|类型|maintain_item|  
|data|objects|额外数据|无|  
|id|int|维修订单id|无|  
|msg|char(100)|信息|无|  

```
{
    'data':{
        'type':'maintain_item',
        'data':{
            'id':0,
            'msg':'失败'
        }
    }
}
```

<h4 id="maintain_maintain_jpush_finish_get">极光推送维修订单完成信息</h4>

手机端设置：登陆以后，把账号注册成别名，服务端面向别名发送信息

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|type|char(100)|类型|maintain_finish|  
|data|objects|额外数据|无|  
|id|int|维修订单id|无|  
|msg|char(100)|信息|无|  

```
{
    'data':{
        'type':'maintain_finish',
        'data':{
            'id':0,
            'msg':'失败'
        }
    }
}
```

<h3 id="maintain_list_get">保养、维修订单列表信息</h3>

url:/api/maintain/list/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|state|int|状态|-1:全部，0:等待接单，1:未支付，2:等待服务，3:服务中，4:已完成|1|必填|  
|is_comment|bool|是否评论|无|true|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|维修 or 保养id|区分需要依靠type|  
|order_name|char(100)|订单名称|无|  
|order_pic_url|char(100)|图片url|无|  
|type|char(50)|类型|upkeep:保养，maintain:维修|  
|create_time|datetime|创建时间|无|  
|now_price|float|价格|无|  
|state|int|状态|0:等待接单，1:未支付，2:等待服务，3:服务中，4:已完成|  
|is_comment|bool|是否评论|无|  
|is_setting|bool|是否已经设置了维修项|维修才有|  
|is_maintain|bool|汽修厂是否完成维修|维修才有|  
|is_upkeep|bool|汽修厂是否完成半阳|保养才有|  
|garage|object|汽修厂|查询汽修厂信息|  

```
{
    'data':
    [{
        'id':1,
        'order_name':'张三年检站维修服务',
        'order_pic_url':'www.asd.cn/dqwd.jpg',
        'type':'upkeep',
        'create_time':'2018-07-08 12:23:34',
        'now_price':1,
        'state':1,
        'is_comment':true,
        'is_setting':true,
        'is_maintain':true,
        'is_upkeep':true,
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
            'filter_price':88,
            'popular':1,
            'score':1,
            'pic_url':'asdla.jpg',
            'distance':10,
            'type':0
        }
    }]
}
```

<h3 id="maintain_aftersales_list_get">保养、维修售后列表信息</h3>

url:/api/maintain/aftersales_list/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|state|int|状态|-1:全部，0:未完成，1:已完成|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|维修售后 or 保养守候id|区分需要依靠type|  
|order_id|char(100)|订单单号|无|  
|car_code|char(100)|车辆号码|无|  
|car_type|char(100)|车辆型号|无|  
|type|char(50)|类型|upkeep:保养，maintain:维修|  
|create_time|datetime|申请时间|无|  
|state|int|状态|0:服务中，1:已完成|  
```
{
    'data':
    [{
        'id':1,
        'order_name':'张三年检站维修服务',
        'order_pic_url':'www.asd.cn/dqwd.jpg',
        'type':'upkeep',
        'create_time':'2018-07-08 12:23:34',
        'now_price':1,
        'state':1,
        'is_comment':true,
        'is_setting':true,
        'is_maintain':true,
        'is_upkeep':true,
    }]
}
```


<h2 id="survey">年检</h2>

<h3 id="survey_surveystation">年检站信息</h3>

<h4 id="survey_surveystation_list_get">查询年检站列表信息</h4>

url:/api/survey/surveystation/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|detail|char(100)|套餐详情|无|  
|is_failure|bool|是否可以失败|无|  
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
        'is_failure':true,
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|名称|无|  
|detail|char(100)|套餐详情|无|  
|is_failure|bool|是否可以失败|无|  
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
        'is_failure':true,
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

```
流程：  
代驾：用户提交订单->用户付款，等待抢单->司机抢单->司机确认取车->司机开始年检，随后司机输入年检结果，如果年检成功才会跳进下一个状态(survey_state:四种状态，0:还没有开始或是正在进行，1：成功，2：不成功，3：复查)->年检成功->司机确认到达->司机确认还车->用户确认完成  
自驾：用户提交订单->用户付款->自行开车过去，点击开始年检->年检完成，点击确认完成订单  

详情：0:等待支付，1:等待接单  
代驾取车：2:等待取车  
开始年检：3.等待年检，4.正在年检，5.年检成功  
检完还车：6.到达还车，7.已还车，8.已完成  
代驾：0-1-2-3-4-5-6-7-8  
自驾：0-3-8  

用户取消订单：
 - 代驾方面，“等待支付”、“等待接单”、“等待取车”阶段可以取消订单，“等待支付”时取消订单将被删除，“等待接单”、“等待取车”时取消订单将变成已退款状态，“等待取车”存在超时扣钱情况。
 - 自驾方面，“等待支付”、“等待年检”阶段可以取消订单，“等待支付”时取消订单将被删除，“等待年检”时取消订单将变成已退款状态，“等待年检”存在超时扣钱情况  
司机取消订单：“等待取车”阶段可以取消订单，订单将回到“等待接单”，“等待接单”存在超时扣钱情况
```

<h4 id="survey_survey_list_get">查询年检订单列表信息</h4>

url:/api/survey/survey/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单id|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|char(100)|车量类型|小型蓝牌，七座以下|  
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
|state|int|状态|0.等待支付，1.等待接单，2.等待取车，3.等待年检，4.正在年检，5.年检成功，6.到达还车，7.已还车，8.已完成|  
|survey_state|int|年检状态|0:还没有开始或是正在进行，1：成功，2：不成功，3：复查|  
|is_comment|bool|是否评论|无|  
|is_feedback|bool|是否投诉|无|  
|drive_user_id|int|接单用户id|无|  
|drive_user_pic_url|char(100)|接单用户头像url|无|  
|drive_user_name|char(100)|接单用户名称|无|  
|drive_user_phone|char(100)|接单用户联系电话|无|  
|drive_user_score|int|司机评分|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|comment_time|datetime|评论时间|无|  
|get_info|object|取车图片-证件照片|无|  
|get_confirm|object|取车图片-车损照片|无|  
|get_car|object|取车图片-车身拍照|无|  
|survey_upload|object|年检已过-上传照片|无|  
|survey_fail_upload|object|年检未过-上传照片|无|  
|return_info|object|还车图片-证件照片|无|  
|return_confirm|object|还车图片-车损照片|无|  
|return_car|object|还车图片-车身拍照|无|  
|failure_list|list|失败信息对象列表|无|  



get_info、get_confirm、get_car、survey_upload、survey_fail_upload、return_info、return_confirm、return_car:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|类别名称|无|  
|obj_list|list|列表|无|  

obj:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

failure_list：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|补充项|无|  
|price|float|总计费用|无|  
|failureitem_list|list|失败详情|无|  

failureitem：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|名称|无|  
|price|float|费用|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'123413131',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':'小型蓝牌',
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
        'survey_state':0,
        'is_comment':0,
        'is_feedback':true,
        'drive_user_id':1,
        'drive_user_pic_url':'http://www.adsa.cn/sjdk.jpg',
        'drive_user_name':'李四',
        'drive_user_phone':'12312',
        'drive_user_score':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'get_info':{
            'name':'取车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_confirm':{
            'name':'取车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_car':{
            'name':'取车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_upload':{
            'name':'年检已过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_fail_upload':{
            'name':'年检未过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_info':{
            'name':'还车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_confirm':{
            'name':'还车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_car':{
            'name':'还车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'failure_list':[{
            'name':'补充项',
            'price':123,
            'failureitem_list':[{
                'name':'名称',
                'price':'费用'
            }]
        }]
    }]
}
```

<h4 id="survey_survey_list_post">提交年检订单信息</h4>

url:/api/survey/survey/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|name|char(20)|联系人|无|张三|必填|  
|phone|char(20)|联系人电话|无|12345678998|必填|  
|car_name|char(20)|车主姓名|无|张三|必填|  
|car_brand|char(20)|品牌型号|无|玛萨拉蒂|必填|  
|car_code|char(20)|车牌|无|粤A23452|必填|  
|car_type|char(100)|车量类型|小型蓝牌，七座以下|必填|  
|surveystation_id|int|年检站id|无|1|必填|  
|order_longitude|float|交接地点经度|无|233|必填|  
|order_latitude|float|交接地点纬度|无|322|必填|  
|order_address|char(100)|交接地点|无|广州白云区|必填|  
|subscribe_time|datetime|预约日期|13点前表示上午，13点后表示下午|2018-07-08 12:23:34|必填|  
|is_self|bool|是否自驾|无|false|必填|  
|combo_id|int|套餐id|无|1|必填|  
|comboitem_list|char(100)|套餐选项id|使用,拼接|1,2|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  

```
{
    'data':{
        'id':1
    }
}
```


<h4 id="survey_survey_get">查询年检订单信息</h4>

url:/api/survey/survey/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单id|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|char(100)|车量类型|小型蓝牌，七座以下|  
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
|state|int|状态|0.等待支付，1.等待接单，2.等待取车，3.等待年检，4.正在年检，5.年检成功，6.到达还车，7.已还车，8.已完成|  
|survey_state|int|年检状态|0:还没有开始或是正在进行，1：成功，2：不成功，3：复查|  
|is_comment|bool|是否评论|无|  
|is_feedback|bool|是否投诉|无|  
|drive_user_id|int|接单用户id|无|  
|drive_user_pic_url|char(100)|接单用户头像url|无|  
|drive_user_name|char(100)|接单用户名称|无|  
|drive_user_phone|char(100)|接单用户联系电话|无|  
|drive_user_score|int|司机评分|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|comment_time|datetime|评论时间|无|  
|get_info|object|取车图片-证件照片|无|  
|get_confirm|object|取车图片-车损照片|无|  
|get_car|object|取车图片-车身拍照|无|  
|survey_upload|object|年检已过-上传照片|无|  
|survey_fail_upload|object|年检未过-上传照片|无|  
|return_info|object|还车图片-证件照片|无|  
|return_confirm|object|还车图片-车损照片|无|  
|return_car|object|还车图片-车身拍照|无|  
|failure_list|list|失败信息对象列表|无|  



get_info、get_confirm、get_car、survey_upload、survey_fail_upload、return_info、return_confirm、return_car:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|类别名称|无|  
|obj_list|list|列表|无|  

obj:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

failure_list：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|补充项|无|  
|price|float|总计费用|无|  
|failureitem_list|list|失败详情|无|  

failureitem：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|名称|无|  
|price|float|费用|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'123413131',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':'小型蓝牌',
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
        'survey_state':0,
        'is_comment':0,
        'is_feedback':true,
        'drive_user_id':1,
        'drive_user_pic_url':'http://www.adsa.cn/sjdk.jpg',
        'drive_user_name':'李四',
        'drive_user_phone':'12312',
        'drive_user_score':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'get_info':{
            'name':'取车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_confirm':{
            'name':'取车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_car':{
            'name':'取车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_upload':{
            'name':'年检已过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_fail_upload':{
            'name':'年检未过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_info':{
            'name':'还车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_confirm':{
            'name':'还车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_car':{
            'name':'还车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'failure_list':[{
            'name':'补充项',
            'price':123,
            'failureitem_list':[{
                'name':'名称',
                'price':'费用'
            }]
        }]
    }]
}
```

<h4 id="survey_survey_selfmethod_post">自驾年检订单操作信息-查询交易状态、取消、查询费用、支付、确认到达(完成订单)</h4>

url:/api/survey/survey_selfmethod/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|查询费用不需要添加id|1|必填|   
|method|char(20)|操作|order_status:查询交易状态，cancel：取消，get：查询费用，pay：支付，survey：确认到达|get|必填|  
|longitude|float|经度|无|123|选填|  
|latitude|float|纬度|无|23|选填|  
|surveystation_id|int|年检站id|无|1|选填|  
|combo_id|int|套餐id|无|1|选填|  
|comboitem_list|char(100)|套餐选项id|使用,拼接|1,2|选填|  
|order_method|char(100)|支付方式|alipay：支付宝，weixin：微信|alipay|pay的时候必填|  

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
|status|int|状态|order_status返回,0未支付，1正在支付，2支付成功，3支付失败重新支付，4支付超时|  
|time|int|交易还剩多少秒|order_status返回|  
|to|char(100)|商家的名字|order_status返回|  
|order_code|char(100)|交易订单号|order_status返回|  
|price|float|交易金额|order_status返回|  
|params|char(1000)|交易码|用于手机端交易|  

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

<h4 id="survey_survey_behalfmethod_post">代驾年检订单操作信息-查询交易状态、取消、查询费用、支付、查询失败支付交易状态、失败支付、确认还车、评分</h4>

url:/api/survey/survey_behalfmethod/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|查询费用不需要添加id|1|必填|   
|method|char(20)|操作|order_status:查询交易状态，cancel：取消，get：查询费用，pay：支付，order_status：查询失败支付交易状态，pay：失败支付，return：确认还车，comment：评分|get|必填|  
|longitude|float|经度|无|123|选填|  
|latitude|float|纬度|无|23|选填|  
|surveystation_id|int|年检站id|无|1|选填|  
|combo_id|int|套餐id|无|1|选填|  
|comboitem_list|char(100)|套餐选项id|使用,拼接|1,2|选填|  
|order_method|char(100)|支付方式|alipay：支付宝，weixin：微信|alipay|pay的时候必填|  
|score|int|评分|大于等于0，小于等于5|1|当method为comment的时候必填|  

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
|status|int|状态|order_status返回,0未支付，1正在支付，2支付成功，3支付失败重新支付，4支付超时|  
|time|int|交易还剩多少秒|order_status返回|  
|to|char(100)|商家的名字|order_status返回|  
|order_code|char(100)|交易订单号|order_status返回|  
|price|float|交易金额|order_status返回|  
|params|char(1000)|交易码|用于手机端交易|  

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

<h4 id="survey_survey_feedback_post">年检投诉</h4>

url:/api/survey/survey_feedback/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|id|1|必填|   
|number|int|数量|多少个文件、备注，二者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  
|note1|char(100)|备注|无|车钥匙|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|   

```
{
    'data':{
    }
}
```

<h4 id="survey_survey_phone_get">自驾咨询电话</h4>

url:/api/survey/survey_phone/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

|参数|类型|说明|备注|  
|---|---|---|---|  
|phone|char(100)|固定电话|无|  
|moblie_phone|char(100)|手机号码|无|  

```
{
    'data':{
        'phone':'12331',
        'moblie_phone':'12331'
    }
}
```

<h4 id="survey_survey_info_get">年检须知</h4>

url:/api/survey/survey_info/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|url|char(100)|页面url|无|  

```
{
    'data':{
        'url':'http://www.nolasthope.cn/survey/surveyinfo/'
    }
}
```

<h4 id="survey_survey_usercancelinfo_get">用户扣费标准</h4>

url:/api/survey/survey_usercancelinfo/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|url|char(100)|页面url|无|  

```
{
    'data':{
        'url':'http://www.nolasthope.cn/survey/surveyusercancelinfo/'
    }
}
```

<h4 id="survey_survey_jpush_grab_get">极光推送年检订单接单信息</h4>

手机端设置：登陆以后，把账号注册成别名，服务端面向别名发送信息

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|type|char(100)|类型|survey_grab|  
|data|objects|额外数据|无|  
|id|int|年检订单id|无|  
|msg|char(100)|信息|无|  

```
{
    'data':{
        'type':'survey_grab',
        'data':{
            'id':0,
            'msg':'失败'
        }
    }
}
```

<h2 id="system">系统</h2>

<h3 id="system_serviceimg_get">服务首页图片信息</h3>

url:/api/system/serviceimg/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

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

<h3 id="system_cover_get">封面图片信息</h3>

url:/api/system/cover/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   
|system|char(50)|系统|android,ios|ios|选填|  
|app_type|char(50)|用户端类型|user,driver|user|选填|  
|version|char(50)|版本|xx.yyzz|1.0000|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|update_time|datetime|修改时间|无|  
|pic_url_list|list|图片路径|无|  

```
{
    'data':{
        'update_time':'2018-07-08 12:23:34',
        'pic_url_list':[
            'alshajfsd/sadf.jpg',
            'alshajfsd/sadf.jpg',
            'alshajfsd/sadf.jpg'
        ]
    }
}
```

<h3 id="system_aboutus_get">关于我们</h3>

url:/api/system/aboutus/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|url|char(100)|页面url|无|  

```
{
    'data':{
        'url':'http://www.nolasthope.cn/system/aboutus/'
    }
}
```

<h3 id="system_useragreement_get">注册用户协议</h3>

url:/api/system/useragreement/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|url|char(100)|页面url|无|  

```
{
    'data':{
        'url':'http://www.nolasthope.cn/system/useragreement/'
    }
}
```

<h2 id="driver">司机端</h2>

<h3 id="driver_order">订单</h3>

<h4 id="driver_order_list_get">查询订单列表信息</h4>

url:/api/driver/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|type|char(100)|类型|order：可以接的单，driver：已接订单|必填|  
|finish|int|是否完成|0表示所有，1表示未完成，2表示已完成|1|当type=driver的时候必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单id|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|char(100)|车量类型|小型蓝牌，七座以下|  
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
|state|int|状态|0.等待支付，1.等待接单，2.等待取车，3.等待年检，4.正在年检，5.年检成功，6.到达还车，7.已还车，8.已完成|  
|survey_state|int|年检状态|0:还没有开始或是正在进行，1：成功，2：不成功，3：复查|  
|is_comment|bool|是否评论|无|  
|is_feedback|bool|是否投诉|无|  
|drive_user_id|int|接单用户id|无|  
|drive_user_pic_url|char(100)|接单用户头像url|无|  
|drive_user_name|char(100)|接单用户名称|无|  
|drive_user_phone|char(100)|接单用户联系电话|无|  
|drive_user_score|int|司机评分|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|comment_time|datetime|评论时间|无|  
|get_info|object|取车图片-证件照片|无|  
|get_confirm|object|取车图片-车损照片|无|  
|get_car|object|取车图片-车身拍照|无|  
|survey_upload|object|年检已过-上传照片|无|  
|survey_fail_upload|object|年检未过-上传照片|无|  
|return_info|object|还车图片-证件照片|无|  
|return_confirm|object|还车图片-车损照片|无|  
|return_car|object|还车图片-车身拍照|无|  
|failure_list|list|失败信息对象列表|无|  



get_info、get_confirm、get_car、survey_upload、survey_fail_upload、return_info、return_confirm、return_car:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|类别名称|无|  
|obj_list|list|列表|无|  

obj:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

failure_list:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|补充项|无|  
|price|float|总计费用|无|  
|failureitem_list|list|失败详情|无|  ：
failureitem：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|名称|无|  
|price|float|费用|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'123413131',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':'小型蓝牌',
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
        'survey_state':0,
        'is_comment':0,
        'is_feedback':true,
        'drive_user_id':1,
        'drive_user_pic_url':'http://www.adsa.cn/sjdk.jpg',
        'drive_user_name':'李四',
        'drive_user_phone':'12312',
        'drive_user_score':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'get_info':{
            'name':'取车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_confirm':{
            'name':'取车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_car':{
            'name':'取车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_upload':{
            'name':'年检已过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_fail_upload':{
            'name':'年检未过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_info':{
            'name':'还车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_confirm':{
            'name':'还车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_car':{
            'name':'还车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'failure_list':[{
            'name':'补充项',
            'price':123,
            'failureitem_list':[{
                'name':'名称',
                'price':'费用'
            }]
        }]
    }]
}
```

<h4 id="driver_order_get">查询订单信息</h4>

url:/api/driver/order/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   
 

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单id|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|char(100)|车量类型|小型蓝牌，七座以下|  
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
|state|int|状态|0.等待支付，1.等待接单，2.等待取车，3.等待年检，4.正在年检，5.年检成功，6.到达还车，7.已还车，8.已完成|  
|survey_state|int|年检状态|0:还没有开始或是正在进行，1：成功，2：不成功，3：复查|  
|is_comment|bool|是否评论|无|  
|is_feedback|bool|是否投诉|无|  
|drive_user_id|int|接单用户id|无|  
|drive_user_pic_url|char(100)|接单用户头像url|无|  
|drive_user_name|char(100)|接单用户名称|无|  
|drive_user_phone|char(100)|接单用户联系电话|无|  
|drive_user_score|int|司机评分|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|comment_time|datetime|评论时间|无|  
|get_info|object|取车图片-证件照片|无|  
|get_confirm|object|取车图片-车损照片|无|  
|get_car|object|取车图片-车身拍照|无|  
|survey_upload|object|年检已过-上传照片|无|  
|survey_fail_upload|object|年检未过-上传照片|无|  
|return_info|object|还车图片-证件照片|无|  
|return_confirm|object|还车图片-车损照片|无|  
|return_car|object|还车图片-车身拍照|无|  
|failure_list|list|失败信息对象列表|无|  



get_info、get_confirm、get_car、survey_upload、survey_fail_upload、return_info、return_confirm、return_car:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|类别名称|无|  
|obj_list|list|列表|无|  

obj:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

failure_list：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|补充项|无|  
|price|float|总计费用|无|  
|failureitem_list|list|失败详情|无|  

failureitem：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|名称|无|  
|price|float|费用|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'123413131',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':'小型蓝牌',
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
        'survey_state':0,
        'is_comment':0,
        'is_feedback':true,
        'drive_user_id':1,
        'drive_user_pic_url':'http://www.adsa.cn/sjdk.jpg',
        'drive_user_name':'李四',
        'drive_user_phone':'12312',
        'drive_user_score':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'get_info':{
            'name':'取车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_confirm':{
            'name':'取车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_car':{
            'name':'取车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_upload':{
            'name':'年检已过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_fail_upload':{
            'name':'年检未过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_info':{
            'name':'还车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_confirm':{
            'name':'还车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_car':{
            'name':'还车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'failure_list':[{
            'name':'补充项',
            'price':123,
            'failureitem_list':[{
                'name':'名称',
                'price':'费用'
            }]
        }]
    }]
}
```

<h4 id="driver_order_picname_get">查询提交图片的类别名称信息</h4>

url:/api/driver/picname/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|get_confirm|char(50)|取车图片-车损照片|无|  
|get_car|char(50)|取车图片-车身拍照|无|  
|survey_upload|char(50)|年检已过-上传照片|无|  
|survey_fail_upload|char(50)|年检未过-上传照片|无|  
|return_confirm|char(50)|还车图片-车损照片|无|  
|return_car|char(50)|还车图片-车身拍照|无|  

```
{
    'data':{
        'get_confirm':'取车图片-车损照片',
        'get_car':'取车图片-车身拍照',
        'survey_upload':'年检已过-上传照片',
        'survey_fail_upload':'年检未过-上传照片',
        'return_confirm':'还车图片-车损照片',
        'return_car':'还车图片-车身拍照'
    }
}
```

<h4 id="driver_order_surveyitem_get">查询年检检查项信息</h4>

url:/api/driver/surveyitem/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|name|char(50)|项目名称|无|  
|price|float|费用|无|  

```
{
    'data':[{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'name':'车身',
        'price':122
    }]
}
```

<h4 id="driver_order_grab_post">抢单</h4>

url:/api/driver/order_grab/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_cancel_post">取消订单</h4>

url:/api/driver/order_cancel/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|number|int|数量|多少个文件、类型、备注，三者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  
|type1|char(100)|类型|get_info:取车图片-证件照片,get_confirm:取车图片-车损照片,get_car:取车图片-车身拍照|get_confirm|选填|  
|note1|char(100)|备注|无|车钥匙|选填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|number|int|数量|多少个文件、类型、备注，三者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  
|type1|char(100)|类型|survey_upload:年检已过-上传照片|survey_upload|选填|  
|note1|char(100)|备注|无|车钥匙|选填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|number|int|数量|多少个文件、类型、备注，三者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  
|type1|char(100)|类型|survey_fail_upload:年检未过-上传照片|survey_fail_upload|选填|  
|note1|char(100)|备注|无|车钥匙|选填|  
|number_item|int|数量|多少个检查项id、价格，二者需要一同出现，缺少其一则会被认为没有|1|必填| 
|item_id1|int|检查项id|来自于年检检查项|1|选填|  
|price1|float|检查项费用|用户自选|12|选填|  


return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_order_arrive_post">到达还车</h4>

url:/api/driver/order_arrive/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  

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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|  
|number|int|数量|多少个文件、类型、备注，三者需要一同出现，缺少其一则会被认为没有|1|必填|  
|pic1|文件流|图片|编号从1开始|(文件流)|选填|  
|type1|char(100)|类型|return_info:还车图片-证件照片,return_confirm:还车图片-车损照片,return_car:还车图片-车身拍照|return_confirm|选填|  
|note1|char(100)|备注|无|车钥匙|选填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="ws_driver_order">查询订单列表信息-服务端推送</h4>

使用websocket连接  
url:/ws/driver/order/<:user_id>/<:timestampe>/<:sign>/  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|user_id|int|用户id|登陆成功后返回|1|必填|  
|timestamp|char(50)|时间戳|app自己生成|1|必填|  
|sign|char(50)|签名|md5(token+timestamp)|asdadsa|必填|  
|longitude|float|经度|必填|23|必填|    
|latitude|float|纬度|必填|123|必填|    

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_code|char(100)|订单id|无|  
|name|char(20)|联系人|无|  
|phone|char(20)|联系人电话|无|   
|car_name|char(20)|车主姓名|无|  
|car_brand|char(20)|品牌型号|无|  
|car_code|char(20)|车牌|无|  
|car_type|char(100)|车量类型|小型蓝牌，七座以下|  
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
|state|int|状态|0.等待支付，1.等待接单，2.等待取车，3.等待年检，4.正在年检，5.年检成功，6.到达还车，7.已还车，8.已完成|  
|survey_state|int|年检状态|0:还没有开始或是正在进行，1：成功，2：不成功，3：复查|  
|is_comment|bool|是否评论|无|  
|is_feedback|bool|是否投诉|无|  
|drive_user_id|int|接单用户id|无|  
|drive_user_pic_url|char(100)|接单用户头像url|无|  
|drive_user_name|char(100)|接单用户名称|无|  
|drive_user_phone|char(100)|接单用户联系电话|无|  
|drive_user_score|int|司机评分|无|  
|order_time|datetime|下单时间|无|  
|receive_time|datetime|接单时间|无|  
|get_time|datetime|取车时间|无|  
|arrive_survey_time|datetime|到达年检时间|无|  
|survey_time|datetime|年检结束时间|无|  
|arrive_return_time|datetime|到达还车时间|无|  
|return_time|datetime|还车时间|无|  
|confirm_time|datetime|确认时间|无|  
|cancel_time|datetime|取消时间|无|  
|comment_time|datetime|评论时间|无|  
|get_info|object|取车图片-证件照片|无|  
|get_confirm|object|取车图片-车损照片|无|  
|get_car|object|取车图片-车身拍照|无|  
|survey_upload|object|年检已过-上传照片|无|  
|survey_fail_upload|object|年检未过-上传照片|无|  
|return_info|object|还车图片-证件照片|无|  
|return_confirm|object|还车图片-车损照片|无|  
|return_car|object|还车图片-车身拍照|无|  
|failure_list|list|失败信息对象列表|无|  



get_info、get_confirm、get_car、survey_upload、survey_fail_upload、return_info、return_confirm、return_car:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|类别名称|无|  
|obj_list|list|列表|无|  

obj:

|参数|类型|说明|备注|  
|---|---|---|---|  
|pic_url|char(100)|图片url|无|  
|note|char(100)|备注|无|  

failure_list：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|补充项|无|  
|price|float|总计费用|无|  
|failureitem_list|list|失败详情|无|  

failureitem：  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|名称|无|  
|price|float|费用|无|  

```
{
    'data':
    [{
        'id':1,
        'create_time':'2018-07-08 12:23:34',
        'update_time':'2018-07-08 12:23:34',
        'order_code':'123413131',
        'name':'张三',
        'phone':'12345678998',
        'car_name':'张三',
        'car_brand':'玛萨拉蒂',
        'car_code':'粤A23452',
        'car_type':'小型蓝牌',
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
        'survey_state':0,
        'is_comment':0,
        'is_feedback':true,
        'drive_user_id':1,
        'drive_user_pic_url':'http://www.adsa.cn/sjdk.jpg',
        'drive_user_name':'李四',
        'drive_user_phone':'12312',
        'drive_user_score':1,
        'order_time':'2018-07-08 12:23:34',
        'receive_time':'2018-07-08 12:23:34',
        'get_time':'2018-07-08 12:23:34',
        'arrive_survey_time':'2018-07-08 12:23:34',
        'survey_time':'2018-07-08 12:23:34',
        'arrive_return_time':'2018-07-08 12:23:34',
        'return_time':'2018-07-08 12:23:34',
        'confirm_time':'2018-07-08 12:23:34',
        'cancel_time':'2018-07-08 12:23:34',
        'comment_time':'2018-07-08 12:23:34',
        'get_info':{
            'name':'取车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_confirm':{
            'name':'取车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'get_car':{
            'name':'取车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'survey_upload':{
            'name':'年检已过-上传照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_info':{
            'name':'还车图片-证件照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_confirm':{
            'name':'还车图片-车损照片',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'return_car':{
            'name':'还车图片-车身拍照',
            'obj_list':[{
                'pic_url':'www.aksdjha.cn/asdfa.jpg',
                'note':'asfdasdfasd'
            }]
        },
        'failure_list':[{
            'name':'补充项',
            'price':123,
            'failureitem_list':[{
                'name':'名称',
                'price':'费用'
            }]
        }]
    }]
}
```

<h4 id="ws_driver_listen">听单-服务端推送</h4>

使用websocket连接  
url:/ws/driver/listen/<:user_id>/<:timestampe>/<:sign>/  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|user_id|int|用户id|登陆成功后返回|1|必填|  
|timestamp|char(50)|时间戳|app自己生成|1|必填|  
|sign|char(50)|签名|md5(token+timestamp)|asdadsa|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|订单id|无|  

```
{
    'data':{
        'id':0
    }
}
```

<h4 id="driver_order_cancelinfo_get">司机扣费标准</h4>

url:/api/driver/order_cancelinfo/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|url|char(100)|页面url|无|  

```
{
    'data':{
        'url':'http://www.nolasthope.cn/driver/ordercancelinfo/'
    }
}
```

<h3 id="driver_account">账户</h3>

支付宝绑定过程：
使用“查询绑定的支付宝账号”接口查询绑定状态

<h4 id="driver_account_alipay_get">查询绑定的支付宝账号</h4>

url:/api/driver/account_alipay/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|name|char(100)|支付宝名称|无|   
|state|bool|绑定状态|无|   

```
{
    'data':{
        'name':'哈哈镜是空的',
        'state':false
    }
}
```

<h4 id="driver_account_alipay_info_get">获取绑定的支付宝账号信息</h4>

url:/api/driver/account_alipayinfo/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|params|char(100)|字符串信息|无|   

```
{
    'data':{
        'params':'qwdqwdqwdwd'
    }
}
```

<h4 id="driver_account_alipay_get">修改绑定的支付宝账号</h4>

url:/api/driver/account_alipay/  
method:post  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|   
|id|int|用户id|无|1|必填|   
|auth_code|char(100)|验证code|无|126134632|必填|   
|alipay_id|char(100)|支付宝用户id|无|11463465|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{
    }
}
```

<h4 id="driver_account_list_get">查询明细列表信息</h4>

url:/api/driver/account/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|method|int|行为|0：提现，1：收入，2：罚款|1|可选|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_time|datetime|时间|无|  
|start_address|char(100)|出发地点|无|  
|end_address|char(100)|到达地点|无|  
|method|int|行为|0：提现，1：收入，2：罚款|  
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|id|int|id|无|  
|create_time|datetime|创建时间|无|  
|update_time|datetime|修改时间|无|  
|order_time|datetime|时间|无|  
|start_address|char(100)|出发地点|无|  
|end_address|char(100)|到达地点|无|  
|method|int|行为|0：提现，1：收入，2：罚款|  
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

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|money|float|提现金额|无|1|必填|  
|via|char(100)|提现途径|alipay|alipay|必填|  
|alipay_account|char(100)|支付宝账号|无|张三|必填|  
|name|char(100)|真实姓名|无|张三|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':{}
}
```

<h4 id="driver_balance_get">用户余额查询</h4>

url:/api/driver/balance/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|id|无|1|必填|   

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  
|balance|float|余额|无|  

```
{
    'data':
    {
        'balance':11231,
    }
}
```

<h4 id="driver_driver_info_get">司机资料</h4>

url:/api/driver/driver_info/  
method:get  
param:   

|参数|类型|说明|备注|例子|是否必填|  
|---|---|---|---|---|---|  
|id|int|用户id|无|1|必填|   
|name|char(100)|姓名|无|张三|必填|   
|IDcard|char(100)|身份证号|1283651287468|1|必填|   
|pic_idcard_front|文件流|身份证正面照|无|(文件流)|必填|  
|pic_idcard_back|文件流|身份证反面照|无|(文件流)|必填|  
|pic_driver|文件流|司机正面照|无|(文件流)|必填|  
|pic_user|文件流|人证合一照|无|(文件流)|必填|  
|pic_drive_front|文件流|驾驶证正面照|无|(文件流)|必填|  
|pic_drive_back|文件流|驾驶证副页照|无|(文件流)|必填|  

return:  

|参数|类型|说明|备注|  
|---|---|---|---|  

```
{
    'data':
    {

    }
}
```
