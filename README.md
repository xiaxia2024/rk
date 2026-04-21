___________________________________________
#### 基于 strcpy 的栈缓冲区溢出（stack-based buffer overflow）

<details>
<summary>[1]使用安全函数strncpy替代 strcpy</summary>
  
```
strncpy(buf, argv[1], sizeof(buf) - 1);
buf[7] = '\0';
优点：
限制最大写入长度
防止溢出
强制字符串结束
```
</details>

<details>
<summary>[2]使用 snprintf（更安全)</summary>

```
char buf[8];
snprintf(buf, sizeof(buf), "%s", argv[1]);
优点：
自动截断
永远不会越界
更推荐现代写法
```
</details>

<details>
<summary>[3]长度检查（最严谨）</summary>

```
if (strlen(argv[1]) >= sizeof(buf)) {
    printf("Input too long\n");
    return 1;  //出错退出（通用错误）
}
strcpy(buf, argv[1]);
```
</details>

___________________________________________
