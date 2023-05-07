

# Python基础

## 数据类型

## 面试题

### 1.python新式类和经典类的区别？

a. python2中默认的都是经典类，只有显示的继承了object才是新式类，python3中默认的都是新式类，不需要再显示的继承object；

b. 新式类的实例可以直接通过\__class__属性获取自身类型，与type的输出相同，即新式类保持了class和type的统一；

c. 在多重继承时属性搜索顺序不一样，新式类是广度优先搜索，经典类是深度优先搜索；

d. 新式类增加了\__getattribute__方法，可以获取类的属性和方法；

e. 新式类增加了\__slots__属性，可以把实例属性的种类锁定到slots规定的范围之中。

> 通常每一个实例都会有一个\__dict__属性，用来记录实例中所有的属性和方法，也是通过这个字典，可以让实例绑定任意的属性
>
> 而\__slots__属性的作用就是，当类有比较少的变量，而且拥有slots属性时，那么类的实例就没有dict属性，而是把变量的值存在一个固定的地方。如果试图访问一个slots中没有的属性，实例就会报错。
>
> 这样的操作有什么好处呢？\__slots__属性虽然令实例失去了绑定任意属性的便利，但是因为每一个实例都没有dict属性，却能有效节省每一个实例的内存消耗，有利于生成小而精干的实例。

### 2.python中内置的数据结构有几种？

- 不可变数据类型：数字、字符串、元组
- 可变数据类型：列表、字典、集合

### 3.什么可以作为字典的键？

字典中的键可以是元组，但不能为列表，因为元组是不可变的，而列表是可变的。python中要求字典的键是不可变的，如字符串、数字或元组，而值则可以是任意的数据类型。

### 4.python如何实现单例模式，并写出实现方式？

a. 第一种方式：使用装饰器

```python
def singleton(cls):
    instances = {}

    def wrapper(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]

    return wrapper


@singleton
class Foo(object):
    pass


foo1 = Foo()
foo2 = Foo()
print(foo1 is foo2)
```

b. 第二种方法：因为\__new__方法是真正用来创建实例的，所以可以重写父类的new方法来实现单例

```python
class Singleton(object):
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
        return cls._instance


class Foo(Singleton):
    pass


foo1 = Foo()
foo2 = Foo()
print(foo1 is foo2)
```

c. 第三种方法：调用实例对象实际上是调用了类中的\__call__方法，那么使用类创建实例时就是在调用类，即调用了元类的call方法，因为元类时创建类的类，这样就可以通过修改元类的call方法来实现单例

```python
class Singleton(type):
    _instance = None

    def __call__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Singleton, cls).__call__(*args, **kwargs)
        return cls._instance


class Foo(metaclass=Singleton):
    pass


foo1 = Foo()
foo2 = Foo()
print(foo1 is foo2)
```

