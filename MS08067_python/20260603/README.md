<details>
<summary>信息搜集</summary>

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

</details>

<details>
<summary>漏洞探测</summary>

```
AWVS(Acunetix Web Vulnerability Scanne):通过爬虫
NESSUS：系统扫描和分析软件，提供主机漏洞扫描服务
AppScan：安装在windows系统上，对Web应用进行漏洞扫描和安全测试
```

</details>

<details>
<summary>漏洞验证</summary>

```
在公开资源寻找漏洞：乌云镜像网站、Google Hacking、渗透代码网站、通用应用漏洞、厂商漏洞警告
可自己搭建乌云镜像站，WooYun.ory
```

</details>

----------------------------------------------------------------------------

<details>
<summary>python 序列</summary>

```
----------------------------------------------------------------------------
列表list = [,]
添加单个元素： .append() //尾部添加
添加列表： .extend() //尾部添加
指定位置添加： .insert(7, )

删除列表首次出现元素： .remove()
删除并返回列表中指定的下标元素： .pop() //默认值为-1，是最后一个 | .pop(0) //返回第一个元素

返回指定元素在列表中出现的次数：.count() //元素对应出现的次数

将列表中的所有元素逆序： .reverse()
对列表中的元素进行排序： .sort(key=str,reverse=False) //key指定排序依据，reverse决定升序False,降序True
----------------------------------------------------------------------------
元组 tuple = (,)
元组(,)与列表[,]不同，元组属于不可变序列
----------------------------------------------------------------------------
字典dic = {键：值,} //键不能重复，值可以重复
通过dict()创建字典： lab = dict(,)
修改字典中的元素： dic['键']=修改值
添加字典新元素： dic['']='' //保持先进后出，新添加的一直在第一个后出，最后输出
返回字典中的元素：.items()
删除字典中元素： del dic['键']
----------------------------------------------------------------------------
```

</details>


<details>
<summary>python 控制结构</summary>

```
顺序结构、选择结构、循环结构
----------------------------------------------------------------------------
选择结构
#!/user/bin/pyton
#coding:utf-8
studentScore = int(input('Scores of students: '))
if (studentScore < 60):
  print('不及格‘）
if (60 <= studentScore < 80):
  print('良好‘）
if (strdentScore >= 80):
  print('优秀')
----------------------------------------------------------------------------
循环结构：for循环一般用于有明显边界范围的情况，while循环一般用于循环次数难以确定的情况
#！/usr/bin/python
#coding:utf-8
Sum = 0
for i in range(1,101):
    Sum = Sum + i
else:
    print('Sum = ', Sum)

运行结果：5050

#!/usr/bin/python
#coding:utf=8
x = int(input('x='))
Sum = 0
while x != 0 :
    Sum = Sum + x
    x = x - 1
else:
    print('Sum=', Sum)

输入100，运行结果：5050
输入1000，运行结果：500500
----------------------------------------------------------------------------

</details>

<details>
<summary>文件处理</summary>

```
数据库文件、图像文件、音频文件、视频文件、文本文化等

----------------------------------------------------------------------------
文本文件：常规字符串，由文本行组成，每行通常由换行符'\n'结尾，读取、写入、删除、修改，关闭并保持

open(file[,mode='r'[,buffering=-1]])
//mode:打开后的处理方式，读模式、写模式、追加模式、二进制模式、文本模式、读写模式
//buffering:缓存模式，0:不缓存、1:使用行缓存模式、>1:缓存区的大小，默认值为-1；
//二进制文件和非交互文本文件以固定大小的块为缓冲单位，等价于io

----------------------------------------------------------------------------
对文件操作：读写、写入、追加、设置二进制模式、文本模式、读写模式

w:写入模式  文件存在，清空；文件不存在，创建
x:写入模式  创建新文件；文件存在，抛出异常
a:追加模式  也是写入模式的一种，不覆盖文件的原始内容

r: 读模式（默认模式，可省略），文件不存，抛出异常
+：读写模式
>>> f = open('demo.txt', 'r')
>>> print(f.readline()) //读取第一行内容
>>>
>>> print(f.read()) //读取全部
----------------------------------------------------------------------------
f.close() //关闭文件对象
关键字with 能够自动管理资源，总能保证文件正确关闭，并且在代码执行后自动还原开始执行代码块时的现场
>>> with open('demo.txt','a') as f:
...     f.write('hello ') //继续追加
...
----------------------------------------------------------------------------
异常处理结构：提高代码的鲁棒性，提高代码的容错性
[1]try...except...结构 //判断是否
try:代码块为可能引发异常的语句
except:捕获相应的异常
当try字句代码执行异常并且被except字句捕获，执行except字句的代码块

#!/usr/bin/python
#coding:utf=8
mathScore = input('数学成绩')
try:
    mathScore = int(mathScore)
    if(0<mathScore <=100):
        pritnt("输入的数学成绩为：",mathScore)
    else:
        print("输入不在本科成绩范围内")
except Exception as e:
    print('输入的数值有误')

[2]try...except...else...结构 //判断是 和 否，否之后; 没有异常会执行else
#!/usr/bin/python
#coding:utf=8
mathScore = input('数学成绩')
try:
    mathScore = int(mathScore)
except Exception as e:
    print('输入的数值有误')
else:
    if(0<mathScore <=100):
       pritnt("输入的数学成绩为：",mathScore)
    else:
       print('请输入正确的数学成绩') 

[3]try...eccept...finally...结构，无论try子句是否正常执行，finally子句中的代码块总会得到执行
在开发，该结构通常用来做清理工作，释放try子句中申请的资源
确保程序的鲁棒性，要求带有异常处理的结构。鲁棒是指系统的健壮性，是在存在异常和危险的情况下系统生存的关键

#！/usr/bin/python
#coding:utf=8
a = int(input('a:'))
b = int(input('b:'))
try:
    div = a/b
    print(div)
except Exception as e:
    print ('The second parameter cannot be 0.')
finally:
    print('运算结果')
    
----------------------------------------------------------------------------
```

</details>

----------------------------------------------------------------------------
