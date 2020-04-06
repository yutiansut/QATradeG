# QATradeG
trade gateway

本代码基于OPEN-Trade-Gateway修改而成, 直接部署即可, 内部没有代码 只有编译好的程序

本项目支持 windows/mac/linux 全平台部署 具体可以参考quantaxis项目的docker文档

感谢天勤提供的OPEN-TRADE-GATEWAY项目,  本项目不提供源代码, 仅供QUANTAXIS用户快速连接OTG和qifi协议使用


- 本地部署的OTG版本 支持所有ctp的接口

- 增加了转账的请求部分 以及 可取资金查询

接入程序 python版本 

- https://github.com/yutiansut/qatrader
- https://github.com/yutiansut/QIFI
- https://github.com/yutiansut/qaotgbroker

目前行情有关的项目推荐是 基于ctpbee直连ctp+ qamarket-rs (rust写的高性能行情分发采样)

- http://github.com/yutiansut/qactpbeebroker
- https://github.com/yutiansut/qamarket-rs

行情的docker-compose被集成在quantaxis的service-future中:

https://github.com/QUANTAXIS/QUANTAXIS/blob/master/docker/qa-service-future/docker-compose.yaml

以及 rust行情替换教程
http://www.yutiansut.com:3000/topic/5e5e6f026d3b182e88b4f71c

另外你可以直接在本地开启自己的期货模拟盘 只需要行情自己做撮合

https://github.com/yutiansut/qifiaccount

https://github.com/yutiansut/qastrategy




### 使用

直接fork/ clone 到你的项目, 修改增加你自己的broker_list.json


然后拉起来即可

docker-compose up -d


### 运维:


查询日志:

cat docker/log/open-trade-gateway.log


示例返回

```
root@redis-1:/home/ubuntu/qatradeG/docker/log# cat open-trade-gateway.log
{"time":"2020-04-06T12:02:06.404075532+08:00","level":"info","node":"6ae545f32608","msg":"trade server init","key":"gateway"}
{"time":"2020-04-06T12:02:06.404218710+08:00","level":"info","node":"6ae545f32608","msg":"LoadConfig","trading_day":"20200406"}
{"time":"2020-04-06T12:02:06.410150441+08:00","level":"info","node":"6ae545f32608","msg":"mdservice init","key":"mdservice"}
{"time":"2020-04-06T12:02:06.660927830+08:00","level":"info","node":"6ae545f32608","msg":"msg=md service download ins file successful, count = 0","key":"mdservice"}
{"time":"2020-04-06T12:02:06.737108837+08:00","level":"info","node":"6ae545f32608","fun":"StartConnect","msg":"mdservice StartConnect openmd service","key":"mdservice"}
{"time":"2020-04-06T12:02:06.737236404+08:00","level":"info","node":"6ae545f32608","msg":"mdservice init success","key":"mdservice"}
{"time":"2020-04-06T12:02:06.767660425+08:00","level":"info","node":"6ae545f32608","fun":"OnMessage","msg":"md_connection receive md message","len":"61","key":"mdservice"}
{"time":"2020-04-06T12:02:07.734474384+08:00","level":"info","node":"6ae545f32608","fun":"OnMessage","msg":"md_connection receive md message","len":"6233869","key":"mdservice"}
root@redis-1:/home/ubuntu/qatradeG/docker/log#
```

### 重启/关闭


docker-compose restart


docker-compose down


@yutiansut
2020-04
