# UNIX环境高级编程(第二版) 
内核: 
系统调用: 内核的接口

口令文件内容(/etc/passwd):  
root:x:0:0:root:/root:/usr/bin/zsh  
登录名:加密口令:用户ID:用户组ID:注释字段:起始目录:shell程序  

shell概述及种类: bash, csh, ksh, tcsh    # p2  
文件属性: 包括文件类型, 文件大新, 文件所有者, 文件权限和文件的最后修改时间  
文件名: 不能只有'/' 或者''   

程序清单1-1: 列出一个目录中的所有文件 ls实现  p4  

<dirent.h>:
opendir	# 返回指向DIR结构体的指针  
readdir	# 读取目录, 返回只想dirent结构体的指针, 没有目录时返回null  
close	# 关闭目录  


程序清单1-2: 将标准输入复制到标准输出 cp实现  p6  
<unistd.h>  
STDIN_FILENO	# 标准输入文件描述符  
STDOUT_FILENO	# 标准输出文件描述符  
read()		# 读取文件返回文件字节数,当到文件尾部,返回0, 错误返回-1  


I/O函数:
- 不用缓冲的I/O: open, read, write, lseek 和 close, 使用文件描述符, 效率受缓冲区大小影响  
- 标准I/O函数: 如printf, 无需担心选择最佳缓冲区  
 
程序清单1-3: 用标准I/O将标准输入复制到标准输出 cp实现  p7  


程序清单1-4: 打印进程ID, getpid()  p8  

