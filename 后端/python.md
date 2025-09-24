# Python(蟒蛇书)

## 变量和简单数据类型

**字符串**

- 大小写
  - title() 首字母大写
  - lower() 全部小写
  - upper() 全部大写
- 去除空格
  - strip() 全部去除
  - lstrip() 左 rstrip() 右

**数字**

## 列表

#### 创建列表

```python
list = [value1, value2]
```

#### 插入

```python
append()
insert()
```

#### 删除

```python
del：按位序
remove：按值
```

#### 排序

```python
sort
sorted
reverse
```

#### 求列表长度

```python
len(list)
```

#### 数值列表

```python
range(start, end, step)
sum()、min()、max()
```

**示例**

1~10 中的所有奇数

```python
list(range(1,10,2))
```

列表解析

```python
square = [value**2 for value in range(1,11)]
```

#### 切片

```python
new_list = old_list[start: end]
start 和 end 可以都为空，或者使用负数代表离末尾的距离
左开右闭，和 range 一样
```

## 元组

> 不可变的列表，但是可以通过重新赋值的方式，修改元组

#### 创建元组

```python
tuple = (value1, value2)
```

#### 修改元组

```python
tuple = (new_value1, new_value2)
```

## 条件判断语句-if

条件判断

- 与 and
- 或 or
- 非 not
- 包含 in
- 不包含 not in

if - elif - else

## 字典

#### 创建

```python
new_dict = {'key': 'value'}
```

#### 修改 / 新增

```python
new_dict['key'] = 'value'
```

#### 删除

```python
del new_dict['key']
```

#### 遍历

```python
for k, v in dict

# 只有一个参数时，默认遍历字典的 key
for k in dict 等价于 for k in dict.keys()

# 根据排序后的 key 进行遍历
for k in sorted(dict.keys())

# 遍历字典的值
for v in dict.values()
```

## 输入 / 输出

#### 用户输入

```python
input()
# 该方法读取到的是字符串，获取其它数据类型时需要使用类似 int()来进行强制类型转换
```

#### 文件

```python
# 打开
with open('file_path') as f:

# 读取
read() # 读取全部文件
readlines() # 逐行读取

# 写入
# w(w+)模式：清空/创建原有文件
with open('file_path', 'w') as f:
  f.write()
# a(a+)模式：附加/创建文件
with open('file_path', 'a') as f:

# 需要注意文件指针
# 可以使用 seek 重置指针到指定行
seek()
```

#### JSON

```python
json.dump()
json.load()
```

## 流程控制语句

#### while

当流程结束条件不明确时，才会选用 while 循环，一般都会使用 for 循环
使用场景

- list 的复制、删除
- 字典填充

#### for

#### break

> 直接退出本层循环

#### continue

> 退出本层循环的当前轮次

## 运算符

```python
** # 平方
% # 取模
```

## 函数

#### 定义

```python
def func*name(arg1, arg2):
```

#### 参数传递方式

> 引用传递

只可以修改列表、字典中的数据
也可以通过切片，禁止修改原始列表数据

> func_name(list[: ])

#### 任意数量的参数

```python
# 所有的参数都会放到一个元组中
def func_name(_arg_name):

# arg_name 为一个字典，存储所有接受到的剩余参数
def func_name(**arg_name):
func_name(user_name = 'mie', user_age = 13)
```

#### 模块化

一个文件中定义一个函数，就会自动导出。想要在另一个文件中使用时，可以通过三种方式导入

```python
import module_name
module_name.func_name()

# 或者可以使用 as 进行别名 from module_name import func_name as new_name
from module_name import func_name
func_name()

# 将所有函数全部导入，优点是不需要再写 module.func()，缺点是导入多个模块时容易产生命名冲突
from module_name import *
func_name()
```

## 类

#### 创建

```python
class ClassName():
  def __init__(self, arg1, arg2):
    # 构造函数内部
```

#### 实例化

```python
my_class = ClassName(arg1, arg2)
```

#### 继承

```python
# 使用父类的构造方法
class ClassName(PClassName)
  def __init__(self, arg1):
    super.__init__(arg1)

# 重写:直接同名方法即可
```

#### 模块化

```python
from module_name import ClassName
```

## 异常

```python
try:
  ...
except Error:
  ...
else:
  ...
finally:
  ...

pass # 失败时一声不吭
```
