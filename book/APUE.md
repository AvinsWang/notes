# UNIX环境高级编程(第二版)

内核: 
系统调用: 内核的接口

口令文件内容(/etc/passwd):  
root:x:0:0:root:/root:/usr/bin/zsh  
登录名:加密口令:用户ID:用户组ID:注释字段:起始目录:shell程序  

shell概述及种类: bash, csh, ksh, tcsh    # p2  
文件属性: 包括文件类型, 文件大新, 文件所有者, 文件权限和文件的最后修改时间  
文件名: 不能只有'/' 或者''   

dirent.h:
func: opendir    # 
