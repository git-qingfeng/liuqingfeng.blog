## 0��ע��
����.PHONY����ΪαĿ�꣺

    .PHONY : clean
    clean :
    	rm -rf  $(objects)
  ������������

    $@����ʾ�����е�Ŀ�ꡣ Ŀ���ͨ���@
    $<����ʾ�����еĵ�һ�������ļ�����һ��������ͨ���<
    $?����ʾ���������б�Ŀ���µ����������һ���б��Կո�ָ���
    $^����ʾ�����е��������������һ���б��Կո�ָ���ʹ��$^��ʾ����ǰ�������Ŀ�����������
    
���������ͨ����Ľ��

    %.o	: %.c
    	gcc -o $@ $< -c			#���ù�gcc�������������������е�.c�ļ����ɶ�Ӧ��.o�ļ�
    -------------------------------------------------------
    %.o: %.c		#��.o�ļ������ڵ�ǰ�ļ��µ�����.c�ļ�
    ------------------------------------------------------
    all:    start.o main.o a.o b.o
    gcc  -o main $^    # $^������all���������o�ļ�

## 1��һ��Makefile
һ�����
�ļ���

    main.c str.c str.h

Makefile��

    obj=main.o str.o
    all:$(obj)
    	gcc -o main $(obj) -L ./
    %.o:%.c
    	gcc -c $^ -o $@ -L ./
    
    .PYTHON:clean
    clean:
    	rm -rf $(obj) main
����

    obj= ����c�ļ���o�ļ�
    all:$(obj)
    	gcc -o main $(obj) -L ./
    %.o:%.c
    	gcc -c $^ -o $@ -L ./
    .PYTHON:clean
        clean:
        	rm -rf $(obj) main

## 2���༶Makefile
![���������ͼƬ����](https://img-blog.csdnimg.cn/20190124132158255.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xxZl9vaw==,size_16,color_FFFFFF,t_70)
