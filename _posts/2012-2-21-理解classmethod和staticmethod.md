---

layout: post

title:  "理解classmethod和staticmethod"

date:   2012-2-21 10:10:18 +0800

categories:  python

tags:   python

---

### 本质

classmethod和staticmethod本质上都是装饰器。可以用@标记。

~~~python
class C:
    @classmethod
    def f(cls, arg1, arg2, ...): ...
~~~

### classmethod作用

根据官方文档解释：

>classmethod Transform a method into a class method.

>A class method receives the class as implicit first argument, just like an instance method receives the instance. 

将一个方法转换为类方法，这个类方法接受本身作为第一参数，就像一个实例接受本身作为第一参数一样。

类方法可以被类本身，实例和继承对象调用。

类方法和类属性一样，都能被所有实例访问。类初始化之后，实例会自动绑定类方法和类属性。相同名称的实例属性和方法将屏蔽掉类属性和类方法。

### cls、self

pep8解释：

>Function and method arguments:

>Always use self for the first argument to instance methods.

>Always use cls for the first argument to class methods.

cls和self一样不是强制性的，都是一种写法上的约定俗成。

### staticmethod

>Transform a method into a static method.

>A static method does not receive an implicit first argument. To declare a static method, use this idiom:

~~~python
class C:
    @staticmethod
    def f(arg1, arg2, ...): ...
~~~

静态方法跟普通函数没什么区别，与类和实例都没有所谓的绑定关系，可以理解为只不过是碰巧存在类中的一个函数而已。不论是通过类还是实例都可以引用该方法。

### 总结

实例方法只能被实例对象调用，静态方法(由@staticmethod装饰的方法)、类方法(由@classmethod装饰的方法)，可以被类或类的实例对象调用。
实例方法，第一个参数必须要默认传实例对象，一般习惯用self。
静态方法，参数没有要求。
类方法，第一个参数必须要默认传类，一般习惯用cls。


----

以上！
