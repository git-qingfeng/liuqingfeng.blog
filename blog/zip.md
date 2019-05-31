01.  .tar格式 
> 解包：[＊＊＊＊＊＊＊]tarxvfFileName.tar
> 打包：[＊＊＊＊＊＊＊]tarxvfFileName.tar
> 打包：[＊＊＊＊＊＊＊] tar cvf FileName.tar DirName（注：tar是打包，不是压缩！）

02.  .gz格式 
> 解压1：[＊＊＊＊＊＊＊]gunzipFileName.gz> 
> 解压2：[＊＊＊＊＊＊＊]gunzipFileName.gz> 
> 解压2：[＊＊＊＊＊＊＊] gzip -d FileName.gz 
压 缩：[＊＊＊＊＊＊＊]$ gzip FileName

03.  .tar.gz格式 
> 解压：[＊＊＊＊＊＊＊]tarzxvfFileName.tar.gz
压缩：[＊＊＊＊＊＊＊]tarzxvfFileName.tar.gz
压缩：[＊＊＊＊＊＊＊] tar zcvf FileName.tar.gz DirName

04.  .bz2格式 
> 解压1：[＊＊＊＊＊＊＊]bzip2?dFileName.bz2
> 解压2：[＊＊＊＊＊＊＊]bzip2?dFileName.bz2
> 解压2：[＊＊＊＊＊＊＊] bunzip2 FileName.bz2 
> 压 缩： [＊＊＊＊＊＊＊]$ bzip2 -z FileName

05.  .tar.bz2格式 
> 解压：[＊＊＊＊＊＊＊]tarjxvfFileName.tar.bz2
> 压缩：[＊＊＊＊＊＊＊]tarjxvfFileName.tar.bz2
> 压缩：[＊＊＊＊＊＊＊] tar jcvf FileName.tar.bz2 DirName

06.  .bz格式 
> 解压1：[＊＊＊＊＊＊＊]bzip2?dFileName.bz
> 解压2：[＊＊＊＊＊＊＊]bzip2?dFileName.bz
> 解压2：[＊＊＊＊＊＊＊] bunzip2 FileName.bz

07.  .tar.bz格式 
> 解压：[＊＊＊＊＊＊＊]$ tar jxvf FileName.tar.bz

08.  .Z格式 
> 解压：[＊＊＊＊＊＊＊]uncompressFileName.Z
> 压缩：[＊＊＊＊＊＊＊]uncompressFileName.Z
> 压缩：[＊＊＊＊＊＊＊] compress FileName

09.  .tar.Z格式 
> 解压：[＊＊＊＊＊＊＊]tarZxvfFileName.tar.Z
> 压缩：[＊＊＊＊＊＊＊]tarZxvfFileName.tar.Z
> 压缩：[＊＊＊＊＊＊＊] tar Zcvf FileName.tar.Z DirName

10.  .tgz格式 
> 解压：[＊＊＊＊＊＊＊]$ tar zxvf FileName.tgz

11.  .tar.tgz格式 
> 解压：[＊＊＊＊＊＊＊]tarzxvfFileName.tar.tgz
> 压缩：[＊＊＊＊＊＊＊]tarzxvfFileName.tar.tgz
> 压缩：[＊＊＊＊＊＊＊] tar zcvf FileName.tar.tgz FileName

12.  .zip格式 
> 解压：[＊＊＊＊＊＊＊]unzipFileName.zip
> 压缩：[＊＊＊＊＊＊＊]unzipFileName.zip
> 压缩：[＊＊＊＊＊＊＊] zip FileName.zip DirName

13.  .lha格式 
> 解压：[＊＊＊＊＊＊＊]lha?eFileName.lha
> 压缩：[＊＊＊＊＊＊＊]lha?eFileName.lha
> 压缩：[＊＊＊＊＊＊＊] lha -a FileName.lha FileName

14.  .rar格式 
> 解压：[＊＊＊＊＊＊＊]raraFileName.rar
> 压缩：[＊＊＊＊＊＊＊]raraFileName.rar
> 压缩：[＊＊＊＊＊＊＊] rar e FileName.rar 
---
rar请到：http://www.rarsoft.com/download.htm 下载！ 
- 解压后请将rar_static拷贝到/usr/bin目录（其他由PATH环境变量指定的目录也行）：[＊＊＊＊＊＊＊]PATH环境变量指定的目录也行）：[＊＊＊＊＊＊＊] cp rar_static /usr/bin/rar

---

1. 我想把一个文件abc.txt和一个目录dir1压缩成为yasuo.zip：

> zip -r yasuo.zip abc.txt dir1

2. 我下载了一个yasuo.zip文件，想> 解压缩：

> unzip yasuo.zip

3. 我当前目录下有abc1.zip，abc2.zip和abc3.zip，我想一起> 解压缩它们：

> unzip abc\?.zip

注释：?表示一个字符，如果用*表示任意多个字符。

4. 我有一个很大的压缩文件large.zip，我不想> 解压缩，只想看看它里面有什么：

> unzip -v large.zip

5. 我下载了一个压缩文件large.zip，想验证一下这个压缩文件是否下载完全了

> unzip -t large.zip

6. 我用-v选项发现music.zip压缩文件里面有很多目录和子目录，并且子目录中其实都是歌曲mp3文件，我想把这些文件都下载到第一级目录，而不是一层一层建目录：

> unzip -j music.zip