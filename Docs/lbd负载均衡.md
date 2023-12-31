### lbd 检测负载均衡

在Kali Linux中，LBD（Load Balancing Detector）是一种用于检测负载均衡器的工具。它可以帮助发现潜在的负载均衡设备，并识别后端服务器的地址。LBD可以用于渗透测试和网络安全评估，特别是在测试负载均衡器的配置和安全性方面。

> - 负载均衡是建立在网络结构之上的，它提供了一种廉价有效透明的方法扩展网络设备和服务器的带宽，增加吞吐量，加强网络数据处理能力、提高网络的灵活性和可用性；
>
> - 负载均衡（Load Balance）其意思就是分摊到多个操作单元上进行执行，例如Web服务器、FTP服务器、企业关键应用服务器和其它关键任务服务器等，从而共同完成工作任务。
>
> - 负载均衡从其应用的地理结构上分为本地负载均衡（Local Load Balance）和全局负载均衡（Global Load Balance，也叫地域负载均衡）：
>
>   - **本地负载均衡**：是指对本地的服务器群做负载均衡；
>   - **全局负载均衡**：全局负载均衡是指对分别放置在不同的地理位置、有不同网络结构的服务器群间作负载均衡。
>
>   **即针对DNS：同一个域名对应多个IP地址（智能DNS，DNS轮询）；**
>   **针对于web的服务负载均衡经常使用Nginx、Apache应用层负载均衡；**

lbd工具：

> - 大型网站为了解决海量访问问题，往往采用负载均衡技术，将用户的访问分配到不同的服务器上。网站的负载均衡可以从DNS和HTTP两个环节进行实施。在进行Web渗透测试的时候，需要先了解网站服务器结构，以确定后期的渗透策略。Kali Linux提供工具lbd来获取网站的负载均衡信息。该工具可以根据DNS域名解析、HTTP服务的header和响应差异，来识别均衡方式。
> - PS：由于用户所使用的线路不同，获取的输出结果不同。大家可以把运行结果和其他人的做比较，以发现目标网站的更多服务器。

```bash
命令：lbd www.baidu.com
命令：lbd mail.163.com
```

