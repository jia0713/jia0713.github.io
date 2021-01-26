---
layout: article
title: 一台新VPS的处置
mathjax: true
tags: 技术 linux系统
---


拿到一台新的VPS，按照顺序执行下面几件事情

1. **更改SSH端口：**

   22端口很容易被攻击，如果刚好密码设置的比较简单，就会被轻易的控制。CentOS控制SSH登陆的文件位置是：`/etc/ssh/sshd_config`， 用vim编辑这个文件，找到`Port=22`字段，修改为自定义的端口即可。操作成功后重启SSH服务：`service sshd restart`

2. **VPS测速脚本：**

    ```shell
    wget -qO- bench.sh | bash
    ```
    显示本机测试信息，并且提供了全球多处测速中心的测速数值。

3. **VPS回程路由脚本：**

    ```shell
    wget https://raw.githubusercontent.com/nanqinlang-script/testrace/master/testrace.sh
    bash testrace.sh
    ```
    VPS线路测试必备，可以看出详细的回程路由

4. **一键梯子脚本：**

    V2ray一键脚本:
    ```shell
    wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh

    ```

    Trojan自带用户管理一键脚本：
    ```shell
    source <(curl -sL https://git.io/trojan-install)
    ```
