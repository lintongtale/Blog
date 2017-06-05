---
title: AMES电力市场仿真
date: 2017-05-19 09:07:34
comments: true
tags:
- 电力市场仿真
- 电力市场交易
- 仿真软件
categories:
- 电力系统
- 电力市场
description:
- AMES电力市场仿真软件介绍。
---
# AMES电力市场仿真软件
## 简介
AMES（[下载](http://www2.econ.iastate.edu/tesfatsi/AMESMarket.V2.06-dist.zip)）是由Iowa State University用Java开发的基于多代理模型的一款开源电力市场仿真交易软件，全称是Agent-based Modeling of Electricity Systems。使用该软件需要电脑安装有Java，用户可以上[Java官网](https://www.java.com/zh_CN/)下载。

双击文件目录下的AMESMarket-2.06.jar，弹出如下界面：

<!--more-->

![Markdown](http://i2.muimg.com/594442/0a1356e0c7c7e570.png)

程序自带5节点及30节点测试算例。

## 说明
市场假设
* 市场遵循ISO（Independent System Operator）或者RTO（Regional Transmission Organization）原则
* 结算方式：日前（远期）和实时（现货）市场
* 采用LMP（Locational Marginal Price）
* 外部监管机构进行市场力及交易监管

交易者
* GenCos（卖方）
* LSEs（买方）
* Learning capabilities

ISO
* 系统可靠性评估
* 基于OPF（optimal power flow）的日前发电计划
* 实时调度

结算方式
* 日前市场（双重拍卖，金融合约）
* 实时市场（差价）

## 5节点测试案例
定义：激励错位  
制度设计不符合效率目标电力系统参与者的激励（非资源消耗）或福利目标（社会理想分布的总净剩余个别电力系统参与者）

