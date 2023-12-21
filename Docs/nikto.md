### nikto

Nikto是一个基于Web的漏洞扫描器，它是用`perl`语言编写的开源软件。这些工具的主要目标是进行漏洞扫描。

该工具扫描站点上常见的6，800个漏洞。该工具还从未打补丁的站点扫描250个平台。还在网络服务器文件中发现一些漏洞。

```bash
-config+  使用此配置文件

-Display    打开/关闭显示输出

-dbcheck  检查数据库和其他关键文件的语法错误

-Format    保存文件（-o）格式

-help    扩展帮助信息

-host    目标主机/URL

-id      要使用的主机身份验证，格式为id:pass或id:pass:realm

-list-plugins    插件列出所有可用的插件

-output  将输出写入此文件

-nossl   禁用使用SSL

-no404   禁用404检查

-plugins    要运行的插件列表（默认值：ALL）

-port    要使用的端口（默认值为80）

-root    将根值前置到所有请求，格式为/directory

-ssl     在端口上强制ssl模式

-timeout 请求超时（默认为10秒）

-Update  从CIRT.net更新数据库和插件

-version 打印插件和数据库版本

-vhost   虚拟主机（用于主机标头）
-useproxy 使用代理服务进行扫描
```

查看详细帮助信息

```
man nikto#查看详细帮助信息

nikto -H #查看详细帮助信息
```

插件升级

```bash
nikto -update #升级插件
```

查看已有插件

```bash
nikto -list-plugins #查看插件已有信息
```



基本扫描

```bash
nikto -h baidu.com
nikto -host baidu.com
```

指定协议扫描

```bash
nikto -h baidu.com -ssl
```

指定端口扫描

```bash
nikto -h baidu.com -port 80,443,445
```

忽略某些HTTP代码

```bash 
nikto -h baidu.com -no404
```

使用代理服务器扫描

```bash
nikto -h baidu.com -userproxy http://proxy.example.com:8080
```

使用认证信息进行扫描

```bash
nikto -h https://www.example.com -id admin:password
```

扫描指定目录

```bash
nikto -h https://www.example.com -root /admin/
```

扫描指定文件类型

```bash
nikto -h https://www.example.com -filetype php
```

扫描指定漏洞

```bash
nikto -h https://www.example.com -plugins vulnerabilities
```

参考：https://www.xjx100.cn/news/436786.html?action=onClick