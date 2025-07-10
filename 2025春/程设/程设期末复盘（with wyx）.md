# 2025 春 程设



## 基础篇

### 特别注意

1. python中的/除法结果都是float，不管是否可以整除。表达式中出现小数，结果也是小数。注意题目要求，需要时要通过 int() 进行强制类型转换。

### isinstance(x,type):

判断x是否为type的类型

### is 和 ==

a is b：表示a和b指向的地址相同

a==b：表示a和b的值相同，但是地址不一定相同

a=b：会使a指向b的位置(浅拷贝)

```python
a=[1,2,3,4]
b=[1,2,3,4]
print(a==b)  # True
print(a is b)  # False
c=a
print(c is a)  # True
```

注意is和==的区分基本只集中在list和dict中，其他不可变的数据类型其实是相同的，例如tuple：

```python
a=(1,2,3)
b=(1,2,3)
print(a==b)  # True
print(a is b)  # True
```

### 整数数据类型

0b为2进制；0x为16进制；0o为八进制。

### True and False

True等价于1；False等价于0。

其他的都是相当于的关系，而非相同

False： ”” ； [] ， {} 。

**注意：**

```python
True==1  # True
False==0  # True
False==""  # False
True==2  # False
```

### 浮点数

1. 浮点数判等：

   ```python
   import sys
   def equal_float(a,b):
   	return abs(a-b)<=sys.float_info.epsilon
   ```

   即可以使用sys.float_info.epsilon（表示最小浮点数间隔）来判断两个float是否相同。sys.float_info中存储着许多有关浮点数的标度，可以进行参考。

2. 取整与舍入

   四舍五入：round( float , ndigits = None) ：四舍五入到第ndigits位，默认情况下是到整数

   下取整：math.floor(number)

   上取整：math.ceil(number)

3. 数的自动装箱：

   可以直接对一个数使用点操作，例如：

   ```python
   print(13.00.is_integer()) # True
   ```

### 高精度浮点数decimal.Decimal

不想看，感觉没用

### 类型转换

1. int( x , [ , base ] )： 基于base进制将字符串转化为int整型数。例如：print(int(”10”,8))  打印8。
2. float(x)：将字符串x转化位浮点数
3. str(x)：将对象x转化为字符串
4. repr(x)：将对象x转化为可执行的字符串
5. chr(x)：将整数转换为字符
6. ord(x)：将字符转换为整数编码值(16位)

### 输入和输出

str=input() 函数可以读入一行字符串

通过str.split()可以将多项同行输入分开

print(str , end=” ”) 输出str，以空格作为结尾，如果不写end这个参数，默认为换行

print(x , y , z) 连续输出多项，以空格作为间隔

输出控制可以使用和cpp相同的方法：`print("666%s%d" % ("name"s,10))`

也可以使用f-string: print( f ”a is {a:.4f} ” )这样也可以控制有效位数和串内表达式

使用sys.stdin=open(” t.txt ”,”r”)和sys.stdout=open(” d.txt ”,”w”)可以进行输入输出的重定向

### 交换两个变量

python中提供元组交换，这样写更为简洁：

```python
a,b=1,2
a,b=b,a
print(a,b)  # 2 1
```

### for循环语句还可以在最后else一下

```python
for i in range(5):
    print(i)
else:
    print("Done")
```

如果循环顺利结束，即没有在中间被break掉，就可以执行else里面的东西。

```python
for i in range(5):
    print(i)
    if i==4:
        break
else:
    print("Done")
```

例如这样就不会执行打印 ”Done” 的操作。

### range函数

在使用for循环时，我们通常会使用range函数打底。

range( start , end , step)：可以只传入一个参数，表示步长为1，从0开始，直到end-1为止。如果传入两个参数，则是设置了start和end，默认步长仍为1，构建一个[ start , end )的一组数。如果传入三个数则按步长从起点开始，直到下一个数不在[ start , end )范围内为止。当然，值得注意的是，range函数返回的不是list，而是一个range对象，其中有一个迭代器进行循环。可以使用list将其强制转换为list类型。

### 字符串操作

