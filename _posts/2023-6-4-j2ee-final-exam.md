---
title: J2EE 期末大作业
date: 2023-06-04 09:00:00 +0800
categories: [Examination, Question]
tags: [exam]
author: saikaisa
---

[TOC]

## 目标

**设计和实现一个简单web应用，实现商品预定功能**





## 知识要求

HTML标记语言、Servlet编程API文档、JSP页面元素、MVC【必须采用】，JDBC数据库编程、JDBCUtils、DBUtils等第三方数据访问库【可选】、分页功能【可选】。





## 具体内容要求和扣分点

### 1. 项目名称为“序号-Homework”，web应用名称“Homework_序号



### 2. 数据库创建

- [ ] 创建3张表**user**，**product**和**reservation**

  - **user(uId, uName, uPw)**，存储用户信息，每行表示一个用户，依次记录其用户id（自动分配）、姓名和密码信息
  - **product (pId, pName, pPrice, pCount)**，存储商品信息，每行表示一种商品，依次记录其商品id（自动分配）、商品名称、商品单价和剩余可供预定或销售的商品数量等信息
  - **reservation (oId, uId, pId，oTime, oCount，oTotal, oStatus)**，存储订单信息，依次订单id（自动分配）、用户id、商品id，预定时间（年月日小时分钟秒）、订购的商品数量、订单总价和订单状态（进行中、已完成、已撤销）等信息。值得说明的是：reservation设计与真实情况不符，**每个预定仅允许订购一种类型的商品**。
- [ ] 创建完成后**预先插入数据**，表user不少于**3**个用户，表product不少于**20**种商品，表reservation不少于**10**个订单。*<u>提交该功能点截图</u>*反映表状态。

[^扣分点]: 【少设计一个表，扣5分；少一个截图，扣5分；数据类型不合适，每个字段扣1分，单个表最多扣3分；表中数据量不满足要求，单个表扣1分；本功能点最多扣15分】



### 3. 实现登录功能

- [ ] 创建3个jsp页面，分别为**login.jsp**、**main.jsp**和**loginFailure.jsp**
  - [ ] login.jsp 负责实现登录表单，包括：用户名、密码和验证码；
  - [ ] loginFailure.jsp 负责给出登录失败的原因描述，并能跳转到login.jsp进行重新登录。
  - [ ] main.jsp 负责实现提示登录成功，5秒钟后自动跳转到 [allReservation.jsp](#allReservation.jsp) 页面，展示该用户的所有预定信息【见商品预定管理功能部分】。
- [ ] 创建1个实体类**User**，封装用户名、密码等信息
- [ ] 创建1个登录业务逻辑处理类**LoginService**，实现登录业务逻辑处理
- [ ] 创建1个用户数据访问类**UserDAO**，从数据库表user中读写用户数据
- [ ] 创建1个servlet，名为**LoginController**，负责实现控制器功能，完成请求数据获取和封装、将请求分发到业务逻辑处理对象 LoginService（实现登录逻辑），并根据业务处理结果确定合适的结果展示页面：main.jsp（登录成功）或 loginFailure.jsp（登录失败，给出原因）。

[^扣分点]: 【缺少能表明该功能点实现的截图，扣15分；表明该功能点实现的截图逻辑性不强，扣5分；缺少User、LoginService、UserDAO、LoginController，每个扣5分；代码功能实现不正确，每个扣5分；资源命名不正确，每个扣1分；本功能点最多扣35分】



### 4. 商品管理和预定功能

- [ ] #### [**allReservation.jsp**](#allReservation.jsp)

	页面布局如下图所示。
	
	<img src="http://pics.saikaisa.top/image-20230604085252868.png" alt="image-20230604085252868" style="zoom: 80%;" />
	
	在页面allReservation.jsp增加2个按钮“**浏览商品**”和“**变更预订状态**”分别跳转到页面**productOverview.jsp**和**modifyReservation.jsp**，具体功能要求见浏览商品页面[productOverview.jsp](#productOverview.jsp)、预订状态变更页面[modifyReservation.jsp](#modifyReservation.jsp)。

	[^加/减分项]: 若提供分页功能，则有额外5个加分【最高分为100分】。【不显示当前用户名，扣3分；中文乱码，扣3分，商品名称没有出现中文，扣3分；预订时间错乱，扣3分；缺少该功能点截图，扣10分；表明该功能点实现的截图逻辑性不强，扣3分；缺少Reservation（实体类，对应表reservation）、Product（实体类、对应表product）、ReservationDAO（实现对表reservation数据读写操作）、ProductDAO（实现对表product数据读写操作）、ReservationService、ReservationController，ProductService、ProductController，每个扣2分；代码功能实现不正确，每个扣3分；资源命名不正确，每个扣1分；本功能点最多扣25分】
	
- [ ] #### [**modifyReservation.jsp**](#modifyReservation.jsp)

	在allReservation.jsp页面通过订单编号列前的选择框选择一行**（每次仅可以选择1行）**，点击“变更预订状态”按钮，跳转到页面**modifyReservation.jsp，**显示该预订详细信息，如图所示。**仅当预订状态为“进行中”，才可以进行变更**，从**“进行中” → ”已撤销”**，或者从 **“进行中” → ”已完成”**。**取消变更则返回页面**allReservation.jsp，确认变更成功则也返回allReservation.jsp，否则提示不能变更，**停留在页面**modifyReservation.jsp。
	
	<img src="http://pics.saikaisa.top/image-20230604085728827.png" alt="image-20230604085728827" style="zoom:50%;" />
	
- [ ] #### [**productOverview.jsp**](#productOverview.jsp)

	浏览商品页面，展示所有商品信息，自行设计页面布局，展示所有商品信息项。

- [ ] 创建1个实体类**Product**，封装商品信息
- [ ] 创建1个实体类**Reservation**，封装商品预订信息
- [ ] 创建1个商品数据访问类**ProductDAO**，从数据库表product中读写商品信息，**至少应该包含获取所有商品信息，或者部分商品信息的数据库读写操作**；采用DBUtils实现数据库访问，增加额外5分
- [ ] 创建1个商品预订数据访问类**ReservationDAO**，从数据库表reservation中读写预订信息，**至少应该包含读取所有预订信息、更改特定订单的状态（“进行中” → ”已撤销”、 “进行中” → ”已完成”）**；采用DBUtils实现数据库访问，增加额外5分
- [ ] 创建1个商品预订管理业务逻辑处理类**ReservationService**，实现预订管理相关业务逻辑处理，**包括查看预订，变更预订状态**
- [ ] 创建1个servlet，名为**ReservationController**，负责实现控制器功能，完成**预订管理相关请求的数据获取和封装**、将**请求分发**到业务逻辑处理对象**ReservationService**，并**根据业务处理结果确定合适的结果展示页面**

- [ ] 创建1个商品管理业务逻辑处理类**ProductService**，实现商品管理相关业务逻辑处理，包括查看所有商品信息、查看特定商品信息等
- [ ] 创建1个servlet，名为**ProductController**，负责实现控制器功能，完成商品管理相关请求的数据获取和封装、将请求分发到业务逻辑处理对象**ProductService**，并根据业务处理结果确定合适的结果展示页面

