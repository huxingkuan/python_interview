# 一、Python基础

1. is和==的区别？

   is用于判断两个变量引用的对象是否是同一个，==用于判断两个变量的值是否相等。a is b 相当于id(a) == id(b)，id() 能够获取对象的内存地址，但当a=[1, 2, 3]，b=a[:]时，虽然a和b的值是一样的，但因为切片返回的是一个新的对象，所以两者的内存地址不同，因此返回False。如果定义a=10，b=10，然后再比较a is b会发现返回的是True，这是因为在Python中会创建一个小型的整形池子，范围为[-5, 256]，为这些整形开辟好内存空间，当代码中定义该范围的整型时，不会再重新分配内存地址，而是直接引用整型池中的数据。

2. 元祖和列表的区别？

   - **相同点**
     1. 在Python中都是序列类型的容器对象；
     2. 可以支持任何类型的数据存放；
     3. 都支持切片和迭代操作；
     4. 元祖可以看作是一个不可变的列表。
   - **不同点**
     1. 创建语法不同：列表使用`[]`或者`list`进行创建，而元祖使用`()`或`tuple`进行创建，并且如果元祖中只有一个元素，则需要在元素后面加上`,`；
     2. 是否可变：列表是可变数据类型，元祖是不可变数据类型；元祖是有局限的不可变，当元祖中包含列表的时候，列表中的内容是可变的；元祖不能直接进行单独的增删改操作，但是可以拼接一个新的元祖来替换之前的元祖；
     3. 支持的方法：因为元祖是不可变的，长度固定，因此在列表中的增删改方法在元祖中均没有；
     4. 拷贝：拷贝的时候，并不会开辟新的地址存放元祖，但是会开辟新的地址空间存放列表，因为元祖是不可变的，所以元祖无法复制；
     5. 存储结构：列表占用的空间更大，性能低但是存储内容可变，元祖占用空间更小，性能更高，但是存储内容不可变；
     6. 使用场景：由于元祖是可hash的，而列表是不可hash的，所以元祖可作为字典的键，但是字典不可以，元祖可以存放在集合当中，但是列表不可以；Python中的方法要返回多个值的时候应该使用元祖来进行返回。

3. try...except...finally...的用法和作用?

   try块有且仅有一个，但except块可以有多个，且每次except块都可以同时处理多种异常。当程序发生不同的意外情况时，会对应特定的异常类型，Python解释器会根据该异常类型选择对应的except块来处理该异常。首先执行try中的代码块，如果执行过程中出现异常，系统会自动生成一个异常类型，并将该异常提交给Python解释器，此过程称为捕获异常。当Python解释器收到异常对象时，会寻找能处理该异常的except块，如果找到合适的except块，则把该异常对象交给该except块处理，这个过程称为处理异常。异常处理完了以后，如果最后一个except块后面还有fnally块，则会再执行finally块中的代码。

4. 什么是Python的LEGB规则？

   

5. Python简单的列表去重怎么实现？

   - 遍历保留原顺序去重

     ```python
     old_list = [2, 3, 4, 5, 1, 2, 3]
     new_list = []
     
     for i in old_list:
         if i not in new_list:
             new_list.append(i)
     
     print(new_list)
     ```

   - 用字典dict去重

     使用列表中的元素创建一个字典，因为字典中的键不能重复，所以会自动去重，但是不能保证原来的顺序

     ```python
     old_list = [2, 3, 4, 5, 1, 2, 3]
     
     new_list = list(dict.fromkeys(old_list))
     print(new_list)
     ```

   - 用集合set去重

     利用集合中不能出现重复元素的特性，把原列表先转成集合，再转回列表可以去重，但是无法保证原来的顺序

     ```python
     old_list = [2, 3, 4, 5, 1, 2, 3]
     
     new_list = list(set(old_list))
     print(new_list)
     ```

   - 用集合set+索引去重

     ```python
     old_list = [2, 3, 4, 5, 1, 2, 3]
     
     new_list = list(set(old_list))
     # 利用原列表中元素的索引位置进行排序
     new_list.sort(key=old_list.index)
     print(new_list)
     ```

