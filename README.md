# online-car-hailing
网约车Web项目，redis+mysql+rocketMQ+Prometheus

## 业务需求

### 基础服务

1. 用户管理
2. 权限管理
3. 角色管理

### TOC

1. 用户方向
   1. 实时叫车（定位/输入地址）
   2. 长途车预定(预定时间以及地址)
   3. 付款（线上/线下）
   4. 订套餐
   5. 突发事件快速报警
2. 司机方向
   1. 接单
   2. 扣税
   3. 定套餐
3. 套餐预定方向
   1. 用户
   2. 司机
4. 定位与地图服务

### TOB

1. 定位与地图找车
2. 及时通话以及临时聊天服务
3. 控诉服务与监控
4. 支付服务
5. 管理员平台
6. 文件过期服务（语音监听过期删除）

### 额外考虑业务问题

1. 选车算法
2. 扣税算法
3. 双方支付怎么保证
4. 路线规划算法（支持用户选择（最快/最便宜））

## 技术选型

### 后端选型

1. rocketmq保证高并发的可靠性，定时消息，事务等等
2. Redis保证快速响应
3. Prometheus观测性
4. mysql持久性

### 安卓选型

1. 前端选型

## 数据库

表结构

1. 用户表
   1. Id:主键
   2. userId：用户id
   3. phone：电话
   4. password：密码
   5. 角色
2. 权限表（Redis缓存）
   1. Id
   2. Discription
   3. name
3. 角色表
   1. Id
   2. Name
   3. String:对应权限（一次MySQL IO）
4. 订单表
   1. Id
   2. order_id
   3. Status
   4. file_address
5. 套餐表
   1. Id
   2. Tye
   3. 开始时间/过期时间
   4. content：优惠内容
   5. price
   6. 剩余份数
6. 用户-套餐表
   1. Id
   2. Userid
   3. taocan_id
   4. status
7. 投诉表
   1. Id
   2. Userid
   3. order_id
   4. Content
