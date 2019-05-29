犯了一个错误：
部分源码：

    unsigned double a = 10/3;
    unsigned int b = static_cast<unsigned double>(a);
    cout<<b<<endl;


在linux g++8.x编译过程提示：

    [samba@centos cpp]$ g++ case.cc 
    case.cc: 在函数‘int main(int, const char**)’中:
    case.cc:23:18: 错误：为‘a’使用‘signed’或‘unsigned’无效
      unsigned double a = 10/3;
                      ^
    case.cc:24:40: 错误：为‘type name’使用‘signed’或‘unsigned’无效
      unsigned int b = static_cast<unsigned double>(a);


我把unsigned去掉之后。就正常了。这是为什么呢？
改过之后的部分源码

double a = 10/3;
unsigned int b = static_cast<double>(a);
cout<<b<<endl;


后来上网查了一下资料：

原来浮点数是不能用 unsigned来规范的。unsigned 的意思就是把内存中的数据第一位也用来表示数据，而不用于表示符号位。而浮点数规定内存中数据的第一位必须是符号位。因此两者之间是互相矛盾的，这也就是为什么浮点数不会有unsigned类型。



在某些编译器下unsigned float 和 unsigned double会被自动转换成unsigned int 类型，而不报错。这时sizeof(unsigned float)和sizeof(unsigned double)的值是4。

 

**切记：不能定义unsigned float和unsigned double类型。**
 

因为整型是一串二进制来存内容
比如00000000，其中第一位是符号位用来表示正负，但是你设置无符号就可以让后面的往这里进位，打到增加数据的目地。

可是浮点数是按照 整数部分，小数部分，指数部分存放的。运算也是分开来运算的。
没法做这样的进位。

 

**unsigned只能修饰整型，即char short int long**

**数据类型定义的时候float，double就是带符号的了，浮点数第一位就是符号位**