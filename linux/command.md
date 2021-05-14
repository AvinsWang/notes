# Linux common commands
## logrotate
logrotate 基于cron运行, 脚本路径在/etc/cron.daily/logrotate
/etc/logrotate.conf    # 默认配置; 如果logrotate.d/目录下的配置某些项目未设置, 则使用该文件的配置
/etc/logrotate.d/      # 用户自定以配置需放置在该目录中

logrotate options:  
-d    # debug, 打印debug信息, 但并不正真进行轮转  
-f    # 强制转储, 系统可能认为并不需要转储, 通常是更新配置文件或者手动删除旧的日志文件后操作  
-m    # 压缩日志后, 发送到邮箱 
-s    # 执行的状态文件, 查看日志轮转是否运行, 可以指定输出到特定文件
-l    # 将-v打印的信息输出到文件中, 需要给定一个文件路径  
-v    # 打印运行详细信息

logrotate example:  
name.log {
# some important options
rotate 10    # number of rotated file to be kept, 0 remove log rather rotate  
daily        # weekly, monthly or yearly
compress     # gzip log then save, opposite 'nocompress'
copytruncate # 拷贝文件后再清空原始文件, 拷贝和清空之间有时间差, 可能导致log信息缺失, 注, 开启时create参数失效. opposite 'nocopytruncate'
create       # 创建新文件的属性, 例 create 0777 root root, opposite 'nocreate'  
delaycompress    # 和compress一起使用是, 转储的日志到下一次转储时才压缩, opposite 'nodelaycompress'
dateext      # name.log-20210101 else, name.log-1
dateformat   # 和dateext一起使用, 定义文件结尾, 默认为 %Y%m%d, 只支持%Y,%m,%d和%s四个参数   
size         # 大于指定size执行rotate, 默认byte, 10, 10k, 10M or 10G, equal to minsize 
missinggok   # 如果日志丢失不报错, 继续rotate下一个日志  
errors address   # rotate 错误发送的邮件地址 
ifempty      # 如果为空, 也做rotate; opposite, 'notifempyt'  
olddir dir   # 转储后的文件放入指定目录, 和原始日志文件在同一个文件系统中; opposite 'noolddir' 放在同一目录中  
sharedscripts    # 所有日志轮转完之后执行一次postrotate脚本, 否则, 每个日志rotate完成后就执行一次  
postrotate   # rotate完之后执行的脚本  
prerotate    # rotate前执行的脚本  
} 