6. 如何区分Python中的break、continue、pass？

   - break：终止循环，跳出循环体，一般用在while和for循环中当满足一个条件后直接跳出循环
   - continue：中止本轮循环，开启下一轮循环，一般用在while和for循环中当满足一个条件后中止本轮循环，continue后面的循环体代码不再执行，直接进入下一轮循环
   - pass：pass是一个保持语法完整性的占位符，如果此处暂未明确要写什么内容，还必须要写否则报错的时候就可以先写一个pass

7. Python中什么元素的布尔值为False？

   0、空字符串、空列表、空元组、空字典、None、False

8. a=1, b=2, 不用中间变量如何交换a和b的值？

   - 方法一

     ```python
     a = a ^ b
     b = a ^ b
     a = a ^ b
     ```

   - 方法二

     ```python
     a, b = b, a
     ```

9. Python中单引号、双引号和三引号的区别是什么？

   单引号和双引号是等效的，如果引号中内容要分为多行，就需要使用符号 \ ，三引号则可以直接换行，并且可以包含注释。单引号里面不能再加单引号，但是可以加 \ 或者是双引号进行转义输出。双引号里面不能再加双引号，但是可以加 \ 或者是单引号进行转义输出。如果想对输出内容不进行转义可以再内容前加一个r。

10. 如何用一行代码实现1-100之和？

   ```python
   print((1 + 100) * 100 // 2)
   print(sum([i for i in range(101)]))
   ```

11. 如何求出列表中所有奇数并构造新列表？

    ```python
    old_list = [3, 2, 6, 4, 9, 5, 1, 8]
    new_list = [i for i in old_list if i % 2]
    
    print(new_list)
    ```

12. 如何用一行代码写出1+2+3+10248？

    ```python
    from functools import reduce
    # 1.使用sum内置求和函数
    num = sum([1,2,3,10248])
    print(num)
    # 2.reduce函数
    num1 = reduce(lambda x,y :x+y,[1,2,3,10248])
    print(num1)
    ```

13. 如何用一行代码实现将1~100的整数列表以3为单位分组？

    ```python
    lis = [[x for x in range(1, 101)][i:i + 3] for i in range(0, 100, 3)]
    print(lis)
    ```

14. json序列化时，默认遇到中文会转换成unicode，如果想要保留中文怎么办？

    ```python
    import json
    
    dict1 = {'name': '张三'}
    print(json.dumps(dict1, ensure_ascii=False))
    ```

15. Python中可变数据类型和不可变数据类型分别有哪些？

    可变数据类型：列表，字典、集合

    不可变数据类型：元组、数字、字符串

16. Python中什么可以作为字典的键？

    Python要求字典中的键是不可变数据类型，如字符串、数字或元组，而值则可以取任何数据类型。

17. Python中如何实现元组和列表的转换？

    ```python
    # list to tuple
    lis = [1, 2, 3, 4, 5, 6]
    tup = tuple(lis)
    print(type(tup), tup)
    
    # tuple to list
    tup = (1, 2, 3, 4, 5, 6)
    lis = list(tup)
    print(type(lis), lis)
    ```

# Python高级

1. @property怎么用？

   Python的@property是一种装饰器，用来修饰方法的。可以使用@property装饰器将方法转换为相同名称的只读属性，一般与类中定义的私有属性配合使用，防止私有属性被修改。

   ```python
   class Person(object):
       def __init__(self):
           self.__age = 20
   
       @property
       def age(self):
           return self.__age
   
       # 给私有属性__age赋值的方法，装饰器名称必须是上面 @方法名.setter
       # @property和@age.setter是一对，一个是取值；一个是赋值，可以防止随意改变私有属性
       @age.setter
       def age(self, age):
           if age > 18:
               self.__age = age
   
   
   if __name__ == '__main__':
       person = Person()
       print(person.age)
       person.age = 30
       print(person.age)
   ```

