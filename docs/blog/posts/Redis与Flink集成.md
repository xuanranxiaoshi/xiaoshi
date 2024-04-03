---
draft: false
date: 2024-03-13
authors:
  - jimi
categories:
  - redis
---

# Redis 基本配置 + Flink Connector

>   2024-03-13

1. Redis 基本安装配置
2. Flink 与 Redis 集成
注：[redis notion笔记](https://www.notion.so/Redis-75ad492d44324ef683261c395279a715#0e46f9a1a421497c8fb85f938cb70dc4)
<!-- more -->

## 一、Redis 基本安装配置

[1][Linux安装部署Redis(超级详细)](https://www.cnblogs.com/hunanzp/p/12304622.html) </br>
[2][Linux下redis7的安装，启动与停止](https://blog.csdn.net/qq_54796785/article/details/126028613)</br>

## 二、Redis 与 FlinK 集成

### 1. POJO 类转 Json 字符串

【问题描述】 POJO 类使用 jackson @JsonProperty 注解指定属性，从 json 字符串转换而来，使用 lambok @Data 注解自动生成 getter、setter 方法；而在将其再次转换 json 字符时，发现转换后的 json 字符串中含有的属性多于 POJO类中定义的属性，增加的属性包括：@JsonProperty 指定的属性名的小写、额外添加的 getXX 和 isXX 方法中的属性名 XX；



【问题原因】产生这个的原因



[3][Flink Redis sink](https://blog.csdn.net/qq_38628046/article/details/133811880)