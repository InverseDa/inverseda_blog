---
title: Go的Proxy问题
date: '2023-01-08 00:00:01'
tags: 
- 环境配置
categories:
- Go
toc: true
---

### 设置GOPROXY代理：

  ```bash
  go env -w GOPROXY=https://goproxy.cn,direct
  ```

### 设置GOPRIVATE来跳过私有库，比如常用的Gitlab或Gitee，中间使用逗号分隔：

  ```bash
  go env -w GOPRIVATE=*.gitlab.com,*.gitee.com
  ```
<!--more-->
  