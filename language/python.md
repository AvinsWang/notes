# Python Rules

## f formart
format time:    
now = datetime.datetime.now()  
f"{now: %Y-%m-%d %H:%M:%S}"  

format float:  
f"{float_var:.2f}"  

format string width:  
f"{{str_var:02}}"    # 如果有0, 位数不够补0; 超出指定位数, 末位截断  

align:  
f"{str_var:>10}"     # align right  
f"{str_var:<10}"     # align left  

## pickle

- 可以存储的数据: 类,对象,类的实例,dict,复数,None,及其他python预定义数据类型
- 写入读取文件需要指定为字节格式, wb or rb

pickle.dump(obj, file, protocol=None)   # file打开格式为wb
pickle.load(file, * , fix_imports=True, encodeing='ASCII', errors='strict')    # file打开格式为rb
pickle.dumps(obj)    # obj to  byte对象
pickle.loads(obj)    # byte对象 to obj


## datetime
from datetime import datetime, timedelta, timezone

datetime.now()    # 当前时间, datetime对象  
datetime(Y,m,d,H,M,S)    # 初始化datetime对象  
dt.timetuple()    # datetime to time obj

dt.timestamp()    # datetime to mktime
time.mktime(dt.timetuple())       # 同上

datetime.fromtimestamp(mktime)    # mktime to localtime(datetime)
datetime.utcfromtimestamp(t)      # mktime to utctime(datetime)

datetime.strptime('2021-01-01 01:01:01', '%Y-%m-%d %H:%M:%S')    # string to datetime
dt.strftime('%Y-%m-%d %H:%M:%S')  # datetime to string

dt + timedelta(days=1, hours=1)   # datetime calc 

tz_utc_8 = timezone(timedelta(hours=8))
dt.replace(tzinfo=tz_utc_8)       # change timezone  

utc_dt = datetime.utcnow()        # get utc now time
bj_dt = utc_dt.astimezone(tz_utc_8)    # change timezone  


## logging v3.9.7
使用标准库中提供的logging API让程序中所有模块(自定义,第三方)都可以记录日志
- Loggers 提供可以让程序直接调用记录日志的接口  
- Handlers 发送由loggers创建的日志到合适目标  
- Fileters 过滤并选择哪些日志需要输出  
- Formaters 指定日志最终的输出格式  
注: 不要直接实例化一个logger, 应使用logging.getLogger(name)来获取logger对象, 类似单例  


