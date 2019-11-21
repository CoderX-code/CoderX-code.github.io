---
title: SpringBoot教程：快速入门（1）
date: 2019-10-26 12:02:47
tags: SpringBoot
categories: SpringBoot
---

# SpringBoot简介

**什么是SpringBoot?**

SpringBoot是Spring开源组织下的一个子项目，旨在简化Spring繁琐的配置，减少配置代码和xml配置文件，降低使用Spring框架的难度。

SpringBoot提供了各种启动器starter，只需引入待使用组件对应的starter SpringBoot即能完成自动配置，开箱即用，开发者能够快速搭建Java项目，避免了以前的构建项目、应用打包、服务部署等操作。

**SpringBoot的优点**

- 为所有Spring开发者更快的入门
- 开箱即用，提供各种默认配置来简化项目配置，自动配置（各种组件的starter）
- 独立运行，内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

**SpringBoot的缺点**

- 上手容易精通难
- Spring项目难以平滑迁移至SpringBoot

# 创建项目

## 环境准备

- Maven 3.3以上版本

- IDEA 2018

- Jdk 1.8+

## 创建项目

创建SpringBoot有两种方式：通过官网的Spring Initializr创建；通过IDEA创建。

1）官网创建

进入https://start.spring.io/，看到项目创建页面。

![image-20191026132451879](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191026132451879.png)

选择对应的参数配置后，点击`Generate`即可。

![image-20191028101455602](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028101455602.png)

2) IDEA中创建

![image-20191028112341695](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028112341695.png)

![image-20191028112847084](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028112847084.png)

勾选需要的依赖，如需要创建web应用，勾选spring-web

![image-20191028125614119](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028125614119.png)

点击next，之后就生成了一个SpringBoot工程。

# 工程结构

工程目录如下：

![image-20191028130157757](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028130157757.png)

Main/java: java源代码目录

Resource: 资源文件夹，Springboot默认在该路径下寻找资源文件

​		static: 放置静态资源文件，如css、js文件等

​		template：放置页面模板文件，html，vm、thymleaf文件等

test: 测试代码目录

# 项目启动

可以在IDEA中启动项目，也可以打包项目后通过命令行启动项目，下面分别介绍两种启动方式。

## IDEA中启动项目

打开项目对应的Application文件，这里是`SpringbootDemoApplication`，点击工具栏上方的`Run`启动程序。![image-20191028131317515](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028131317515.png)

控制台输出`Started SpringbootDemoApplication in 1.726 seconds (JVM running for 2.375)`，启动成功。

![image-20191028131634754](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028131634754.png)

## 命令行启动

命令行启动首先需要将工程打成一个可执行的jar包，在项目的pom文件中引入如下依赖(项目文件若是通过Spring Initializr自动生成的应该有这个依赖)：

```xml
 <!-- 这个插件，可以将应用打包成一个可执行的jar包；-->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

执行命令`mvn package`后，可以看到target目录下生成了jar包。

![image-20191028133645225](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028133645225.png)

执行`java -jar jar文件 `，运行程序，效果同1)。

![image-20191028134123492](SpringBoot%E6%95%99%E7%A8%8B%EF%BC%9A%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%EF%BC%881%EF%BC%89/image-20191028134123492.png)