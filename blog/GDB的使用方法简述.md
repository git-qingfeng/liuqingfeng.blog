
һ������ʾ��
������������
Դ����tst.c

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

��������ִ���ļ�����Linux�£�
hchen/test> cc -g tst.c -o tst
ʹ��GDB���ԣ�

    hchen/test> gdb tst <---------- ����GDB
    GNU gdb 5.1.1
    Copyright 2002 Free Software Foundation, Inc.
    GDB is free software, covered by the GNU General Public License, and you are
    welcome to change it and/or distribute copies of it under certain conditions.
    Type "show copying" to see the conditions.
    There is absolutely no warranty for GDB. Type "show warranty" for details.
    This GDB was configured as "i386-suse-linux"...
    (gdb) l <-------------------- *l�����൱��list���ӵ�һ�п�ʼ����ԭ�롣*
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
    (gdb) <-------------------- *ֱ�ӻس���ʾ���ظ���һ������*
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
    (gdb) break 16 <-------------------- *���öϵ㣬��Դ�����16�д���*
    Breakpoint 1 at 0x8048496: file tst.c, line 16.
    (gdb) break func <-------------------- *���öϵ㣬�ں���func()��ڴ���*
    Breakpoint 2 at 0x8048456: file tst.c, line 5.
    (gdb) info break <-------------------- *�鿴�ϵ���Ϣ��*
    Num Type Disp Enb Address What
    1 breakpoint keep y 0x08048496 in main at tst.c:16
    2 breakpoint keep y 0x08048456 in func at tst.c:5
    (gdb) r <--------------------- *���г���run�����д*
    Starting program: /home/hchen/test/tst
    Breakpoint 1, main () at tst.c:17 <---------- *�ڶϵ㴦ͣס��*
    17 long result = 0;
    (gdb) n <--------------------- *�������ִ�У�next�����д��*
    18 for(i=1; i<=100; i++)
    (gdb) n
    20 result += i;
    (gdb) n
    18 for(i=1; i<=100; i++)
    (gdb) n
    20 result += i;
    (gdb) c <--------------------- *�������г���continue�����д��*
    Continuing.
    result[1-100] = 5050 <----------*���������*
    Breakpoint 2, func (n=250) at tst.c:5
    5 int sum=0,i;
    (gdb) n
    6 for(i=1; i<=n; i++)
    (gdb) p i <--------------------- *��ӡ����i��ֵ��print�����д��*
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
    (gdb) bt <--------------------- *�鿴������ջ��*
    #0 func (n=250) at tst.c:5
    #1 0x080484e4 in main () at tst.c:24
    #2 0x400409ed in __libc_start_main () from /lib/libc.so.6
    (gdb) finish <--------------------- *�˳�������*
    Run till exit from #0 func (n=250) at tst.c:5
    0x080484e4 in main () at tst.c:24
    24 printf("result[1-250] = %d n", func(250) );
    Value returned is $6 = 31375
    (gdb) c <--------------------- *�������С�*
    Continuing.
    result[1-250] = 31375 <----------*���������*
    Program exited with code 027. <--------*�����˳������Խ�����*
    (gdb) q <--------------------- *�˳�gdb��*
    hchen/test>

���ˣ��������ϵĸ�����ʶ��������������ϵͳ����ʶһ��gdb�ɡ�
ʹ��GDB
��������
һ����˵GDB��Ҫ���Ե���C/C++�ĳ���Ҫ����C/C++�ĳ��������ڱ���ʱ�����Ǳ���Ҫ�ѵ�����Ϣ�ӵ���ִ���ļ�
�С�ʹ�ñ�������cc/gcc/g++���� -g ��������������һ�㡣�磺

    > cc -g hello.c -o hello
    > g++ -g hello.cpp -o hello

���û��-g���㽫����������ĺ����������������������ȫ������ʱ���ڴ��ַ��