1. **一个字符串的索引是[ - len ( str ) , len ( str ) - 1 ]的**
2. **字符串反转，最常用的方法是str[::-1]，使用reverse函数要注意先将str转化为list才行**
3. 字符串是不可修改的
4. r ” ans\n123 ” ：不转义的字符串
5. **可以使用 in 和 not in 判断子串**
6. 可以使用 eval(str) 函数执行str中的表达式，例如str=”1+2”这种
7. **可以使用count函数统计子串出现的数量，例如：str.count( sub )**
8. 可以使用len()函数得到一个字符串的长度
9. **可以使用str.find(sub)和str.rfind(sub)分别表示从左向右和从右向左查找子串位置，如果找到则返回子串第一个字符在主串中的index值，如果没有则返回-1**
10. 可以使用str.index(sub)和str.rindex(sub)实现上述相同的效果，但是如果找不到则抛出异常
11. 可以使用str.replace( sub , later )将sub部分替换成later
12. 可以使用 isdigit() , islower() 和 isupper()来判断是否为数字、小写字母和大写字母
13. 字符串的格式化：（使用format控制）

```python
x="Hello {0} {1:>10}, you get ${2:0.4f}".format("Mr.","Jack",3.2)
```

{ 序号：宽度.精度.类型 } ，使用>表示右对齐，<表示左对齐，^表示居中

1. 使用%作为print函数的输出控制：

   %s为字符串；%d为整数；%f为小数；%.nf表示输出一个小数，保留小数点后n位，四舍六入，五则是都有可能

   注意这种使用方法需要在字符串末尾使用%表明字符中需要输出量是什么，例如： `print("我的身高为%.2f" % 1.8345)  #输出：我的身高为1.83`

### Python字符串和字节流的互相转换（我没看懂）PPT 89页

### tuple元组

元组的内容不能修改，但是元组中的元素如果是引用类型（例如list），那这个元素的内容是可以修改的

元组也可以像str和list一样使用+进行拼接，使用*进行迭代

### list列表

1. 可以使用 `del list_name[index]` 对list中某一个元素进行删除（用remove会更好一些的感觉）
2. **列表生成式（可以加入多条循环语句和判断语句）**

```python
lst=[x*y for x in range(1,11) for y in range(1,11) if y%2==0 if isinstance(x,int)]
print(lst)
```

1. **使用lst.append(value)函数添加一个元素**

2. 使用lst.extend(list)添加其他表中的元素（会被依次填进去，和+差不多）

3. **使用lst.insert(index,value)表示在index处插入一个value，原值向后依次移动**

4. 使用lst.remove(value)可以删掉第一个出现的value值

5. **使用lst.reverse()可以使列表颠倒（直接在lst上操作）**

6. 使用lst.index(value)可以返回第一次出现value值得索引

7. 使用len(lst)可以返回lst的长度

8. **使用map函数进行列表和元组的相关操作：**

   map( function , sequence )：将sequence按照function的映射结果返回，返回值仍然是一个map的数据结构

   ```python
   lst=[1,2,3]
   print(list(map(lambda x: x*2,lst))) # [2, 4, 6]
   ```

   map可以吸收多个lst，只需要保证映射关系也吸收相同多的参数即可。

9. 可以使用类似的filter( function , sequence ) ：由function对数据进行筛选，返回值是filter。

10. 可以使用functools库中的reduce(function , sequence , startValue)进行累积求和。方法如下所示：

    ```python
    for x in sequence:
    	startValue=function(startValue,x)
    return startValue
    ```

11. 构造二维数组，不要使用*累乘，因为引用相同的问题，导致修改值时会修改到不希望修改的位置。可以使用如下方法构建：

    ```python
    lst2d=[[0 for _ in range(3)] for _ in range(3)]
    print(lst2d)
    ```

### lambda表达式

标准写法是

```
func=lambda 变量:返回值
```

这等价于

```python
def func(变量表):
	return 返回值
```

### 列表的排序

1. new=sorted(lst)，这个排序不会改变原lst的顺序

2. lst.sort()，这个排序会直接在lst上进行

3. 可选参数reverse，默认为False，即从小到大排序，设置为True就会从大到小排

4. **可选参数key，这个十分重要，自定义了排序的规则**

   key需要吸收一个list中的元素，返回一个变换后希望进行比较的形式。返回值可以是一个元组或列表，表示比较的优先级，优先级高的放在前面。

   python的排序是稳定的，所以如果很多元素有相同的key，他们不会出现顺序改变的情况。

