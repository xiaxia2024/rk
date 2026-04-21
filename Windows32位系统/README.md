```
void Challenge(char *str)  //接收一个字符串 str（也就是你在 main 里传进去的 buf）
{
    char temp[9]={0};  //创建一个 9字节数组，temp = [0][0][0][0][0][0][0][0][0]
    strncpy(temp,str,8);  //从 str 复制 最多8个字节 到 temp，只复制 8 字节 temp[0] ~ temp[7] 被覆盖，temp[8] 仍然是 0；｜ 只检查前8字节，后面的内容完全不管
    printf("temp=%s\n",temp);  //所以 temp 一定是：[8字节数据] + '\0'，打印 temp 内容
    if(strcmp(temp, "Please!@")==0) {   //比较：temp 是否等于 "Please!@"，，所以这里要求：temp == "Please!@"
        printf("KEY:*****");
    }
}
int main(int argc, char *argv[])
{
    char buf2[16];
    int check = 1;
    char buf[8];
    strcpy(buf2, "Give me Key!!!");  //稳定栈布局 + 干扰你判断； buf → check → buf2
    strcpy(buf,argv[1]);  //argv[1] 可控（用户输入），strcpy 不检查长度
    if(check==65) {  //strcpy 溢出 → 修改 check = 1 -> check = 65
        Challenge(buf);
    }
    else {
        printf("Check is not 65 (%d) \n Program terminated!!\n",check);
    }
    return 0;
}
```
#### [问题1】main函数内的三个本地变量所在的内存区域称为什么，它的两个基本操作是
main函数内的三个本地变量所在的内存区域称为：
```
栈区（Stack）
```
它的两个基本操作是：
```
入栈（push） 和 出栈（pop）
```
#### 【问题2】
┌──────────────┐ ① 
│     buf      │低地址
├──────────────┤ ② 
│     buf      │
├──────────────┤ ③ 
│     check    │
├──────────────┤ ④ 
│     buf2     │
├──────────────┤ ⑤
│     buf2     │高地址
└──────────────┘
#### 【问题3】应该给程序提供什么样的命令行参数值（通过argv变量传递）才能使程序执行流程进入判断语句if (check=65)...然后调用challenge()函数
```
前8字节满足：Please!@
后面可以溢出（如果题允许）Please!@\x41\x00\x00\x00
```
<details>
<summary>注释</summary>

```
注
strcpy(buf, argv[1]);
check = 65;   ← 这里已经被强制改掉
if (65)       ← 永远成立
    Challenge(buf);

前8字节必须严格匹配 "Please!@"
后续字节可以控制，但要满足：
→ 不能有 \0
→ 长度足够覆盖目标变量
→ 布局要对齐

正确内存表示（32位 int）
41 00 00 00
👉 才等于 65

AAAA = 0x41 0x41 0x41 0x41
👉 这会发生：
check = 0x41414141
0x41414141 ≠ 65
```
</details>

#### 【问题4】 上述代码所存在的漏洞名字是什么，针对本例子代码，请简要说明如何修正上述代码以修补此漏洞
```
栈溢出漏洞（Stack Buffer Overflow）

更精确一点说：
基于 strcpy 的栈缓冲区溢出（stack-based buffer overflow）

[1]使用安全函数替代 strcpy,改成 strncpy
strncpy(buf, argv[1], sizeof(buf) - 1);
buf[7] = '\0';
优点：
限制最大写入长度
防止溢出
强制字符串结束
[2]使用 snprintf（更安全）
snprintf(buf, sizeof(buf), "%s", argv[1]);
优点：
自动截断
永远不会越界
更推荐现代写法
[3]长度检查（最严谨）
if (strlen(argv[1]) >= sizeof(buf)) {
    printf("Input too long\n");
    return 1;
}
strcpy(buf, argv[1]);
```
<details>
<summary>进一步加固（防御思路升级）</summary>

```
✔ 1. 使用编译器保护
-fstack-protector-strong
-D_FORTIFY_SOURCE=2
✔ 2. 开启 ASLR / NX
ASLR：地址随机化
NX：禁止执行栈代码
✔ 3. 避免危险函数
禁止：
strcpy
gets
sprintf
```
</details>

```
问题点：
buf 只有 8 字节
strcpy 不检查长度
argv[1] 用户可控且长度不受限
```
### 解析
#### 这段代码本质上是一个典型的栈溢出（stack overflow）练习题，核心点在于：如何通过溢出修改 check 的值，从而进入 Challenge() 并触发 KEY 输出
```
//在main
char buf2[16];
int check = 1;
char buf[8];
```
#### 栈上变量布局（很关键）大致是：栈是从高地址 → 低地址增长的
```
| buf2 (16 bytes) |
| check (4 bytes) |
| buf  (8 bytes)  |
```
| 变量    | 实际大小 | 格子数        |
| ----- | ---- | ---------- |
| buf   | 8B   | 1格         |
| check | 4B   | 半格（但通常画1格） |
| buf2  | 16B  | 2格         |
#### strcpy本质：
```
while(*src != '\0'){
    *dst = *src;
    dst++;
    src++;
}
```
#### 65 的十六进制 65 = 0x41，把 check 内存改成41 00 00 00
#### 前 8 字节给 buf = Please!@，再 4 字节覆盖 check：\x41\x00\x00\x00，所以：Please!@\x41\x00\x00\x00
```
动态存储区 堆（heap），用 malloc / free 管理

main里的变量 栈区（stack）

栈的基本操作 push / pop
```
#### 什么是“动态存储区” :程序运行时才申请、用完可以释放的内存区域-->堆（heap）
```
特点:
不是编译时固定的
需要你手动申请 / 释放
生命周期由你控制

典型操作:
malloc()   // 分配空间
free()     // 释放空间

例子：
int *p = malloc(4);  // 分配4字节
free(p);             // 释放
```
#### main函数里的变量属于：栈区（stack）
```
用来存：
函数里的局部变量
参数
返回地址

自动分配（函数调用时）
自动释放（函数结束时）
速度快
空间小

push  入栈（压入数据）
pop   出栈（弹出数据）

后进先出（LIFO）
```
