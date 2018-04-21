---
title: mybatis
photos:
  #- ''
date: 2018-01-09 20:55:37
tags: 
	- java
	- web
	- mybatis
	- framework
categories: 
	- java
	- framework
	- mybatis
	
comments:
---
{% fi http://p6wzlnrcf.bkt.clouddn.com/bolg-message-backgrund.jpg %}
框架（Framework）
<!-- more -->

[toc]

# 框架技术
## 什么是框架：
客观解释：
>框架（Framework）框架这个词最早出现在建筑领域，指的是在建造房屋前期构建的建筑骨架。对于我们所开发的程序来说，“框架”就是我们程序的骨架。通过框架可以使程序开发变得简单且利于维护，使混乱的东西变得有序。++框架的强大之处不是源自它能让你做什么，而是它不能让你做什么！++

个人理解：
>懒是人类进步的原始动力，车子是、taobao是、框架也是。框架就是让我们站在前辈的肩膀上把偷懒的精神发扬光大。（懒为褒义）

总的来说：
>一千个人眼中有一千个哈姆雷特，每一个程序员都有不同的代码风格。框架则将程序员的代码风格强制要求为某一种统一的规范。提高代码的可读性、降低后期的维护成本。

# Mybatis框架
## Mybatis框架简介 && ORM
### Mybatis框架简介
MyBatis是一个开源的数据持久层框架。它内部封装了通过JDBC访问数据库的操作，支持普通的SQL查询、存储过程和高级映射，几乎消除了所有的JDBC代码和参数的手工设置以及结果集的检索。MyBatis作为持久层框架。思想上是将程序中的大量SQL语句剥离出来，配置在配置文件中，实现SQL的灵活配置，这样做的好处是将SQL与程序代码分离，可以在不修改程序代码的情况下，直接在配置文件中修改SQL。

[MyBatis官网 (科学访问)](https://mybatis.org)

[Github](https://github.com/mybatis)

###  ORM
ORM (Object/Relational Mapping) ：
>对象/关系映射，是一种数据持久化技术。它在对象模型和关系型数据库之间建立起对应关系，并且提供一种机制，通过JavaBean对象去操作数据库表中的数据.
# Mybatis环境搭建
在Eclipse中新建工程后，要使用MyBatis，需做以下准备工作。

```
graph LR
Mybatis环境搭建-->1.下载jar包
Mybatis环境搭建-->2.部署jar包
Mybatis环境搭建-->3.编写MySatis核心配置文件
Mybatis环境搭建-->4.创建实体类
Mybatis环境搭建-->5.创建DAO接口
Mybatis环境搭建-->6.创建SQL映射文件
Mybatis环境搭建-->7.编写测试类

```
## Mybaits-config.xml详解

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-config.dtd">
 <!--以上为配置文件声明（固定格式）-->
 <configuration>    <!--根节点（唯一）-->
    <!--加载外部属性文件-->
    <!--<properties resource="jdbc.properties"></properties>-->
    <!--方式二：直接在配置文件中定义属性（）-->
    <properties resource="jdbc.properties">
		<property name="jdbc.driver" value="com.mysql.jdbc.Driver" />
		<property name="jdbc.url" value="jdbc:mysql://127.0.0.1:3306/easybuy?useUnicode=true&amp;characterEncoding=UTF8" />
		<property name="jdbc.username" value="root" />
		<property name="jdbc.password" value="123456" />
	</properties>
	<!-- settings:Mybatis全局配置标签 -->
	<settings>
		<setting name="logImpl" value="LOG4J" />
		<!-- PARTIAL:自动把属性名和列名相同的数据，进行设置值（在有association或collection标签会失效） -->
		<setting name="autoMappingBehavior" value="FULL" />
		<!-- 启用二级缓存 -->
		<!-- <setting name="cacheEnabled" value="true"/> -->
	</settings>
	<!-- 给现有的实体类定义，方便sql配置文件中直接使用，sql中可以直接使用别名代表相应的实体类 -->
	<!-- 自动给某个包下所有类取别名，别名为：类名全小写 -->
	<typeAliases>
		<package name="com.demo.entity" />
	</typeAliases>
	<!-- environments：配置程序数据库环境，可以配置多个数据库（开发库，测试库，生产库） -->
	<!-- default：默认使用的数据库id -->
	<environments default="development">
		<!-- id：数据库环境唯一标识 -->
		<environment id="development">
			<!-- transactionManager：配置程序事务管理的容器 -->
			<!-- type：jdbc（由JDBC管理事务）、managed（mybatis不负责事务，由外部容器管理，比如：spring容器、JavaEE应用服务器管理） -->
			<transactionManager type="JDBC" />
			<!-- dataSource：配置数据库连接的获取方式 -->
			<!-- POOLED：用户数据库连接池的方式获得连接、unpooled:非数据库连接池方式，程序要连接数据库的时候，再连接，适用于非常简单的小程序 -->
			<!-- JNDI：适用于用外部容器配置数库连接的情况，外部容器管理连接 -->
			<dataSource type="POOLED">
				<!-- driver：数据库连接，驱动类 -->
				<!--**注意**property中name属性的值不可变（固定写法）-->
				<property name="driver" value="${jdbc.driver}" />
				<!-- url：数据库连接的地址 -->
				<property name="url" value="${jdbc.url}" />
				<!-- username:用户名 -->
				<property name="username" value="${jdbc.username}" />
				<!-- password:密码 -->
				<property name="password" value="${jdbc.password}" />
			</dataSource>
		</environment>
	</environments>

	<!-- 加载sql配置文件 -->
	<mappers>
		<mapper resource="com/demo/mapper/UserDaoMapper.xml" />
	</mappers>
 </configuration>
```


















