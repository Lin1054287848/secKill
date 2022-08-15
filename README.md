# Seckill
# 秒杀系统
## 整体介绍：

秒杀主要解决两个问题，并发读和并发写。  
并发读的核心优化理念就是尽量减少用户到服务端来读数据，或者让用户读更少的数据；  
并发写也一样，我们要在数据库层做一个独立的库，来做特殊的处理。  
不管是并发读也好，并发写也好，都是为了缓解数据库的读写压力，防止大量的请求瞬间到达数据库使数据库响应速度变慢甚至使服务器崩溃。  

另外，我们还要设计兜底方案，为最坏的情况做打算。  

秒杀整体架构可以概况为“稳、准、快”。  

稳：系统要满足高可用，流量在预期范围内必须要稳定，流量超出预期也要撑住，不可以崩溃。保证整个秒杀过程顺利，商品能顺利卖出去。参考铁路12306，每年春运流量高峰期，也能保持系统正常运行不至于崩掉。  

准：字面意思，数量精准。秒杀活动上架100台手机，那就只能成交出100台。多一台或者少一台都不可以(同一个用户只能秒杀一台，多一台不行，同时如果秒杀成功，就是一台，少一台也不行)  

快：快也好理解，就是性能要足够高，即速度要快。像京东淘宝的购物节，如果不够快，性能不够高，同一时间大量用户涌入平台，系统的响应速度会慢得让人受不了，网页加载慢，图片加载也慢，不免让用户抱怨一句“ ** 卡死了 ”。  

“稳、准、快”就对应了我们系统架构的高可用、高一致、高性能。  

本项目重点在实现后端秒杀功能，前端只写了几个简单的页面  

## 项目技术栈：
### 前端：
Thymeleaf模板、Bootstrap、Jquery
### 后端：
Spring Boot、Mybatis-Plus、Lombok、Redis、RabbitMQ、JMeter压测工具
### 开发工具：
IDEA、Git、Maven、FinalShell、VMware、Redis Desktop Manager
## 秒杀方案：
### 分布式会话：
1.用户登录
设计数据库  
明文密码进行二次MD5加密  
参数校验+全局异常处理  
2.共享Session
SpringSession  
Redis  
### 功能开发：
商品列表  
商品详情  
秒杀  
订单详情  
### 系统压测：
JMeter  
自定义变量模拟多用户  
JMeter命令行的使用  
#### 正式压测
商品列表  
秒杀  
### 页面优化：
页面缓存+URL缓存+对象缓存  
页面静态化，前后端分离  
静态资源优化  
CDN优化  
### 接口优化：
Redis预减库存减少数据库的访问  
内存标记减少Redis的访问  
RabbitMQ异步下单  
SpringBoot整合RabbitMQ  
交换机  
### 安全优化：
秒杀接口地址隐藏  
算术验证码  
对接口限流，防刷
