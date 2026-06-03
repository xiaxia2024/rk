#### 在公开资源寻找漏洞：乌云镜像网站、Google Hacking、渗透代码网站、通用应用漏洞、厂商漏洞警告

#### 信息搜集
```
1.拿到域名后，判断域名是否存在CDN (Content Delivery Network,内容分发网络),http://ping.chinaz.com/
[1]查询IP>1,说明IP地址并不是真实的服务器地址
[2]查询IP[2,3],同时[2,3]IP地址属于同一个运营商时，可能为服务器的出口地址-->该服务器部署在内网中，，使用了不同运营商的映射进行互联网访问
[3]查询IP地址多个，并且分布在不同的地区时，基本可以确定网站就是使用了CDN的服务

绕过CDN获取真实IP信息
[1]内部邮箱
邮件服务系统都是部署在公司内部，并且咩呦经过CDN解析，可以通过目标网站的邮箱注册或订阅邮件功能，让网站的邮箱服务器给自己的邮箱服务发生邮件
查看邮件的原始邮件头，包含邮件服务器的IP地址
[2]查看域名的历史解析记录，后来加上的CDN服务，存在未使用CDN时的真实IP地址，可以通过EXAMPLE网站https://dnsdb.io/zh-cn进行查询
[3]字域名查询，子站或旁站的IP地址拆解网站的真实IP地址
[4]国外地址访问，没有多少国内的CDN服务商会进行服务    <---
[5]主域名查询，去掉www,ping域名，看是否有变化
[6]Nslookup查询
NS记录：域名服务器的记录，nslookup -qt=ns xxx.com
MX记录：mail服务的权重值，nslookup -qt=mx xxx.com
TXT记录：为某一条记录设置说明，使用nslookup -qt=txt xxx.com

2.搜集真实IP后，whois信息进行搜集 http://whois.chinaz.com/
3.确定具体信息后，查询公司有关信息，如邮箱、邮箱格式、公司员工姓名、公司人员配置等
同时在github、码云等代码托管平台查找敏感信息：包含数据库连接信息、密码、甚至网站源代码等
4.CMS建站系统，如phpcms、eshop、wordpress、dedecms、dicuz、phpweb、dvbbs、thinkphp等
指纹识别网站http://www.yunsee.cn/finger.html --->CMS信息可以查找相关的历史漏洞
```
