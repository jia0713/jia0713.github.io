---
layout: article
title: linux系统安装软件包
mathjax: true
tags: 技术 linux系统
---

linux系统安装软件包，分两种情况

1. 当系统是debian, ubantu的情况, 安装包是`.deb`文件:

   ```shell
   sudo dpkg -i package_name.deb
   ```

2. 当系统是centos, redhat的情况，安装包是`.rpm`文件：

   ```shell
   sudo rpm -ivh package_name.rpm
   ```