### 列表的拷贝

对于全是基础数据类型的list，我们可以直接使用`b=a[:]`实现深度拷贝，但是如果a中存在list等引用类型的变量，在使用：拷贝时，仍然只复制了他们的引用，所以没有实现深拷贝。

可以使用copy库中的`b=copy.deepcopy(a)`函数进行深度复制。

列表的计算中，`a=a+[…]` 会重新构建一个a，如果有b=a，b的值并不会改变。

而`a+=[…]` 则会改变原有的a

### 字典

定义格式为

```
dict={key1:value1,key2:value2}
```

1. `dict.clear()`方法用来清空一个字典
2. `in`操作符可以判断左值是否在字典的key中
3. `dict.keys()` 返回字典键值的集合(set)
4. `dict.items()` 返回字典元素的集合
5. `dict.values()` 返回字典中值的集合
6. `dict2=dict1.copy()` 实现了浅拷贝，如果value都是基本类型和深拷贝没有区别
7. `dict2=copy.deepcopy(dict1)` 实现了深拷贝

### 集合set

1. `a={}` 或定义为`a={1,2,3,"ok",(1,2,3)}`
2. 两个集合之间可以使用 &求交；| 求并；- 求差
3. 使用`set.update(str/lst)`可以是str或lst分开并加入到set中
4. 使用`set.remove(val)` 可以删掉set中的元素，如果没有该元素就会报错；`discard`函数也可以，没有时不会报错

### 函数

1. 参数个数不定的函数

   ```python
   def PrintAll(*b):
   	print(b)
   ```

   这里b是一个元组

   另外一种方法是：

   ```python
   def Function(**b):
       print(b)
   Function(a1=1,a2=2,a3=3)
   dict={"a1":1,"a2":2,"a3":3}
   Function(**dict)
   ```

   在这里b就是一个字典

2. 全局变量和局部变量

   ```python
   x=100
   def func():
       global x
       print(x) 
       x=10
   func() # 100
   print(x) # 10
   ```

   如果一个函数中改变了一个全局变量，需要在函数内声明glabol，否则会出现错误。类似于JS中的TDZ死域报错。

3. 使用`exit()`函数可以退出程序

### Object类：面向对象编程

1. 使用class定义一个类，所有类都派生自object类

2. 每一个类可以定义一些具有固定功能的成员函数，主要包括：

   `__init__` 构造函数；`__eq__` ==；`__lt__` <

   `__le__` ≤；`__ge__` ≥；`__gt__` >；`__ne__` ≠

   `__str__` 将class强制转化为str

   `__repr__` 强制转化为python可执行的字符串

   `__del__` 析构函数

3. 注意python的成员变量是可以随时添加的，类似于JS中object的语法，可以在外面随意添加

4. 静态方法和类方法：

   1. 静态方法使用`@staticmethod` ，写法参数表中不可以有`self`参数
   2. 类方法使用`@classmethod` ，参数表中第一个参数应该是`cls` ，就表示本类

5. 私有属性：使用`__name` 定义一个私有属性，这个属性在外面是不能访问的，但是可以使用`_cls__name`进行访问

6. 使用`property` 为一个类增加属性，使用`propertyName=property(get,set)` 就可以得到类中的一个属性

   还有另一种定义`property`的方法，使用`@property` 修饰一个函数，函数名就是属性名，可以为其设置一个`@propertyName.setter` ，后面的函数就是设置函数，名字也是属性名

### 函数式编程

1. 注意函数可以赋值给变量  `f=abs`  ，同样这样的函数变量可以传入其他函数的参数表

2. 函数的闭包

   ```python
   def func(x):
   	def g(y):
   		nonlocal x
   		x+=1
   		return x+y
   	return g
   ```

   使用`nonlocal` 就可以在函数内改变函数外的变量赋值

### 迭代器

1. 使用`for i in x` ，就可以遍历对象x，但是要求对象x是一个可迭代对象。迭代对象必须实现override两个方法：`__iter__()` 和`__next__()` 。`__iter__()` 方法返回对象本身，`__next__()` 方法返回下一个元素。