2. 在Python中如何实现单例？

   > **点评**：单例模式是指让一个类只能创建出唯一的实例，这个题目在面试中出现的频率极高，因为它考察的不仅仅是单例模式，更是对Python语言到底掌握到何种程度，建议使用装饰器和元类这两种方法来实现单例模式，因为这两种方式的通用性最强，而且也可以顺便展示自己对装饰器和元类两个关键知识点的理解。

   - 模块是天然的单例，可以在模块中创建好一个类对象，在别的模块中使用到该类的对象时都导入指定模块中已经创建好的类对象

   - 继承单例类

     ```python
     class Singleton(object):
         _instance = None
     
         def __new__(cls, *args, **kwargs):
             if cls._instance is None:
                 cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
             return cls._instance
     
     
     class Foo(Singleton):
         pass
     
     
     if __name__ == '__main__':
         foo1 = Foo()
         foo2 = Foo()
         print(foo1 is foo2)
     ```

   - 使用装饰器

     ```python
     from functools import wraps
     
     
     def singleton(cls):
         instances = {}
     
         @wraps(cls)
         def wrapper(*args, **kwargs):
             if cls not in instances:
                 instances[cls] = cls(*args, **kwargs)
             return instances[cls]
     
         return wrapper
     
     
     @singleton
     class Foo(object):
         pass
     
     
     if __name__ == '__main__':
         foo1 = Foo()
         foo2 = Foo()
         print(foo1 is foo2)
     ```

   - 使用元类

     ```python
     class Singleton(type):
         _instance = None
     
         def __call__(cls, *args, **kwargs):
             if cls._instance is None:
                 cls._instance = super(Singleton, cls).__call__(*args, **kwargs)
             return cls._instance
     
     
     class Foo(metaclass=Singleton):
         pass
     
     
     if __name__ == '__main__':
         foo1 = Foo()
         foo2 = Foo()
         print(foo1 is foo2)
     ```

   > **扩展**：Python时面型对象的语言，在面向对象的世界中，一切皆为对象。对象时通过类来创建的，而类本身也是对象，类这样的对象时通过元类来创建的。我们在定义类时，如果没有给一个类指定父类，那么默认的父类是`object`，如果没有给一个类指定元类，那么默认的元类是`type`。通过自定义的元类，我们可以改变一个类默认的行为，就如同上面的代码中，实际上类创建对象的过程`Foo()`也是在调用元类的`__call__`魔法方法，因此我们可以通过改变该魔法方法来改变类本身的构造过程。

   > **补充**：关于单例模式，在面试中还有可能被问到它的应用场景。通常一个对象的状态是被其他对象共享的，就可以将其设计为单例，例如项目中使用的数据库连接池对象和配置对象通常都是单例，这样才能保证所有地方获取到的数据库连接和配置信息是完全一致的；而且由于对象只有唯一的实例，因此从根本上避免了重复创建对象造成的时间和空间上的开销，也避免了对资源的多重占用。再举个例子，项目中的日志操作通常也会使用单例模式，这是因为共享的日志文件一直处于打开状态，只能有一个实例去操作它，否则在写入日志的时候会产生混乱。

3. 装饰器的应用场景，写一个统计性能的装饰器

4. 说一下你对可迭代对象、迭代器和生成器的理解。

   简单从概念上来说，可迭代对象 > 迭代器 > 生成器

   - 可迭代对象`Iterable`，可以认为是一个容器，其中有N个元素，可以进行迭代操作。

     在Python中可以简单的认为，能够使用for循环遍历的都是可迭代对象。常见的类型有列表、元组、range对象、字符串、集合、字典等，但这些类型并非是迭代器。

     实现了`__iter__`方法的对象是可迭代对象

5. 写一个删除列表中重复元素的函数，要求去重后元素的相对位置保持不变

   ```python
   def dedup(items):
       no_dup_items = []
       seen = set()
   
       for item in items:
           if item not in seen:
               no_dup_items.append(item)
               seen.add(item)
       return no_dup_items
   
   
   if __name__ == '__main__':
       items = [4, 5, 8, 2, 4, 7, 5, 9, 8, 3, 7]
       print(dedup(items))
   ```

   如果去重以后的列表依然很大，为了减少内存消耗，可以将上述函数改成一个生成器

   ```python
   def dedup(items):
       seen = set()
   
       for item in items:
           if item not in seen:
               seen.add(item)
               yield item
   
   
   if __name__ == '__main__':
       items = [4, 5, 8, 2, 4, 7, 5, 9, 8, 3, 7]
       for i in dedup(items):
           print(i)
   ```

   > **扩展**：由于Python中集合底层使用哈希存储，所以集合的`in`和`not in`成员运算在性能上远远优于列表，所以撒谎给你面的代码我们使用了集合来保存已经出现过的元素。集合中元素必须是`hashable`对象，因此上面的代码在列表元素不是`hashable`对象时会失效，要解决这个问题可以给函数增加一个参数，该参数可以设计为返回哈希码或`hashable`对象的函数。

