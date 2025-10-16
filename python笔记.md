多数软件版本号一般分为三段，形如A.B.C，A表示大版本号，B表示功能更新，C表示小的改动。

## ***变量***

常用和**变量**类型相关的函数：

*   `int()`：将一个数值或字符串转换成整数，可以指定进制。

*   `float()`：将一个字符串（在可能的情况下）转换成浮点数。

*   `str()`：将指定的对象转换成字符串形式，可以指定编码方式。

*   `chr()`：将整数（字符编码）转换成对应的（一个字符的）字符串。

*   `ord()`：将（一个字符的）字符串转换成对应的整数（字符编码）。

## ***运算符***

| 运算符                                                                  | 描述              |
| :------------------------------------------------------------------- | :-------------- |
| `[]`、`[:]`                                                           | 索引、切片           |
| `**`                                                                 | 幂               |
| `~`、`+`、`-`                                                          | 按位取反、正号、负号      |
| `*`、`/`、`%`、`//`                                                     | 乘、除、模、整除        |
| `+`、`-`                                                              | 加、减             |
| `>>`、`<<`                                                            | 右移、左移           |
| `&`                                                                  | 按位与             |
| `^`、\`                                                               | \`              |
| `<=`、`<`、`>`、`>=`                                                    | 小于等于、小于、大于、大于等于 |
| `==`、`!=`                                                            | 等于、不等于          |
| `is`、`is not`                                                        | 身份运算符           |
| `in`、`not in`                                                        | 成员运算符           |
| `not`、`or`、`and`                                                     | 逻辑运算符           |
| `=`、`+=`、`-=`、`*=`、`/=`、`%=`、`//=`、`**=`、`&=`、`\|=`、`^=`、`>>=`、`<<=` | 赋值运算符           |

*   ***海象运算符*** “**：=**” ，将运算符右侧的值赋给左边的变量，运算符右侧的值也是整个表达式的值。

```python
print((a:=10)) # 10
print(a) #10
```

*   \*\*\*短路原理，\*\*\*如果根据运算符左侧已经能判断出表达式结果，则右侧不被执行

***

***

## ***分支结构***

1.  常见的有**if，elif，else**语句。
2.  使用**match和case**构造分支结构

    ```python
    status_code = int(input('响应状态码: '))
    match status_code:
        case 400: description = 'Bad Request'
        case 401: description = 'Unauthorized'
        case _: description = 'Unknown Status Code'
    print('状态码描述:', description)
    ```

&#x20;     说明：带有\*\_的case语句在代码中起到通配符的作用，如果前面的分之都没有匹配上，\*代码就会来到case\_，它只能放在分支结构的最后面，如果他后面还有其他分支，这些分支将是不可达的。

&#x20;     ***合并模式***：将几种归入一个分支，如下：

```python
status_code = int(input('响应状态码: '))
match status_code:
    case 400 | 401: description = 'Invalid Request'
print('状态码描述:', description)
```

## ***循环结构***

### **for-in语句**

```python
"""
每隔1秒输出一次“hello, world”，持续1小时
"""
import time
for i in range(3600):   #构造出一个从0到2599的范围
    print('hello, world')
    time.sleep(1)
```

*   `range(101)`：可以用来产生`0`到`100`范围的整数，需要注意的是取不到`101`。
*   `range(1, 101)`：可以用来产生`1`到`100`范围的整数，相当于是左闭右开的设定，即`[1, 101)`。
*   `range(1, 101, 2)`：可以用来产生`1`到`100`的奇数，其中`2`是步长（跨度），即每次递增的值，`101`取不到。
*   `range(100, 0, -2)`：可以用来产生`100`到`1`的偶数，其中`-2`是步长（跨度），即每次递减的值，`0`取不到。

例：从1-100偶数求和代码：

```python
total = 0
for i in range(1, 101):
    if i % 2 == 0:       # 判断是否为偶数
        total += i
print(total)
```

```python
total = 0
for i in range(2, 101, 2):     # 起始值和跨度改为2
    total += i
print(total)
```

```python
print(sum(range(2, 101, 2)))    # Python内置sum函数求和
```

### **while循环**

如果要构造循环结构但不能确定循环次数，推荐用while循环。

实例：

```python
"""
从1到100的偶数求和
"""
total = 0
i = 2
while i <= 100:
    total += i
    i += 2
print(total)
```

### **break和continue**

*   break可以终止它所在的那个循环，让循环停下来。（在嵌套循环中使用时需要注意）
*   continue可以用来放弃本轮循环后续代码，直接让循环进入下一轮。

    示例：

    ```python
    """
    从1到100的偶数求和
    """
    total = 0
    for i in range(1, 101):
        if i % 2 != 0:
            continue      #用continue调过来i是奇数的情况
        total += i
    print(total)
    ```

### **循环结构的应用**

*   例1：输入一个大于1的正整数，判断他是不是素数。

```python
num = int(input('请输入一个正整数: '))
end = int(num ** 0.5)       # 在2~根号m的范围内寻找
is_prime = True
for i in range(2, end + 1):
    if num % i == 0:
        is_prime = False
        break
if is_prime:
    print(f'{num}是素数')
else:
    print(f'{num}不是素数')
```

*   例2：输入两个大于 0 的正整数，求两个数的最大公约数。

```python
# 一般算法（数字大时效率低）
x = int(input('x = '))
y = int(input('y = '))
for i in range(x, 0, -1):          # 倒序步长为1去寻找
    if x % i == 0 and y % i == 0:
        print(f'最大公约数: {i}')
        break
```

```python
# 欧几里得算法
x = int(input('x = '))
y = int(input('y = '))
while y % x != 0:
    x, y = y % x, x         # y % x得到的余数替换原来的x
print(f'最大公约数: {x}')
```

**欧几里得算法：**

核心定理：两个整数的最大公约数等于其中较小的数与两数相除余数的最大公约数。

**即：用较小的数去除较大的数，然后用余数替换较大的数，直到余数为 0。​**

*   随机生成数函数randrange

    ```python
    import random
    i = random.randrange(1,101)
    # 导入了Python标准库的random模块，其中的randrange函数生成了1到101范围的随机数（不包含101）
    ```

*   函数语法：

    ```python
    random.randrange(start,stop=None,steo=1)
    ```

    *   **start**​（可选）: 起始值（***包含***），默认从 `0` 开始。
    *   ​**stop**​（必填）: 结束值（***不包含***），生成的随机数小于此值。
    *   ​**step**​（可选）: 步长（间隔），默认 `1`。

### **分支与循环练习：见Vs code**

### 正整数的反转代码

```python
num = int(input('num = '))
reversed_num = 0
while num > 0:
    reversed_num = reversed_num * 10 + num % 10
    num //= 10
print(reversed_num)
```

