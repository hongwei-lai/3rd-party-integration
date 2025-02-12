## 库存信息接口
### 1.被动获取库存信息接口
#### 1.1 接口描述
* 1.ERP预先同步库存数据至线上系统，并且将库存数据持续与线上系统保持同步
* 2.预下单时，实时查询商品在哪些门店拥有库存
* 3.门店盘点时，实时查询商品库存确定盘点盈亏
* 4.以门店为单位同步，一次可同步一个门店的多个库存数据
#### 1.1 结构描述
> 根据给定的参数通过结构查询获取商品对应门店的库存信息
#### 1.2 请求方式
> POST
#### 1.3 url
* 线上系统
> /orders/storagePassive
#### 1.4 数据方向
> ERP-->线上系统
#### 1.5 请求参数
| 参数名称 | 参数类型 | 是否必须 | 示例值 | 参数描述  |
| :---         |     :---      |     :--- | :--- | :--- |
| unitNo   | 字符串    | 是    | 2    | 门店id |
| siteId   | 字符串    | 是    | 100123    | 商户id |
| goodsCode   | 字符串    | 是    |   90301104  | 商品编码 |
| specification   | 字符串    | 是    |   10*10  | 商品规格 |
| state   | 整型    | 是    |   0  | 商品状态:: 0: 正常，1:不正常，2:删除|
| inventoryQuantity   | 浮点型    | 是    |   39.00  | 库存数量，两位小数|
--------------------- 
#### 1.6 请求示例
```
{
  "unitNo":"913",
  "siteId":"100123"，
  "goodsList":[{
    "goodsCode": "90301104",
    "specification": "10*10",
    "state": "0",
    "inventoryQuantity": "39.00"
  },
  {
    "goodsCode": "90301105",
    "specification": "10*10",
    "state": "0",
    "inventoryQuantity": "22.00"
  }]
}
```
#### 1.7 返回参数
| 参数名称 | 参数类型 | 是否必须 | 示例值 | 参数描述  |
| :---  |   :-------    |    :---   | :---        | :---        |
| code   | 字符串     | 是            | 10000   |返回结果标识::10000:成功,20000:失败|
| msg   | 字符串     | 是    | 推送成功   |返回结果描述|
--------------------- 
#### 1.8 返回示例(匹配到库存信息)
 ``` 
{
    "code" : 10000,
    "msg" : "推送成功"
    }
}
```
#### 1.9 返回成功(未匹配到库存信息)
```
{
  "code": 10000,
  "msg":"推送成功"
}
```
#### 2.0 请求失败
```
{
  "code": 20000,
  "msg":"推送失败,相关原因"
}
```
