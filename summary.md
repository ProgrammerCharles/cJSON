1. struct global_hooks
2. sizeof("") == 1
3. C 库函数 size_t strlen(const char *str) 计算字符串 str 的长度，直到空结束字符，但不包括空结束字符。
4. 宏
5. cJSON.c line 185  global_hooks的定义
6. struct 的初始化
````
   parse_buffer buffer = { 0, 0, 0, 0, { 0, 0, 0 } };
````

1. whitespace and cr/lf  https://www.jianshu.com/p/8d33019d1c69  

|||
|----|----|
|\t |制表符tab键 | 
|\r |回车 |
|\n |回车换行
2. 文件读取  标准库   fopen fread fseek获取文件内容长度  ftell
3. 宏 (...) 可变参数
4. char '\0' === int 0
5. 调了allocate 就要调free
6. '\0'为ASCII码表第一个表项，为空字符串NUL
7. \"\\\"
8. goto关键词
9. 数值字面值占几个字节 int 4个？
10.NOTE 学习一下单元测试，测试包含了什么内容



    关于二次指针的理解
    C为值传递，函数参数为指针类型，在函数中为该指针的拷贝；函数参数为二次指针，在该函数中为该指针（原指针）

    关于指针++操作的理解 
    （前提：数组指针表示）指针指向地址，指针++操作表示指针指向的地址发生变化，所以读取的第一个元素发生变化





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


cJSON数据结构
----

````
video
    child -> name
    
name
    prev -> name
    next -> format
    
format 
    prev -> name
    next -> null


typedef struct
{
    const unsigned char *content; //将要解析的字符串
    size_t length;                //字符串长度
    size_t offset;                //从0开始; 步长1; 字符串偏移量 范围 0 -- length-1
    size_t depth; /* How deeply nested (in arrays/objects) is the input at the current offset. */
    internal_hooks hooks;
} parse_buffer;


typedef struct 
{
    unsigned char *buffer;
    size_t length;  // buffer大小
    size_t offset;  // 偏移量
    size_t depth; /* current nesting depth (for formatted printing) */ /** object嵌套深度 */
    cJSON_bool noalloc;
    cJSON_bool format; /* is this print a formatted print */
    internal_hooks hooks;
} printbuffer; //printbuffer 属性参照parse_buffer


C标准
----------------------------
fseek(file, 0, SEEK_END) 
ftell(file)
配合，可知文件内容大小，单位：字节

int sprintf(char *str, const char *format, ...) 
发送格式化输出到 str 所指向的字符串。

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

Parse
- cJSON_Parse

- parse_array

Compare 
- cJSON_Compare 
- compare_from_string

get_object_item
- get_object_item
- cJSON_IsString
- cJSON_IsArray

cJSON_Duplicate


cJson_Utils
- decode_patch_operation


方法
- cJSON_GetObjectItemCaseSensitive
    - get_object_item
    
- cJSON_Parse
    - cJSON_ParseWithOpts
    - parse_value
    - parse_string
- cJSON_Compare 
- cJSON_Minify
    - skip_oneline_comment
    - skip_multiline_comment
    - minify_string
    
其中，minify_tests值得重新看一次

- cJSON_ReplaceItemViaPointer
- cJSON_DetachItemViaPointer

misc_tests
- cJSON_AddArrayToObject
- cJSON_Delete
    
#### 对象

附
---------------
\t属于转义字符。是水平制表符，相当于键盘上的TAB按键。通常宽度相当于8个空格的位置，

input_end这样的字符指针强转为size_t类型的值，该值表示什么？