6. 假设你使用的是官方的的CPython，说出下面代码的运行结果。

   > **点评**：下面的程序对实际开发并没有什么意义，但却是CPython中的一个大坑，这道题旨在考查面试者对官方的Python解释器到底了解到什么程度。

   ```python
   a, b, c, d = 1, 1, 1000, 1000
   print(a is b, c is d)
   
   def foo():
       e = 1000
       f = 1000
       print(e is f, e is d)
       g = 1
       print(g is a)
   
   foo()
   ```

   运行结果：

   ```python
   True False
   True False
   True
   ```

   上面代码中`a is b`的结果是`True`但`c is d`的结果是`False`，这一点的确让人费解。CPython解释器出于性能优化的考虑，把频繁使用的整数对象用一个叫`small_ints`的对象池缓存起来造成的。`small_ints`缓存的整数值被设定为`[-5, 256]`这个区间，也就是说，在任何引用这些整数的地方，都不需要重新创建`int`对象，而是直接引用缓存池中的对象。如果整数不在该范围内，那么即便两个整数的值相同，它们也是不同的对象。

   CPython底层为了进一步提升性能还做了另一个设定，对于同一个代码块中值不在`small_ints`缓存范围内的整数，如果同一个代码块中已经存在一个值与其相同的整数对象，那么就直接引用该对象，否则创建新的`int`对象。需要大家注意的是，这条规则对数值型适用，但对字符串则需要考虑字符串的长度，这一点大家可以自行证明。

7. Lambda函数是什么，举例说明它的应用场景。

8. 说说Python中的浅拷贝和深拷贝。

   > **点评**：这个题目本身出现的频率非常高，但是就题论题而言没有什么技术含量。对于这种面试题，在回答的时候一定要让你的答案能够超出面试官的预期，这样才能获得更好的印象分。所以回答这个题目的要点不仅仅是能够说出浅拷贝和深拷贝的区别，深拷贝的时候可能遇到的两大问题，还要说出Python标准库对浅拷贝和深拷贝的支持，然后可以说说列表、字典如何实现拷贝操作以及如何通过序列化和反序列化的方式实现深拷贝，最后还可以提到设计模式中的原型模式以及它在项目中的应用。

   浅拷贝只复制对象本身，而深拷贝不仅会赋值对象，还会递归的复制对象所关联的对象。深拷贝可能会遇到两个问题：一是一个对象如果直接或间接的引用了本身，会导致无休止的递归拷贝；二是深拷贝肯恶搞对原本设计为多个对象共享的数据也进行拷贝。Python通过`copy`模块中的`copy`和`deepcopy`方法来实现浅拷贝和深拷贝的操作，其中`deepcopy`可以通过`memo`字典来保存已经拷贝过的对象，从而避免刚才说的自引用递归问题；此外，可以通过`copyreg`模块的`pickle`方法来定制指定类型对象的拷贝行为。

   `deepcopy`方法的本质其实就是对象的一次序列化和反序列化，面试题中还考过自定义方法实现对象的深拷贝操作，显然我们可以使用`pickle`模块的`dumps`和`loads`来做到，代码如下所示：

   列表的切片操作 [:] 相当于实现了列表对象的浅拷贝，而字典的`copy`方法可以实现字典对象的浅拷贝。对象拷贝其实是更为快捷的创建对象的方式。在Python中，通过构造器创建对象属于两阶段构造，首先是分配内存空间，然后是初始化。在创建对象时，我们也可以基于“原型”对象来创建新对象，通过对原型对象的拷贝（复制内存）就完成了对象的创建和初始化，这种做法更加高效，这就是设计模式中的原型模式。在Python中，我们可以通过元类的方式实现原型模式，代码如下所示：

   ```python
   import copy
   
   
   class PrototypeMeta(type):
       """实现原型模式的元类"""
   
       def __init__(cls, *args, **kwargs):
           super().__init__(*args, **kwargs)
           # 为对象绑定clone方法来实现对象拷贝
           cls.clone = lambda self, is_deep=True: \
               copy.deepcopy(self) if is_deep else copy.copy(self)
   
   
   class Person(metaclass=PrototypeMeta):
       pass
   
   
   p1 = Person()
   p2 = p1.clone()                 # 深拷贝
   p3 = p1.clone(is_deep=False)    # 浅拷贝
   ```

