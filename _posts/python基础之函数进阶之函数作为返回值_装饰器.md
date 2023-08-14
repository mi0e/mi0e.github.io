---
layout: post
cid: 35
title: python基础之函数进阶之函数作为返回值/装饰器
slug: 35
date: 2021/04/06 18:44:00
updated: 2021/04/06 18:50:49
status: publish
author: mi0e
categories: 
  - Python
tags: 
customSummary: 
noThumbInfoStyle: default
outdatedNotice: no
reprint: trans
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


**因为装饰器需要用到返回函数的知识，所以在这里将返回函数和装饰器合并讲解。**
**什么是返回函数？**

我们知道，一个函数中return可以返回一个或者多个值，但其实，return不仅可以返回值，还可以返回函数。

 实例：

```python
    def col(*arg):
        def sum():
            res_sum=0
            for i in arg:
                res_sum=res_sum+i
            return res_sum
        return sum()
    a=col(1,2,3,4,5)
    print(a)#结果：15
    #a=col(1,2,3,4,5)  ==〉
    #即a=sum,并且arg=(1,2,3,4,5)也被传入sum中了
    #a()==sum()
```
<p style="color:red">并且因为sum()定义在col()函数中，所以sum()继承了col()函数的局部变量和参数，这就是闭包。</p>（比如，col()的arg参数就被sum()所继承）

下面来看一个我在检验上面加红的句话时所碰到的一个问题：

```python
    #还是用上面这段代码。稍稍修改一下
    def col(*arg):
        res_sum=0         #注意：将这句话移动到这里了
        def sum():
            for i in arg:
                res_sum=res_sum+i
            return res_sum
        return sum()
    a=col(1,2,3,4,5)
    print(a())       
```    
    结果报错：local variable 'res_sum' referenced before assignment
    #既然内部函数可以引用外部函数的变量，为什么res_sum没有被内#部函数所引用？
为啥会报错？我当时很是疑惑，后来终于弄明白，错在这句：res_sum=res_sum+i     

<p style="color:blue">这句导致内部函数修改了外部函数的局部变量res_sum，这时，Python认为res_sum是内部函数的局部变量，而res_sum=res_sum+i之前并没有事先定义res_sum，所以当然会发生这种错误。</p>

所以，需要这样进行修改：

```python
    def col(*arg):
        res_sum=0         
        def sum():
            for i in arg:
                a=res_sum+i     #在内部函数中定义一个新的变量a
            return a
        return sum
    a=col(1,2,3,4,5)
    print(a())
```

----------
**什么是装饰器？**
```python
    def login():
        pass
    @login       #关键字@
    def open():
        pass
```
上例就是一个装饰器的例子。

**装饰器的作用：**
当我们定义了open函数后（可以帮助我们打开某个文件），过了一段时间，发现我们需要在进行open之前进行验证用户，如何在<p style="color:red">不修改open函数的条件下将login函数和open函数进行结合</p>，即：运行open之前先运行login？ 这里就要用到装饰器。

下面我们来看一个真正的装饰器的实例：
```python
    def login(fun):
        def real_login():
            print('please input your password')
            return fun()
        return real_login
    @login
    def open():
        print('hello world')
    open()
```
@login相当于open=login(open)   也就是将open函数偷梁换柱了一番。

当我们运行open()时：
```python
    open=login(open)　　
    #login(open)中的参数及局部变量：fun=open(原)　　
    #open=login(open)的返回值！
    #即：open=real_login　　
    open()=real_login()
    　　#因为real_login定义在login之中，所以继承其参数和局部变量
    　　#所以整体来看open()==login(open)+real_login()+open()
```

实现一个可以接受任意参数的装饰器：
```python
    def outer(func):
        def inner(*args,**kwargs):
            print('start')
            r=func(*args,**kwargs)    # 这里func(*args,**kwargs)相当于f(a,b)
            print('end')
            return r
        return inner
    
    @outer
    def f(a,b):
        print(a+b)
    @outer
    def f2(a,b,c):
        print(a+b+c)
    
    f(1,2)
    f2(1,2,3)
```
    #结果：
    start
    3
    end
    start
    6
    end