2. 在list中使用迭代器，例如以下这段代码

   ```python
   x=[1,2,3,4]
   it=iter(x)
   while True:
       try:
           print(next(it))
       except StopIteration: # 迭代器的最后就会抛出这个错误
           break
   ```

3. 自定义的迭代器

   ```python
   class Myrange:
       def __init__(self , end):
           self.idx=0
           self.end = end
       def __iter__(self):
           return self
       def __next__(self):
           if self.idx<self.end:
               val = self.idx
               self.idx+=1
               return val
           else:
               raise StopIteration
   for x in Myrange(10):
       print(x)
   ```

4. 对于仅实现了`__getitem__`方法没有实现`__iter__`方法的对象x，`iter(x)`会返回一个Python创建的迭代器，迭代器的next方法去调用x的`__getitem__`

### 生成器

生成器是一种延时求值对象，内部包含计算过程，真正需要时才完成计算，例如 `a=(i*i for i in range(5))` ，a是生成器，其内容还未生成。

1. 使用yield定义生成器：使用了 yield 的函数被称为生成器（generator）。当函数被调用的时候，并不执行函数，而是返回一个迭代器(iterator)。如果 X 是一个生成器被调用时的返回值（迭代器)，则next(X) 执行生成器中的语句，直到碰到yield语句为止，并且返回 yield语句中的对象。如果碰不到yield语句函数就结束了，则抛出异常。例如：

   ```python
   def generate():
       yield 1
       yield 2
       yield (1,2)
   it=generate()
   while True:
       try:
           print(next(it))         # 逐行打印generate中的3个数据
       except StopIteration:
           break
   ```

2. 使用生成器计算斐波那契数列：

   ```python
   def Fobi(n):
       a,b,count=0,1,0
       while count <= n:
           yield a
           a,b=b,a+b
           count+=1
   ```

   运行这个函数会得到一个对应数量的迭代器，可以逐步计算斐波那契数列的值

3. 用`send`向`yield`语句传送数据，没有执行`next`或`send(None)`前，不能`send(x)` (x非None)；send是给上一个已经执行的yield前面的变量赋值。PPT 224页例子

### try-except-finally语句（没啥好说的，按照规范写就行）

PPT 236页

### 装饰器

```python
def good(func):
    def wrapper(*args):
        print("%s called" % func.__name__)
        return func(*args)+5
    return wrapper
@good
def mysum(a,b,c):
    return a+b+c
print(mysum(1,2,3))  #这时mysum(1,2,3)等价于good(mysum)(1,2,3)
```

使用装饰器扩展函数的功能，另外装饰器还可以带有参数：

```python
def good(var):
    def decorator(func):
        def wrapper(*args):
            print("%s called" % func.__name__)
            return func(*args)+var
        return wrapper
    return decorator
@good(10)
def f(x,y):
    return x+y
print(f(10,20))
```

还可以使用对象作为装饰器：

```python
class decorator(object):
    def __init__(self, x):
        self.x = x
    def de(self,func):
        def wrapper(*args):
            print("%s is called" % func.__name__)
            return func(*args)+self.x
        return wrapper
dec=decorator(1)
@dec.de
def mysum(a,b,c):
    return a+b+c
print(mysum(1,2,3))  # 7
dec.x=7
print(mysum(1,2,3))  # 13
```

其实装饰器就是以累可以吸入一个函数作为参数，又返回一个函数作为结果的函数，通过@函数名的形式嵌套在我们希望执行的函数之前，这样就可以扩展函数的功能

### 文件读写（和C++一样混乱）

首先需要打开一个文件，执行`f=open("file_name_and_root","r or w or a")` ，其中后面的r表示只读，w表示可以写，a表示在文件中添加内容（如果没有就新建）。

使用`f.write(str)` 可以将str写入文件f中；使用`f.readlines()` 读取文件f的全部内容；使用`f.readline()` 读取文件f的一行；最后应该使用`f.close()` 关闭文件夹。

`open`函数中有`encoding`可选参数，规定了文件的编码方式，一般使用utf-8的编码方式。

### 基础部分到此为止了

感觉也没啥东西

## beautifulsoup部分

速度是正则表达式的约几分之一

要使用beautifulsoup库，首先就是要了解网页源代码的样式，例如“tag”的书写方式

