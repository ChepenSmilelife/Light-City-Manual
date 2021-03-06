.. figure:: http://p20tr36iw.bkt.clouddn.com/c++_const.png
   :alt: 

.. raw:: html

   <!--more-->

c++之const
==========

1.const与基本数据类型
---------------------

-  加上const后,变量变为常量,不可修改

.. code:: cpp

    const int x = 3; //常量

上述代码与宏定义\ ``#define x =3;``\ 作用相同,区别点在于:const修饰会在执行时候提示报错，而宏定义不会。

2.const与指针类型
-----------------

2.1 对比等价
~~~~~~~~~~~~

.. code:: cpp

    1.const int *p = NULL;
    2.int const *p = NULL;
    3.int * const p = NULL;
    1与2完全等价,3则与前两个不等价
    4.const int * const p = NULL;
    5.int const * const p = NULL;
    4与5也完全等价

2.2 查看错误
~~~~~~~~~~~~

-  第一种

.. code:: cpp

    int x = 3;
    const int *p = &x;
    p = &y; //正确
    *p = 4; //错误

原因:
上述\ ``const``\ 修饰的是\ ``*p``,也就是\ ``*p``\ 不能修改,\ ``p``\ 可以修改。

-  第二种

.. code:: cpp

    int x = 3;
    int * const p = &x;
    p = &y; //错误
    *p = 4; //正确

原因:
上述\ ``const``\ 修饰的是\ ``p``,也就是\ ``p``\ 不能修改,\ ``*p``\ 可以修改。

-  第三种

.. code:: cpp

    const int x = 3;
    const int * const p = &x;
    p = &y; //错误
    *p = 4; //错误

原因: 上述\ ``const``\ 修饰的是\ ``*p``\ 与\ ``p``,两者均不能修改。

3.const与引用
-------------

.. code:: cpp

    int x = 3;
    const int &y = x;
    x = 10; //正确
    y = 20; //错误

原因: const修饰的是&y,对x修改可以，但对y不能修改。

4.示例
------

4.1 大权限操纵小权限
~~~~~~~~~~~~~~~~~~~~

.. code:: cpp

    const int x = 3;
    int *y = &x;

上述代码报错！

原因:
x不可变,权限小,只能读,而指针y指向了x的地址,y的权限很大,如果修改了y的值,那么x也会发生变化,这样就会报错！

总结:以一个大的权限去操纵小的权限则是不允许的。反之成立，如下。

4.2 小权限操纵大权限
~~~~~~~~~~~~~~~~~~~~

.. code:: cpp

    int x = 3;
    const int *y = x;

上述代码不报错!

**总结:const谁,谁就不能被修改！**
