---
layout:     post
title:      "油猴的简单使用"
subtitle:   "挖掘chrome的潜力"
date:       2017-09-05 14:50:04
catalog: true
tags:
    - 插件
    - plugins
---

- [步骤](#%E6%AD%A5%E9%AA%A4)
  - [1. 打开一个新标签页](#1-%E6%89%93%E5%BC%80%E4%B8%80%E4%B8%AA%E6%96%B0%E6%A0%87%E7%AD%BE%E9%A1%B5)
  - [2. 地址栏输入`chrome://apps/`](#2-%E5%9C%B0%E5%9D%80%E6%A0%8F%E8%BE%93%E5%85%A5chromeapps)
  - [3. 页面右下角选择`网上应用店`](#3-%E9%A1%B5%E9%9D%A2%E5%8F%B3%E4%B8%8B%E8%A7%92%E9%80%89%E6%8B%A9%E7%BD%91%E4%B8%8A%E5%BA%94%E7%94%A8%E5%BA%97)
  - [4. 搜索`greasemonkey`,如图:](#4-%E6%90%9C%E7%B4%A2greasemonkey%E5%A6%82%E5%9B%BE)
  - [5. 点击安装,完成安装后在如图位置会出现一个图标](#5-%E7%82%B9%E5%87%BB%E5%AE%89%E8%A3%85%E5%AE%8C%E6%88%90%E5%AE%89%E8%A3%85%E5%90%8E%E5%9C%A8%E5%A6%82%E5%9B%BE%E4%BD%8D%E7%BD%AE%E4%BC%9A%E5%87%BA%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%9B%BE%E6%A0%87)
  - [6. 点击`获取新脚本`跳转到一个页面,在当前页面中点击途中位置](#6-%E7%82%B9%E5%87%BB%E8%8E%B7%E5%8F%96%E6%96%B0%E8%84%9A%E6%9C%AC%E8%B7%B3%E8%BD%AC%E5%88%B0%E4%B8%80%E4%B8%AA%E9%A1%B5%E9%9D%A2%E5%9C%A8%E5%BD%93%E5%89%8D%E9%A1%B5%E9%9D%A2%E4%B8%AD%E7%82%B9%E5%87%BB%E9%80%94%E4%B8%AD%E4%BD%8D%E7%BD%AE)
  - [7. 会跳转到Greasy Fork的搜索页,在搜索框中输入`userscript+`点击`enter`](#7-%E4%BC%9A%E8%B7%B3%E8%BD%AC%E5%88%B0greasy-fork%E7%9A%84%E6%90%9C%E7%B4%A2%E9%A1%B5%E5%9C%A8%E6%90%9C%E7%B4%A2%E6%A1%86%E4%B8%AD%E8%BE%93%E5%85%A5userscript%E7%82%B9%E5%87%BBenter)
  - [8. 在出现的结果中选择](#8-%E5%9C%A8%E5%87%BA%E7%8E%B0%E7%9A%84%E7%BB%93%E6%9E%9C%E4%B8%AD%E9%80%89%E6%8B%A9)
- [其他](#%E5%85%B6%E4%BB%96)
- [介绍一下VIP视频破解脚本用法](#%E4%BB%8B%E7%BB%8D%E4%B8%80%E4%B8%8Bvip%E8%A7%86%E9%A2%91%E7%A0%B4%E8%A7%A3%E8%84%9A%E6%9C%AC%E7%94%A8%E6%B3%95)
  - [1. 首页点击`会员` !这里写图片描述](#1-%E9%A6%96%E9%A1%B5%E7%82%B9%E5%87%BB%E4%BC%9A%E5%91%98-%E8%BF%99%E9%87%8C%E5%86%99%E5%9B%BE%E7%89%87%E6%8F%8F%E8%BF%B0)
  - [2. 随便选择一个视频 !这里写图片描述](#2-%E9%9A%8F%E4%BE%BF%E9%80%89%E6%8B%A9%E4%B8%80%E4%B8%AA%E8%A7%86%E9%A2%91-%E8%BF%99%E9%87%8C%E5%86%99%E5%9B%BE%E7%89%87%E6%8F%8F%E8%BF%B0)
  - [3. 视频播放窗口左上角可以切换通道(部分通道可能无法播放,不过选择超多) !这里写图片描述](#3-%E8%A7%86%E9%A2%91%E6%92%AD%E6%94%BE%E7%AA%97%E5%8F%A3%E5%B7%A6%E4%B8%8A%E8%A7%92%E5%8F%AF%E4%BB%A5%E5%88%87%E6%8D%A2%E9%80%9A%E9%81%93%E9%83%A8%E5%88%86%E9%80%9A%E9%81%93%E5%8F%AF%E8%83%BD%E6%97%A0%E6%B3%95%E6%92%AD%E6%94%BE%E4%B8%8D%E8%BF%87%E9%80%89%E6%8B%A9%E8%B6%85%E5%A4%9A-%E8%BF%99%E9%87%8C%E5%86%99%E5%9B%BE%E7%89%87%E6%8F%8F%E8%BF%B0)

> 关于greasemonkey(油猴)的安装和一些实用脚本推荐

## 步骤

准备工作:确保你的电脑可以科学上网
以本人的chrome浏览器为例

### 1. 打开一个新标签页

### 2. 地址栏输入`chrome://apps/`

### 3.  页面右下角选择`网上应用店`

### 4.  搜索`greasemonkey`,如图:
![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905220548620.png)

### 5.  点击安装,完成安装后在如图位置会出现一个图标
![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905220938865.png)

### 6.  点击`获取新脚本`跳转到一个页面,在当前页面中点击途中位置
![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905221214234.png)

### 7.  会跳转到Greasy Fork的搜索页,在搜索框中输入`userscript+`点击`enter`

### 8. 在出现的结果中选择
![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905221514070.png)


## 其他
>[greasemonkey(油猴子介绍)](https://zh.wikipedia.org/zh/Greasemonkey)
>简单说是一个可以安装当前正在浏览页面可用的额外功能的脚本,举个栗子:非会员在优酷视频无法观看会员视频,而安装油猴子之后再安装了userscript+脚本就可以自动在当前页面检测可用的脚本(可用脚本的提示将会出现在页面右下角,点击即安装)

## 介绍一下VIP视频破解脚本用法
用优酷举例吧,直接上图
### 1.  首页点击`会员` ![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905223840097.png)
### 2. 随便选择一个视频 ![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905223857412.png)
### 3.  视频播放窗口左上角可以切换通道(部分通道可能无法播放,不过选择超多) ![这里写图片描述](https://lestat.b0.upaiyun.com/blog/20170905223911820.png)
本文仅供心得交流,请自觉购买会员支持正版!
关于`科学上网`请自行baidu
