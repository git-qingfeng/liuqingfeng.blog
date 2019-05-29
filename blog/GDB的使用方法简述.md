
一个调试示例
——————
源程序：tst.c

    1 #include <stdio.h>
    2
    3 int func(int n)
    4 {
    5 	int sum=0,i;
    6 	for(i=0; i<n; i++)
    7 	{
    8 		sum+=i;
    9 	}
    10 	return sum;
    11 }
    12
    13
    14 main()
    15 {
    16 	int i;
    17 	long result = 0;
    18 	for(i=1; i<=100; i++)
    19 	{
    20 		result += i;
    21 	}
    22
    23 	printf("result[1-100] = %d n", result );
    24 	printf("result[1-250] = %d n", func(250) );
    25 }

编译生成执行文件：（Linux下）
hchen/test> cc -g tst.c -o tst
使用GDB调试：

    hchen/test> gdb tst <---------- 启动GDB
    GNU gdb 5.1.1
    Copyright 2002 Free Software Foundation, Inc.
    GDB is free software, covered by the GNU General Public License, and you are
    welcome to change it and/or distribute copies of it under certain conditions.
    Type "show copying" to see the conditions.
    There is absolutely no warranty for GDB. Type "show warranty" for details.
    This GDB was configured as "i386-suse-linux"...
    (gdb) l <-------------------- *l命令相当于list，从第一行开始例出原码。*
    1 #include <stdio.h>
    2
    3 int func(int n)
    4 {
    5 int sum=0,i;
    6 for(i=0; i<n; i++)
    7 {
    8 sum+=i;
    9 }
    10 return sum;
    (gdb) <-------------------- *直接回车表示，重复上一次命令*
    11 }
    12
    13
    14 main()
    15 {
    16 int i;
    17 long result = 0;
    18 for(i=1; i<=100; i++)
    19 {
    20 result += i;
    (gdb) break 16 <-------------------- *设置断点，在源程序第16行处。*
    Breakpoint 1 at 0x8048496: file tst.c, line 16.
    (gdb) break func <-------------------- *设置断点，在函数func()入口处。*
    Breakpoint 2 at 0x8048456: file tst.c, line 5.
    (gdb) info break <-------------------- *查看断点信息。*
    Num Type Disp Enb Address What
    1 breakpoint keep y 0x08048496 in main at tst.c:16
    2 breakpoint keep y 0x08048456 in func at tst.c:5
    (gdb) r <--------------------- *运行程序，run命令简写*
    Starting program: /home/hchen/test/tst
    Breakpoint 1, main () at tst.c:17 <---------- *在断点处停住。*
    17 long result = 0;
    (gdb) n <--------------------- *单条语句执行，next命令简写。*
    18 for(i=1; i<=100; i++)
    (gdb) n
    20 result += i;
    (gdb) n
    18 for(i=1; i<=100; i++)
    (gdb) n
    20 result += i;
    (gdb) c <--------------------- *继续运行程序，continue命令简写。*
    Continuing.
    result[1-100] = 5050 <----------*程序输出。*
    Breakpoint 2, func (n=250) at tst.c:5
    5 int sum=0,i;
    (gdb) n
    6 for(i=1; i<=n; i++)
    (gdb) p i <--------------------- *打印变量i的值，print命令简写。*
    $1 = 134513808
    (gdb) n
    8 sum+=i;
    (gdb) n
    6 for(i=1; i<=n; i++)
    (gdb) p sum
    $2 = 1
    (gdb) n
    8 sum+=i;
    (gdb) p i
    $3 = 2
    (gdb) n
    6 for(i=1; i<=n; i++)
    (gdb) p sum
    $4 = 3
    (gdb) bt <--------------------- *查看函数堆栈。*
    #0 func (n=250) at tst.c:5
    #1 0x080484e4 in main () at tst.c:24
    #2 0x400409ed in __libc_start_main () from /lib/libc.so.6
    (gdb) finish <--------------------- *退出函数。*
    Run till exit from #0 func (n=250) at tst.c:5
    0x080484e4 in main () at tst.c:24
    24 printf("result[1-250] = %d n", func(250) );
    Value returned is $6 = 31375
    (gdb) c <--------------------- *继续运行。*
    Continuing.
    result[1-250] = 31375 <----------*程序输出。*
    Program exited with code 027. <--------*程序退出，调试结束。*
    (gdb) q <--------------------- *退出gdb。*
    hchen/test>

好了，有了以上的感性认识，还是让我们来系统地认识一下gdb吧。
使用GDB
————
一般来说GDB主要调试的是C/C++的程序。要调试C/C++的程序，首先在编译时，我们必须要把调试信息加到可执行文件
中。使用编译器（cc/gcc/g++）的 -g 参数可以做到这一点。如：

    > cc -g hello.c -o hello
    > g++ -g hello.cpp -o hello

如果没有-g，你将看不见程序的函数名、变量名，所代替的全是运行时的内存地址。