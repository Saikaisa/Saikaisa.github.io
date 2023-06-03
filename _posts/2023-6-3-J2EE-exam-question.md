---
title: J2EE 模拟题
date: 2023-05-13 18:40:00 +0800
categories: [Examination, Question]
tags: [exam]
author: saikaisa
---
## 1. 数据库创建

- [ ] 创建数据库，名为“序号_JDBC”

- [ ] 创建3张表user，food和order

  - user(uId, uName, uPw, uSchool, uDepartment)，存储学生信息，每行表示一个学生，依次记录其id（自动分配）、姓名、密码、学院、系等信息。

  - food(fId, fName, fPrice, fType)，存储外卖菜肴信息，每行表示一种菜肴，依次记录其id（自动分配）、菜肴名称、单价和类型（在售、停售、缺货）等信息。

  - **orders**(oId, uId, oTime, **oItems**, totalPrice)，存储订单信息，依次订单id（自动分配）、用户id、订单时间（年月日小时分钟秒）、订购的菜肴和订单总价等信息。

  - 创建完成后预先插入数据，表user不少于3个用户，表food不少于20种菜肴，表order不少于10个订单。

	[^扣分项]: 【少设计一个表，扣5分；少一个截图，扣5分；数据类型不合适，每个字段扣1分，单个表最多扣3分；数据条目不满足要求，单个表扣1分；本功能点最多扣15分】



## 2. 实现登录功能

- [ ] 创建3个jsp页面，分别为**login.jsp**、**main.jsp**和**loginFailure.jsp**

  - login.jsp 负责实现登录表单，包括用户名、密码和验证码，“所在学院”【下拉列表】、“所在系”【下拉列表】，要求实现系与学院的联动，即选择的学院改变所在系的选项也同步变化；

    ![img](http://pics.saikaisa.top/clip_image002.png)

  - **loginFailure.jsp** 负责给出登录失败的原因描述，并能跳转到**login.jsp**进行重新登录。

  - **main.jsp** 负责实现提示登录成功，5秒钟后自动跳转到**allOrder.jsp**页面【见菜肴和订单管理功能部分】。

- [ ] 创建1个实体类**Login**，封装用户名、密码等信息
- [ ] 创建1个登录业务逻辑处理类**LoginService**，实现登录业务逻辑处理
- [ ] 创建1个用户数据访问类**UserDAO**，从数据库表user中读写用户数据
- [ ] 创建1个servlet，名为**LoginController**，负责实现控制器功能，完成请求数据获取和封装、将请求分发到业务逻辑处理对象**LoginService**（实现登录逻辑），并根据业务处理结果确定合适的结果展示页面：**main.jsp**（登录成功）或**loginFailure.jsp**（登录失败，给出原因）

	[^扣分项]: 【缺少能表明该功能点实现的截图，扣15分；表明该功能点实现的截图逻辑性不强，扣10分；缺少Login、LoginService、UserDAO、LoginController，每个扣5分；代码功能实现不正确，每个扣5分；资源命名不正确，每个扣1分；本功能点最多扣35分】



## 3. 菜肴和订单管理功能

- [ ] #### allOrder.jsp

	<img src="http://pics.saikaisa.top/image-20230603201157374.png" alt="image-20230603201157374" style="zoom:67%;" />

	在页面**allOrder.jsp**增加3个按钮“浏览菜肴”、“删除订单”和“撤销订单”，其中浏是览菜肴页面不用实现功能，出现该超链接或按钮即可。

	[^扣分点]: 【不显示当前用户名，扣3分；中文乱码，扣3分；订单时间错乱，扣3分；缺少该功能点截图，扣10分；表明该功能点实现的截图逻辑性不强，扣3分；缺少Order、Food、OrderDAO、FoodDAO、OrderService、OrderController，每个扣3分；代码功能实现不正确，每个扣3分；资源命名不正确，每个扣1分；本功能点最多扣25分】

- [ ] 	#### delOrder.jsp

	显示选中一行或者多行（通过**allOrder.jsp**的序号列前的选择框选择），确认取消后，若执行取消成功，给出提示信息，而后跳转到**allOrder.jsp**，取消失败则跳转到**orderFailure.jsp**，给出失败原因描述，并提供超链接返回**allOrder.jsp**；**订单删除逻辑为：选中的所有订单，当前时间距离订单时间大于24小时，则订单可以删除。**

- [ ] #### cancelOrder.jsp

	显示选中一行或者多行（通过**allOrder.jsp**的序号列前的选择框选择），确认取消后，若执行取消成功，给出提示信息，而后跳转到**allOrder.jsp**，取消失败则跳转到**orderFailure.jsp**，给出失败原因描述，并提供超链接返回**allOrder.jsp**；**订单取消逻辑为：选中的所有订单，当前时间距离订单时间小于10分钟。**

- [ ] #### orderFailure.jsp

  展示订单管理中出现的可能错误信息。

  

- [ ] 创建1个实体类**Food**，封装菜肴信息。
- [ ] 创建1个实体类**Order**，封装订单信息。
- [ ] 创建1个菜肴数据访问类**FoodDAO**，从数据库表food中读写菜肴信息；**采用DBUtils实现数据库访问，增加额外5分【数据库编程额外加分最多5分】**
- [ ] 创建1个菜肴数据访问类**OrderDAO**，从数据库表order中读写订单信息；**采用DBUtils实现数据库访问，增加额外5分【数据库编程额外加分最多5分】**
- [ ] 创建1个订单管理业务逻辑处理类**OrderService**，实现订单相关业务逻辑处理，包括查看订单，取消订单、删除订单；考虑上述描述的订单取消和删除逻辑；
- [ ] 创建1个servlet，名为**OrderController**，负责实现控制器功能，完成订单相关请求的数据获取和封装、将请求分发到业务逻辑处理对象**OrderService**，并根据业务处理结果确定合适的结果展示页面：**allOrder.jsp**、**delOrder.jsp**、**cancelOrder.jsp**、**orderFailure.jsp**。





