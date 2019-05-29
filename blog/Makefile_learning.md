## 0、注意
增加.PHONY声明为伪目标：

    .PHONY : clean
    clean :
    	rm -rf  $(objects)
  几个变量规则：

    $@，表示规则中的目标。 目标的通配符@
    $<，表示规则中的第一个依赖文件。第一个依赖的通配符<
    $?，表示规则中所有比目标新的条件，组成一个列表，以空格分隔。
    $^，表示规则中的所有条件，组成一个列表，以空格分隔。使用$^表示，它前面最近的目标的所有依赖
    
上面变量和通配符的结合

    %.o	: %.c
    	gcc -o $@ $< -c			#即用过gcc命令，根据输入的依赖所有的.c文件生成对应的.o文件
    -------------------------------------------------------
    %.o: %.c		#即.o文件依赖于当前文件下的所有.c文件
    ------------------------------------------------------
    all:    start.o main.o a.o b.o
    gcc  -o main $^    # $^代表着all后面的依赖o文件

## 1、一级Makefile
一般规则：
文件：

    main.c str.c str.h

Makefile：

    obj=main.o str.o
    all:$(obj)
    	gcc -o main $(obj) -L ./
    %.o:%.c
    	gcc -c $^ -o $@ -L ./
    
    .PYTHON:clean
    clean:
    	rm -rf $(obj) main
规则：

    obj= 各个c文件的o文件
    all:$(obj)
    	gcc -o main $(obj) -L ./
    %.o:%.c
    	gcc -c $^ -o $@ -L ./
    .PYTHON:clean
        clean:
        	rm -rf $(obj) main

## 2、多级Makefile
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190124132158255.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xxZl9vaw==,size_16,color_FFFFFF,t_70)
