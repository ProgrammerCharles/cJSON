1. struct global_hooks
2. sizeof("") == 1
3. C 库函数 size_t strlen(const char *str) 计算字符串 str 的长度，直到空结束字符，但不包括空结束字符。
4. 宏
5. cJSON.c line 185  global_hooks的定义

6. struct 的初始化
````
   parse_buffer buffer = { 0, 0, 0, 0, { 0, 0, 0 } };
````
7. whitespace and cr/lf  https://www.jianshu.com/p/8d33019d1c69


----------------------------------



|符号|意义|
|----|----|
|%d| 　　 有符号10进制整数（%ld 长整型，%hd短整型 ）|
|%hu| 　　 无符号短整形（%u无符号整形，%lu无符号长整形）|
|%i| 　　 有符号10进制整数 （%i 和%d 没有区别，%i 是老式写法，都是整型格式）|
|%o| 　　 无符号8进制整数|
|%u| 　　 无符号10进制整数|
|%x| 　　 无符号的16进制数字，并以小写abcdef表示|
|%X| 　　 无符号的16进制数字，并以大写ABCDEF表示|
|%f|　　  输入输出为浮点型 （%lf双精度浮点型）|
|%E/e| 　　 用科学表示格式的浮点数|
|%c| 　　 输入输出为单个字符|
|%s| 　　 输入输出为字符串|


----------------------------------


cJSON数据结构

````
video
    child -> name
    
name
    prev -> name
    next -> format
    
format 
    prev -> name
    next -> null

````
定义 cJSON_CreateObject(void)
调用 cJSON_CreateObject()

已跟源代码
------------------------------------
cJSON_PrintPreallocated
#### 数组
- cJSON_CreateArray
- cJSON_CreateIntArray
- add_item_to_array
- add_item_to_array NOTE line 1989