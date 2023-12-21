### Nmap

参考地址：

- https://blog.csdn.net/qq_29277155/article/details/50977143

#### 漏洞扫描

**http拒绝 服务**

```bash
nmap --max-parallelism 800--script http-slowloris XXX.XXX.com
```

**IIS短文件泄露**

```bash
nmap -p 8080 --script http-iis-short-name-brute 10.9.75.1
```

**ftp弱口令暴力破解**

```
nmap --script ftp-brute --script-args brute.emptypass=true,ftp-brute.timeout=30,userdb=/root/用户名字典路径/usernames.txt,brute.useraspass=true,passdb=/root/密码字典路径/passwords.txt,brute.threads=3,brute.delay=6 10.9.75.3
```

**检测CVE-2011-2523中的ftp-vsftpd-backdoor**

```bash
nmap -T2 --script ftp-vsftpd-backdoor 10.9.75.3
```

**验证http中开启的-methods 方法**

```bash
nmap -T3 --script http-methods --script-args http.test-all=true,http.url-path=/www.haoshangjia.com
```

 **验证HTTP.sys 远程代码执行**

```bash
nmap -sV --script http-vuln-cve2015-1635 10.9.75.3
```

**验证 SSL POODLE information leak**

```bash
nmap -sV -p 443 --version-light --script ssl-poodle 10.9.75.3
```

**验证http 中开启了put 方法**

```bash
nmap --script http-put --script-args http-put.url=/uploads/testput.txt,http-put.file=/root/put.txt 10.9.75.3
```

 **验证mysql 匿名访问**

```bash
nmap --script mysql-empty-password 10.9.75.3
```

**验证cve2014-8877漏洞**

```bash
nmap -Pn --script http-vuln-cve2014-8877 --script-args http-vuln-cve2014-8877.cmd=dir,http-vuln-cve2014-8877.uri=/wordpress 10.9.75.3
```



 **验证Cisco ASA中的CVE-2014-2126,CVE-2014-2127,CVE-2014-21,CVE-2014-2129漏洞**

```bash
nmap -p 443 --script http-vuln-cve2014-2126,http-vuln-cve2014-2127,http-vuln-cve2014-2128,http-vuln-cve2014-2129 10.9.75.3
```



**验证低安全的 SSHv1，sslv2协议**

```bash
nmap --script sshv1,sslv2 www.haoshangjia.com
```



 **验证CVE-2014-0224 ssl-ccs-injection**

```bash
nmap -Pn --script ssl-ccs-injection 10.9.75.3
```



 **验证ssl-cert证书问题**

```bash
nmap -v -v --script ssl-cert 10.9.75.3
```



**验证SSL证书的有限期**

```bash
nmap -Pn --script ssl-date www.XXXx.com
```



**验证CVE-2014-0160 OpenSSL Heartbleed bug**

```bash
nmap -p 443 --script ssl-heartbleed,ssl-known-key 10.9.75.3
```

 **验证 Debian OpenSSL keys**

```bash
nmap -p 443 --script ssl-known-key 10.9.75.3
```



**验证弱加密SSL套件**

```bash
nmap --script ssl-enum-ciphers 10.9.75.3
```

**验证多种SSL漏洞问题**

```bash
nmap 10.9.75.3 --vv --script sshv1,ssl-ccs-injection,ssl-cert,ssl-date,ssl-dh-params,ssl-enum-ciphers,ssl-google-cert-catalog,ssl-heartbleed,ssl-known-key,sslv2
```

**在网络中检测某主机是否存在窃听他人流量**

```bash
nmap --script sniffer-detect 10.10.167.5
```

**精准地确认端口上运行的服务**

```bash
nmap -sV --script unusual-port 10.10.167.5
```



nmap脚本主要分为以下几类，在扫描时可根据需要设置--script=类别这种方式进行比较笼统的扫描：

- **auth**: 负责处理鉴权证书（绕开鉴权）的脚本 
- **broadcast**: 在局域网内探查更多服务开启状况，如dhcp/dns/sqlserver等服务  
- **brute:** 提供暴力破解方式，针对常见的应用如http/snmp等  
- **default**: 使用-sC或-A选项扫描时候默认的脚本，提供基本脚本扫描能力  
- **discovery**: 对网络进行更多的信息，如SMB枚举、SNMP查询等  dos: 用于进行拒绝服务攻击  
- **exploit**: 利用已知的漏洞入侵系统  
- **external**: 利用第三方的数据库或资源，例如进行whois解析  
- **fuzzer**: 模糊测试的脚本，发送异常的包到目标机，探测出潜在漏洞 
- **intrusive**: 入侵性的脚本，此类脚本可能引发对方的IDS/IPS的记录或屏蔽  
- **malware**: 探测目标机是否感染了病毒、开启了后门等信息  
- **safe**: 此类与intrusive相反，属于安全性脚本  
- **version**: 负责增强服务与版本扫描（Version Detection）功能的脚本  
- **vuln**: 负责检查目标机是否有常见的漏洞（Vulnerability）

```bash
Nmap提供的脚本命令行参数如下：
-sC: 等价于--script=default，使用默认类别的脚本进行扫描。    
--script=<Lua scripts>: <Lua scripts>使用某个或某类脚本进行扫描，支持通配符描述   
--script-args=<n1=v1,[n2=v2,...]>: 为脚本提供默认参数   
--script-args-file=filename: 使用文件来为脚本提供参数   
--script-trace: 显示脚本执行过程中发送与接收的数据   
--script-updatedb: 更新脚本数据库   
--script-help=<Lua scripts>: 显示脚本的帮助信息，其中<Lua scripts>部分可以逗号分隔的文件或脚本类别。
```

