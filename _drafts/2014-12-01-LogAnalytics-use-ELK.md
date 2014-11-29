---
layout: post
title: 用 Elasticsearch、Logstash 和 Kibana 分析日志
date: 2014-12-01 19:19:22
categories: tech
tags: Elasticsearch Logstash Kibana Log
---

# 目标



# 环境配置

## 使用的软件

Ubuntu Server 14.04
Elasticsearch
Logstash
Kibana
Logstash Forwarder

## 安装配置过程

### 安装 Java7 环境

	sudo apt-get install software-properties-common python-software-properties
	sudo add-apt-repository -y ppa:webupd8team/java
	sudo apt-get update
	sudo apt-get -y install oracle-java7-installer

### 下载解压 ELK（Elasticsearch、Logstash、Kibana 的简写）

	mkdir -p /log/src && cd /log/src

下载最新 Elasticsearch（当前是 1.4.0）、Logstash（1.4.2）、Kibana（3.1.2）：

    wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.4.0.tar.gz
    wget https://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.tar.gz
    wget https://download.elasticsearch.org/kibana/kibana/kibana-3.1.2.tar.gz

### 安装配置 Elasticsearch

添加禁止动态脚本行：

	script.disable_dynamic: true

限制 localhost：

	network.host: localhost


### 安装配置 Logstash



### 安装配置 Kibana



### 安装配置 Nginx

https://gist.github.com/thisismitch/2205786838a6a5d61f55