9. Python是如何实现内存管理的？

10. `__init__`和`__new__`方法有什么区别？

    Python中调用构造器创建对象分为两个过程，首先执行`__new__`方法申请一段内存地址并创建一个对象保存在该地址中，然后把创建好的对象返回给`__init__`方法的第一个参数`self`，该方法对传过来的对象进行属性初始化。

    区别：

    - `__new__`：该方法是一个类方法，因此其第一个参数是cls，代表的是类本身。因为在创建对象时它先于`__init__`方法调用，所以可以用于实现单例模式。
    - `__init__`：该方法是实例方法，用来对`__new__`方法创建出来的对象进行实例化，因此其第一个参数是self，代表实例对象本身。对象的私有属性也是要在该方法中定义。

11. 用多种方式实现一个记录函数执行时间的装饰器。

12. 说一下你对闭包的理解。

    函数执行完后返回结果是一个内部函数，并被外部变量所引用，如果内部函数使用被执行函数作用域的变量，就形成了闭包。正常情况下，函数的局部变量在函数调用结束之后就结束了生命周期，但是闭包使得局部变量的声明周期得到了延展。使用闭包的时候需要注意，闭包会使得函数中创建的对象不会被垃圾回收，可能会导致很大的内存开销，所以闭包一定不能滥用。

13. 说一下对`hasattr()`，`getattr()`，` setattr()` 函数的理解。

14. 简述一下`any()`和`all()`方法。

15. 说一下Python中的多线程和多进程的应用场景和优缺点。

16. 解释一下线程池的工作原理。

17. 举例说明什么情况下会出现`KeyError`、`TypeError`、`ValueError`。

18. 说一下Python中常见的异常类型。

19. 说一下你对Python中模块和包的理解。

20. 函数参数`*args`和`kwargs`分别代表什么？

    在Python中，函数的参数分为位置参数、可变参数、关键字参数、命名关键字参数。`*args`代表可变参数，可以接收任意多个参数，当不确定调用者会传入几个位置参数时，就可以使用可变参数，它会将传入的参数打包成一个元组。`**kwargs`代表关键字参数，可以接收用`参数名=参数值`的方式传入的参数，传入的参数会打包成一个字典。定义函数的时候如果同时使用`*args`和`**kwargs`，那么函数可以接收任意参数，但要求`args`，`kwargs`必须位于位置参数之后。

21. 谈谈你对“猴子补丁”的理解。

    “猴子补丁”是动态类型语言的一个特性，代码运行时在不修改源代码的前提下改变代码中的方法、属性等以达到热补丁的效果。很多系统的安全补丁也是通过热补丁的方式实现的，但实际开发中应该避免对猴子补丁的使用，以免造成代码行为不一致的问题。在使用`gevent`库的时候，我们会在代码开头的地方执行`gevent.monkey.patch_all()`，这行代码的作用是把标准库中的socket模块给替换掉，这样我们在使用`socket`的时候，不用修改任何代码就可以实现对代码的协程化，达到提升性能的目的，这就是猴子补丁的应用。

    另外，如果希望用`ujson`三方库替换掉标准库中的`json`，也可以使用猴子补丁的方式，代码如下所示：

    ```python
    import json
    import ujson
    
    
    def monkey_patch_json():
        json.__name__ = 'ujson'
        json.dumps = ujson.dumps
        json.loads = ujson.loads
    
    
    monkey_patch_json()
    ```

    