tag的格式通常为：

```python
<X(tag的名字） attr1 =’’ attr2=’’ attr3=’’…>

text(具体的内容）

</X>

# 少数的没有text和最后的尾标
```

总的来说，一般就是名字+属性及其值+文本+尾标

另外，tag可以嵌套，即一个tag的text内可以包含另一个tag

导入beutifulsoup库：

```python
import bs4
```

使用的大致逻辑如下：

1. 将html文档装入一个BeautifulSoup对象X

   1. 法一： html文档来自字符串：

      ```python
      str = '''
       <div id="siteHeader" class="wrapper">
       <h1 class="logo">
       <div id="topsearch">
       <ul id="userMenu">
       <li><a href="<http://openjudge.cn/>">首页</a></li>
       </div>
       </div>
       ''' 
      # 带href的<a>都是链接, 上面 “首页” 是链接文字,  href后面
      # <http://openjudge.cn是链接地址>
      soup = bs4.BeautifulSoup(str,"html.parser")
      print(soup.find("li").text) 
      #>> 首页
      
      # 个人加强版：
      import bs4
      str = '''
       <div id="siteHeader" class="wrapper">
       <h1 class="logo">
       <div id="topsearch">这是<ul id="userMenu">我的<li><a href="<http://openjudge.cn/>">首页</a></li>对吗
       </ul>
       </div>
       </div>
       '''
      # 带href的<a>都是链接, 上面 “首页” 是链接文字,  href后面
      # <http://openjudge.cn是链接地址>
      soup = bs4.BeautifulSoup(str,"html.parser")
      print(soup.find("div").text)  # 这是我的首页
      
      # 可以大致观察到输出的逻辑是从高级到低级逐级的嵌套时，就按照text出现的顺序来依次连接输出
      ```

   2. 法二：来自于文件：

      ```python
      import bs4
      soup = bs4.BeautifulSoup(open("D://trial-cache/ATLÉTICO DE MADRID 2024.html","r",encoding="utf-8"), "html.parser")
      print(soup.find("title"))
      ```

   3. 法三：来源于获取url(实时爬虫）

      ```python
      import requests
      import bs4
      def getHtml(url):
       #获得html文本
          try:
              r = requests.get(url)
              r.raise_for_status()
              r.encoding = r.apparent_encoding
              return r.text
          except:
              return ""
      
      html = getHtml("<https://cn.bing.com/dict/search?q=new>")
      soup = bs4.BeautifulSoup(html, "html.parser")
      print(soup.find("title"))
      ```

2. 用X对象的find, find_all等函数去找想要的tag对象

   其实上面已经大致可以探索出如何去查找，就是根据这个tag的名称去find

   其实大致理解tag在html中是一个嵌套结构的存在后，我们后面就是具体看如何快速高效的筛选出我们想要的tag及其包含的信息

   示例：

   ```python
   import bs4
   soup = bs4.BeautifulSoup(open("d://trial-cache/ATLÉTICO DE MADRID 2024.html",
    encoding = "utf-8"),"html.parser")
   # diva = soup.find("div", attrs={"id":"synoid"})
   # #寻找名为"div", 且具有 值为"synoid"的属性"id"的tag
   diva = soup.find("section")
   if diva != None:  #如果找到
       for x in diva.find_all("header", attrs={'id':"newHeader"}):
           print(x.text)  #在diva内部继续找
   
           print(x["id"])
   ```

3. 对找到的tag对象, 还可以用其find, find_all函数去找它内部包含（嵌套）的tag对象

4. tag对象的text就是该对象里的正文(text), tag对象也可以看作是一个字典, 里面包含各种属性(attr)及其值

## 数据分析与可视化

## 0. 基础-Numpy

所有元素类型必须相同，

经常用于处理高维向量、矩阵

![05b856ab87dd999406787a28dbd3f8a.png](attachment:62f0ce69-faaa-4bbc-9d9d-0a0226795572:05b856ab87dd999406787a28dbd3f8a.png)

range和linespace大体类似，细微区别是range左闭右开，而linespace两端都闭，且range第三个参数是步长的直接指定，而linespace则指定等分数

```python
print(np.random.randint(10,20,[2,3]))
#生成2行3列的随机整数矩阵
#>>输出 [[12 19 12]
#[19 13 10]]
print(np.random.randint(10,20,5)) 
#生成5个[10,20)的随机整数
#>>输出 [12 19 19 10 13]

# 左闭右开
```

![35ddb9030db50c6fa6c10ef1843a084.png](attachment:61b797d8-8a96-4f73-9609-dd4596c88a88:35ddb9030db50c6fa6c10ef1843a084.png)

这上述的一些变形都是用拷贝去完成，重新赋值给一个新变量，不影响原数组

这本质上也是体现，numpy创建的数组本身的”形式“不能变动，（但可以具体修改元素值）

增删的函数（following）事实上也是整出来新的：

![9f56049844b3cdc52e54c046b9ed097.png](attachment:82ac6170-84bb-45c6-818e-9218bce2d28a:9f56049844b3cdc52e54c046b9ed097.png)

numpy数组的数学运算几乎是自然定义：

就是逐元素的运算

两个数组相加相乘也对应到对应元素的运算

**切片**：

注意切片与上述的其他函数和变换不同，切片操作本质上可以看作一种局部的”视图“，是原数组的一部分, 而非一部分的拷贝

## pandas部分

主要就是dataframe的构造和访问

处理二维数组

**核心功能是在二维表格上做各种操作, 如增删, 修改,求一列数据的和, 方差, 中位数, 平均数等 需要numpy支持 如果有openpyxl或xlrd或xlwt支持, 还可以读写excel文档 最关键的类：DataFrame, 表示二维表格**

重要的类：Series

是一维表格, 每个元素带标签且有下标,

data是数据，index存储标签

兼具列表和字典的访问形式，即既可以用标签，也可以用下标

切片操作会改变下标；另外切片的范围也是左闭右开

```python
s['体育'] = 110 #在尾部添加元素, 标签为'体育', 值为110
s.pop('数学')   
#删除标签为'数学'的元素
s2 = s._append(pd.Series(120, index = ['政治'])) 
#不改变s
```

DataFrame是带行列标签的二维表格, 每一列都是一个Series

相当于dataframe再加上一个参数，即columns = ?

这个？本身需要是一个一维数组，作为和index等同的一种”标签“,只不过出现为行，而index出现在最左的一列

选择一行/列(逗号后的第二个参数）：

\#iloc[行选择器, 列选择器] 用下标做切片 #loc[行选择器, 列选择器] 用标签做切片

df.loc（参数是这一行的index）

iloc相应的就是某行对应的下标（第n行即n-1）

下例对行列切片举例明之：

![daec06b1acfa81382fcbdfbe3fc2ccb.png](attachment:bbdc71fe-3047-4962-bafc-6812e63a39ad:daec06b1acfa81382fcbdfbe3fc2ccb.png)

**分析统计：**

1. .T 行列转置
2. drop，去除某一行/列，传axis=0/1
3. sort_values(第一个参数传按什么数据比，第二个ascending=false降序，true升序）
4. inplace=True：表示直接在原DataFrame上进行修改, 而不是返回一个新的排序后的DataFrame
5. min,max返回单纯的数据；而minarg,maxidx则返回行号、标签
6. 修改和增删几乎是平凡的：就直接按索引指示为左值，然后右边赋上新值即可

**读写excel/csv:**

需要Openpyxl (对.xlsx文件) 或 xlrd或xlwt支持(老的.xls文件)

读/写

yjm:

做题过程中补充：

1. 关于输出格式控制

只能对字符串进行操作，

在字符串中用%.nf代替这个位置上需要保留的小数

最后在”“外面补上%然后（ ， ， ）括号内逗号隔开你需要用的变量

（要注意这个是四舍六入）

另一种方法（适用于更详细的格式控制）：用format函数，直接对字符串进行格式化，最后再输出返回后的字符串

这个需要在原来字符串的对应位置按如下格式挖空：

{序号（第n个空位就是n-1)：宽度.精度.类型}

在最后.format(” “,” “,…)

还有一种较简单的方法：

f”  {a:.4f}…{b:.3f}  … “

1. join可以很好的满足中间插入的格式需求，例如’,’.join(a)，a是一个list
2. 创建n个元素的数组： a = [0] *n，下标是0 - n-1
3. 