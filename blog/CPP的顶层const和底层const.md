
指针本身是一个对象，它又可以指向另一个对象。因此，指针本身是不是常量以及指针所指的是不是一个常量就是两个相互独立的问题，作名词

## 顶层const表示指针本身是个常量，

而名词

## 底层const表示指针所指的对象是一个常量

。
----------------------

## 如何区分顶层const和底层const
指针如果添加const修饰符时有两种情况：

1 指向常量的指针：
代表不能改变其指向内容的指针。声明时const可以放在类型名前后都可，拿int类型来说，
**声明时：const int和int const 是等价的。**
**声明指向常量的指针也就是底层const。**


    int a = 1;
    int const  *p_a = &a; //底层const
    //*p_a = 2;  //错误，指向“常量”的指针不能改变所指的对象

*注意：指向“常量”的指针不代表它所指向的内容一定是常量，只是代表不能通过解引用符（操作符*）来改变它所指向的内容。上例中指针p_a指向的内容就不是常量，可以通过赋值语句：num_a=2;  来改变它所指向的内容。*

2 指针常量：
**代表指针本身是常量，声明时必须初始化，之后它存储的地址值就不能再改变。**


声明时**const必须放在指针符号*后面，即：*const 。**声明常量指针就是顶层const，下面举一个例子：

    int b = 2;
    int *const p_b = &b; //顶层const
    //p_b = &a;  //错误，常量指针不能改变存储的地址值

其实顶层const和底层const很简单，**一个指针本身添加const限定符就是顶层const（int * const p = 0;），而指针所指的对象添加const限定符就是底层const（const int *p = 0;）。** 

## 二 区分顶层const和底层const的作用


1 **执行对象拷贝时有限制，常量的底层const不能赋值给非常量的底层const。**
正确区分顶层const和底层const，你就能避免这样的赋值错误。


    int num_c = 3;
    const int *c = &c;  //p_c为底层const的指针
    int *p_d = p_c;  //错误，不能将底层const指针赋值给非底层const指针
    const int *p_d = p_c; //正确，可以将底层const指针复制给底层const指针

2 **使用命名的强制类型转换函数const_cast时，需要能够分辨底层const和顶层const，因为const_cast只能改变运算对象的底层const。**

    int e = 4;
    const int *p_e = &e;//*p_e = 5;  //错误，不能改变底层const指针指向的内容
    int *p_f = const_cast<int*>(p_e);  
    //正确，const_cast可以改变运算对象的底层const。
    //但是使用时一定要知道不是const的类型。
    *p_f = 5;  //正确，非顶层const指针可以改变指向的内容
    cout << num_e;  //输出5

三 练习

    const int *const*const* pppi ;
    //是顶层const还是底层const？
    //是底层const，因为int前面const限定符，而最后一个*后面没有const限定符。


    int i = 0;
    int * const p1 = &i;	 	//顶层const，不能改变p1的值
    const int ci = 42;			//顶层const，不能改变ci的值
    const int *p2 = &ci；		//底层const，不能改变p2的值、
    const int *const p3 = p2；	//右边是顶层，左边是底层
    const int &r = ci；			//用于声明引用的const都是底层
    int *p = p3;				//F	p3包含底层定义，p没有，不能赋值
    p2 = p3；				//T	p2 p3都是底层const
    int &r = ci;			//F	普通的int引用不能绑定到int常量
    const int &r2 = i;		//T 	const iny &可以绑定到int常量

