# billingcooker

# 项目背景

### 由于一些特定场景和需求，需要给出对应域名计费带宽数据，比如第4峰值 或95计费的截图，或给对应一些客户基于域名API 的带宽数据。

### 在线DEMO

**<mark>生成当前数据，请粘到浏览器中执行（把month=2022-02 替换为当前月份）</mark>**


[https://bwdemo.xiangyundns.cn/master/data/month/generate?domain=img.qq.com&month=2022-02&token=339a65e93299ad8d72c42b263aa23117](生成指定时间数据)

生成后，访问

https://bwdemo.xiangyundns.cn/

![](https://raw.githubusercontent.com/bytebitgo/billingcooker/main/demo.png)

## http api (客户使用)

- 一分钟接口 

`https://bwdemo.xiangyundns.cn/api/data/bandwidth/realtime/edge?domain=img.qq.com&start=2022-02-01T00:00:00&end=2022-02-04T23:59:00`

- 五分钟接口 

`https://bwdemo.xiangyundns.cn/api/data/bandwidth/edge?domain=img.qq.com&start=2022-02-01T00:00:00&end=2020-02-04T23:59:00`

- 返回数据格式 

```
{

"success": "1", // 1：success，0：fail

"error": "",

"data": [

{

"time": "2020-12-04T00:00:00",

"bps": 10656659000000

},

{

"time": "2020-12-04T00:05:00",

"bps": 10236982600000

}

]

}
```

- 接口限制拉取数据间隔不能超过`24`小时





## master api （管理端使用，返回目前配置域名列表 重新生成月份数据）

- 域名列表 

`https://bwdemo.xiangyundns.cn/master/domain/list?&token=339a65e93299ad8d72c42b263aa23117`

- 数据返回格式 

```
{

"success": "1",

"error": "",

"data": [

"img.qq.com"

]

}
```

- 重新生成某月的数据 <br>

`https://bwdemo.xiangyundns.cn/master/data/month/generate?domain=img.qq.com&month=2022-02&token=339a65e93299ad8d72c42b263aa23117`

- 服务端查看已经生成计费数据 ( master_token: "339a65e93299ad8d72c42b263aa23117" 
  
  
-  访问master api所需的token, 在etc/billingcooker/config.yaml配置)

- 一分钟接口 

`https://bwdemo.xiangyundns.cn/master/data/bandwidth/realtime/edge?domain=img.qq.com&start=2021-01-01T00:00:00&end=2022-02-01T23:59:00&token=339a65e93299ad8d72c42b263aa23117`

- 五分钟接口 

`https://bwdemo.xiangyundns.cn/master/data/bandwidth/edge?domain=img.qq.com&start=2021-01-01T00:00:00&end=2022-02-01T23:59:00&token=339a65e93299ad8d72c42b263aa23117`

___

## 配置文件例子

- 生成规则配置 [rule.yaml](rule.yaml)

- 域名及通用配置 [config.yaml](config.yaml)

