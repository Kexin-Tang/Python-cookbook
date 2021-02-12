- [基本数据结构](#基本数据结构)
  - [list](#list)
  - [tuple](#tuple)
  - [set](#set)
  - [dict](#dict)
- [流程控制](#流程控制)
  - [循环](#循环)
    - [for](#for)
    - [while](#while)
  - [条件](#条件)
  - [遍历](#遍历)
- [函数](#函数)
  - [函数参数传递](#函数参数传递)
  - [参数](#参数)
  - [匿名函数(lambda)](#匿名函数lambda)
- [迭代 &amp; 生成](#迭代--生成)
- [面向对象](#面向对象)
    - [基本概念](#基本概念)
    - [class的定义与使用](#class的定义与使用)
    - [保护&私有](#保护私有)
      - [保护](#保护)
      - [私有](#私有)
    - [继承&覆写](#继承覆写)
    - [多态](#多态)
    - [`__slots__`](#__slots__)
    - [@property & @setter](#property--setter)
    - [多重继承](#多重继承)

# 基本数据结构
## list
* 定义的时候使用`[]`，内部可存放各种数据类型，且可以存放重复的元素
> ```py
> myList = ['tom', 18, 'jerry', 'tom']
> ```

* 添加/删除元素
> * 添加元素
>   * list.append(`ele`) -- 在末尾直接添加一个元素
>   * list.insert(`pos`, `ele`) -- 在`pos`位置添加一个元素`ele`
> * 删除元素
>   * del list[`pos`] -- 删除`pos`上的元素，<u>可以使用切片删除其中一段</u>
>   * list.pop(`pos=-1`) -- 弹出`pos`位置上的元素，<u>默认为最末位的元素</u>，且可以将该弹出的元素赋值给其他variable
>   * list.remove(`ele`) -- 删除**首个**匹配到内容为`ele`的元素

* 排序
> * list.sort() -- 永久<b>升序</b>排序list，可用<u>reverse=True</u>反向排序
> * sorted(`list`) -- 临时升序排序list，源list并不会改变
> * list.reverse() -- **永久**反转list的元素内容，如[a, b, c]&rarr;[c, b, a]

* 列表长度
> * len(list) -- 获取列表长度(元素个数)

* 列表解析
> ```python
> square = [value**2 for value in range(1, 11)] # 产生1~10的平方
> ```

* 计数
> list.count(`ele`) -- 计算`ele`出现的次数

* 返回索引
> list.index(`ele`) -- 返回第一个`ele`的索引

* 切片
> * listName[`start=0`: `end=len(listName)`]将会取<b>`[start, end)`</b>的元素，start默认为头部，end默认为尾部
> * 可以使用`-1`等来从尾部开始计算选取元素

* [**直接赋值 Vs 浅拷贝 Vs 深拷贝**](https://www.runoob.com/w3cnote/python-understanding-dict-copy-shallow-or-deep.html) [[More Details and Example]](https://zhuanlan.zhihu.com/p/54011712)
> * 赋值 -- 类似于C++中引用，就是给一个内存区域换了个名字而已
> * 浅拷贝有三种方式
>   * 切片 -- `data2 = data1[:]` or `data2 = [i for i in data1]`
>   * 工厂函数 -- `data2 = list(data1)`
>   * copy()函数 -- `data2 = data1.copy()`
> * 深拷贝只有一种方式 -- `data2 = copy.deepcopy(data1)`

> **总结** 
>   1. 外层添加元素时，浅拷贝不会随原列表变化而变化；内层添加元素时，浅拷贝才会变化。
>   2. 无论原列表如何变化，深拷贝都保持不变。
>   3. 赋值对象随着原列表一起变化。
```py
import copy

# 不可变对象
print("<=====对不可变对象tuple中的可变对象进行更改=====>")
t1 = (1, 2, [3, 4])

t2 = t1                 # 直接赋值
t3 = t1[:]              # 浅复制
t4 = copy.deepcopy(t1)  # 深复制

t1[2].append(5)
print(t1, t2, t3, t4)

print("<=====对不可变对象tuple赋予新的值=====>")
t1 = (1, 2, [3, 4])

t2 = t1                 # 直接赋值
t3 = t1[:]              # 浅复制
t4 = copy.deepcopy(t1)  # 深复制

t1 = (1, 2, 3)
print(t1, t2, t3, t4)

# 可变对象
print('<=====对可变对象list进行更改=====>')
l1 = [1, 2, [3, 4]]

l2 = l1                 # 直接赋值
l3 = l1[:]              # 浅复制
l4 = copy.deepcopy(l1)  # 深复制

l1.append(5)
print(l1, l2, l3, l4)

print('<=====对可变对象list内部的可变对象进行更改=====>')
l1 = [1, 2, [3, 4]]

l2 = l1                 # 直接赋值
l3 = l1[:]              # 浅复制
l4 = copy.deepcopy(l1)  # 深复制

l1[2].append(5)
print(l1, l2, l3, l4)

```
![tuple.jpg](https://i.loli.net/2021/02/10/tev4TMDWnAiGxIf.jpg)
![list.jpg](https://i.loli.net/2021/02/10/5SPs31MHTYADLzF.jpg)

* `+`拼接 -- 多个列表可以通过`+`进行拼凑

## tuple
* 定义的时候使用`()`，内部元素不得修改<i>(但是可以将整个变量重新赋值)</i>
> ```py
> data = (1, 2, 3)
> data[0] = 4       # error
> data = (4, 2, 3)  # ok
> ```

* 基本操作与list保持一致

* 虽然不可以更改，但是可以使用列表list作为元素
> ```py
> myData = ('tom', 18, ['red', 'blue'], 'tom')
> myData[2].append('yellow')
> ```

* 可以使用`+`拼接，可以切片，可以使用索引随机访问

* 构造0个和1个元素的语法比较奇葩
> ```py
> data = ()     # 0个元素
> data2 = (1, ) # 1个元素时必须要加上逗号，不加逗号会被认为是括号+元素 => 单个变量
> ```

## set
* 定义时使用`{}`或者`set()`来进行，不可重复元素，无序(基于hash，不可索引)
> 注意，创建空集合时不能使用`{}`，因为这会创建一个空字典

* 增加/删除元素
> * 增加
>   * set.add(`ele`) -- 更新一个值，如果该值已经存在，则不做任何操作
>   * set.update(`ele`) -- `ele`可以是一个值，也可以是字典、列表、原则等，要注意<u>更新后并不会保存源格式</u>
>   ```py
>   data = {1, 2}
>   data.update([3,4], [5,6])   # {3,5,6,4,1,2}
>   data.update({'tom': cat})   # {3,5,6,4,1,2,'tom'}
>   ```
> * 删除
>   * set.remove(`ele`) -- 删除一个元素，如果不存在则报错
>   * set.discard(`ele`) -- 删除一个元素，不存在则忽略该步骤

* set可以使用集合运算，如交、并、补等

## dict
* 创建时使用`{key: value}`的形式，可以保存任意形式元素，但是`key`必须是独一无二的
* 访问方法`myDict[key]`，删除元素使用`pop(myDict[key])`
* `key`必须独一无二不可变化，所以不能使用list
* 常用函数
> * dict.get(`key`, `default`) -- 返回指定键的值，如果键不在字典中返回default设置的默认值
> * dict.items() -- 返回key-value对的tuple
> * dict.keys() / dict.values() -- 返回键/值的迭代器，可用list()转换成列表
> * dict1.update(`dict2`) -- 可以将`dict2`添加到`dict1`中

---

# 流程控制
## 循环
### for
* 基本语法
> ```py
> for item in items:
>   pass
> ```

* `range()`能够轻松的产生一串内容
> * `range(a, b)`将会生成<b>`[a, b)`</b>的内容
> * `range(start, end, step)`可以指定步长
> * `list(range(start, end))`可以生成list内容

* `for...else...` -- 如果`for`中条件满足，则执行`for`的，否则执行`else`
> ```py
> for i<5:
>   i+=1
>   ...
> else:
>   ...
> ```

### while
* 基本语法
> ```py
> while condition:
>   pass
> ```

* `while...else...`的语法同上

## 条件
* 基本语法
> ```py
> if condition1:
>   ...
> elif condition2:
>   ...
> else:
>   ...
> ```

## 遍历
* 遍历dict中键值对
```py
for k, v in dict.items():
    pass
```
* 遍历时取出索引和内容
```py
for idx, value in enumerate(list):
    pass
```
* 遍历多个数据结构
```py
for q, a in zip(questions, answers):
    pass
```
* 按序遍历但是不改变原数据
```py
for i in sorted(list):
    pass
```

---

# 函数
## 函数参数传递
1. 可更改(mutable)对象
    * 包括list，set，dict等
    * 在函数中做参数传递时，类似C++中的引用传参，即函数内对其做了操作也会影响函数外的值
2. 不可更改(immutable)对象
    * strings,tuples和numbers是不可更改的对象
    * 类似C++的值传递，传递的只是值。如果需要进行更改，需要进行return返回
```py
def func(dataList, num):
    num += 1
    dataList.append(num)

data = [1, 2, 3]
num = 3
func(data, num)

print(data, num)    # [1,2,3,4] 3
```

## 参数
* 默认参数
> ```py
> def func(a, b, c=0):
>     pass
> ```

* 不定长参数
> * `*`的定义方式中，参数会以tuple的形式被加载，即要求传递**位置参数**
> ```py
> def func(a, *b):
>   print(b)
>
> func(1, 2, 3) # (2,3)
> ```
> * `**`的定义方式中，参数会以dict形式被加载，在传递参数时需要使用`param = value`的形式，即要求传递**关键字参数**
> ```py
> def func(a, **b):
>   print(b)
>
> func(1, a=2, b=3) # {'a': 2, 'b': 3}
> ```

* 强制位置参数 *(Python > 3.8.0)*
> * 在`/`前面的参数必须使用**位置形参**；在`*`后面的参数必须使用**关键字形参**，中间的参数可以随意
> ```py
> def func(a,b,/,c,d,*,e,f):
>   pass
> func(1,2,3,d=4,e=5,f=6)   # 正确调用方法
> ```

## 匿名函数(lambda)
1. lambda 只是一个表达式，函数体比 def 简单很多。
2. lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
3. lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
4. 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。
5. lambda的语法`lambda [arg1 [,arg2,.....argn]]:expression`
```py
square = lambda x: x**2
square(2)   # 4
```

---

# 迭代 &amp; 生成
* 任何定义了`.__iter__()`和`.__next__()`的对象都可以成为可迭代对象，如list, dict, tuple等
* 使用`iter()`将可迭代对象转换为迭代器，然后使用`next()`访问下一个元素<b>(迭代器只能从前往后，不可以随机访问)</b>
> ```py
> data = [1,2,3]
> it = iter(data)
> # 循环遍历
> for i in it:
>   print(i)
> # 迭代器迭代
> while True:
>   print(next(it))
> ```

* 使用了`yield`的函数称为生成器，生成器可以视为一个迭代器。在调用生成器运行的过程中，每次遇到`yield`时函数会暂停并保存当前所有的运行信息，返回`yield`的值, 并在下一次执行`next()`方法时从当前位置继续运行。
> ```py
> import sys
> def fibonacci(n):
>   a, b, cnt = 0, 1, 0
>   while True:
>       if(cnt>n):
>           return
>       yield a
>       a, b = b, b+a
>       cnt+=1
> f = fibonacci(10)
> while True:
>   try:
>       print(next(f), end="")
>   except StopIteration:
>       sys.exit()
> ```

---

# 面向对象
### 基本概念
* 属性：类内定义的数据参数
* 方法：类内定义的函数
* 对象：实例化的类
* 重写/覆写：如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写
* 继承：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待
* 实例属性与类属性
> ```py
> class Stu(object):
>   type = "Student"            # 类属性，所有Stu类均可访问，是公共属性
>   def __init__(self, name):
>       self.name = name        # 实例属性，每个对象的实例属性都是独立的
> s = Stu("smith")
> t = Stu("tom")
>
> print(s.name, s.type, Stu.type)   # smith Student Student
> print(t.name, t.type, Stu.type)   # tom   Student Student
>
> s.type = "Teacher"
> print(s.type, Stu.type, t.type)   # Teacher Student Student
>
> Stu.type = "Teacher"
> print(Stu.type, t.type)   # Teacher Teacher
> ```
  

### class的定义与使用
> ```py
> class Student:
>   name="tom"
>   def func(self):
>       pass
>
> stu = Student()   # 实例化
> print(stu.name)   # 访问属性
> print(stu.func()) # 使用方法
> ```

* `__init__(self, [params])`是一个会在实例化类的时候自动调用的方法，其中`self`代表了实例化的对象，在每个类内方法中都必须置于第一个参数的位置

### 保护&私有
|   继承类型    | 对象访问权限 | 子类访问权限 |
| :-----------: | :----------: | :----------: |
| 公有(default) |   可以访问   |   可以访问   |
|     私有      |   不可访问   |   不可访问   |
|     保护      |   不可访问   |   可以访问   |

#### 保护
* 对于保护属性和保护方法，需要加上**单下划线**，如`self._protected`
* 受保护的属性和方法不能在对象中使用，但可以在类内或者子类中使用/访问
* Pyhon不像C++一样真正提供了保护，而是**伪保护**--实际上实例化对象仍然可以访问属性和方法，但是不建议这么做

#### 私有
* 对于私有属性和私有方法，需要加上**双下划线**，如`self.__private`
* 私有的属性和方法不能再对象中使用，也不能被子类继承
* Python不像C++一样真正的提供了私有，而是**伪私有**--实际上可以通过`_className__attribute`来进行访问，但是不建议这么做

### 继承&覆写
```py
class Animal:
    def __init__(self, age):
        self.age = age
    def show(self):
        print(self.age)

class Dog(Animal):
    def __init__(self, age, name):
        super().__init__(self, age)
        self.name = name
    def show(self):
        print(self.name, self.age)
```
* 子类继承父类的时候，需要在类名后加上父类的名称，如`class Dog(Animal)`
* `super()`是一个特殊函数。使用该函数可以在创建子类的时候自动调用父类的初始化函数，并初始化父类中的属性
* **覆写** -- 当子类中出现父类的同名方法，则在调用时，子类方法会覆盖父类方法，如上述代码调用`show()`时会打印`name`和`age`
* 父类和子类要定义在同一个文件中

### 多态
```py
def showAge(animal):
    print(animal.age)

showAge(Animal())
showAge(Dog())
```
* 可以使用`isinstance(instance, class)`来判断某个实例化对象是否属于某个类
> ```py
> isinstance(Animal(), Animal)  # True
> isinstance(Dog(), Animal)     # True
> isinstance(Animal(), Dog)     # False
> isinstance(Dog(), Dog)        # True
> ```
> 一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类。但是，反过来就不行。

* 函数只要定义了参数为某个类的类型，那么该类和其子类都可以共用该函数。即一个函数可以不作修改，根据传入的class类别输出不同的内容
> ```py
> class Animal(object):
>   def __init__(self):
>       pass
> class Dog(Animal):
>   def __init__(self, name):
>       super().__init__(self)
>       self.name = name
>   def run(self):
>       print(self.name + " is running...")
> class Tortoise(Animal):
>   def __init__(self, name):
>       super().__init__(self)
>       self.name = name
>   def run(self):
>       print(self.name + " is running slowly...")
>
> dog = Dog('dog')
> tor = Torroise('tor')
>
> def run(Animal):
>   Animal.run()
>
> run(dog)  # "dog is running..."
> run(tor)  # "tor is running slowly..."
> ```

* 调用方只管调用，不管细节，而当我们新增一种子类时，只要确保方法编写正确，不用管原来的代码是如何调用的

* 静态语言 VS 动态语言
  * 在静态语言中（如Java，C++），如果某函数定义参数为`Animal`类型，那么传入的参数必须为`Animal`或者`Animal`的子类
  * 在动态语言中（如Python），如果某函数定义参数为`Animal`类型，而传入的参数可以为别的类型，但是要求该class有该函数定义中的各种方法和属性即可<i>(长得像鸭子，叫声像鸭子，走路像鸭子&rarr;一只鸭子)</i>

### `__slots__`
在动态语言中，可以给class绑定额外的属性和方法，为了限制绑定的内容，可以使用`__slots__(attr1, attr2, ...)`

<u>(注意：使用前后双下划线的某些方法有特殊作用，如`__str__`, `__getitem__`, `__iter__`)</u>
```py
class Stu:
    __slots__('name', 'age')
    ...
s = Stu()
s.name = 'tom'  # OK
s.grade = 88    # Error, __slots__ does not have 'grade'
```

### @property & @setter
* 在类中，比如定义了一个属性叫做`self.__score`，但是不希望在类外暴露该属性，那么需要再定义一个获取的函数`getScore(self)`和一个设置的函数`setScore(self, value)`，但是这样过于复杂。于是可以使用**装饰器**
```py
class People(object):
    @property
    def birth(self):
        return self.__birth
    @birth.setter
    def birth(self, day):
        self.__birth = day
    
    @property
    def age(self):
        return 2021-self.__birth

t = People()
t.birth = 2000  # 相当于调用t.birth(2000)
print(t.birth)  # 相当于调用t.birth()
t.age           # 21
t.age = 21      # 报错，因为age被设置为只读属性
```
* 通过只设置`@property`，可以将属性设置为**只读**

### 多重继承
* 比如要定义一个`Dog`class，那么需要定义其为`Mammal`+`Runnable`，因此可以使用如下的多重继承
```py
class Dog(Mammal, Runnable):
    ...
```
* 一般而言设置继承会有一个主线，比如从Animal&rarr;Mammal&rarr;Dog，那么Runnable需要作为旁路插入，此时Runnable被称为MixIn
