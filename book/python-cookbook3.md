# python cookbook3 笔记

## 数据结构和算法  

### 解压可迭代对象
data = [1,2,[3,4]]
a,b,c = data		# 常规解压  
a,b,(c,d) = data 	# 解压所有所有值  
a,*_ = data		# 忽略某些值  

注意: 操作对象为 字符串,文件对象,迭代器,生成器  


### 保留最后N个元素
deque = collections.deque(maxlen=N)	# 长度为N的队列  
deque.append(val)
deque.pop()
deque.appendleft(val)			# 列表头插入O(N)
deque.popleft()				# 列表头删除N(N)


### 获取最大或最小的N个元素
heapq.nlargest(n,iterable, key)		# 前N个最大元素, n: 个数, iterable: 数据, key: 同sorted中key一致  
heapq.nsmallest(n, iterable, key)	# 前N个最小元素   

heapq.heapify(heap_list) 		# 堆排序, AESC, inplace
heapq.heappop(heap_list)		# 弹出元素  
heapq.heappush(heap_list, data)		# 插入堆, 保持堆的顺序不变

注意: 查找最大/最小元素数量较少, 使用heapq合适; 查找唯一最大/最小使用max()或min(); 查找元素和集合大小接近sorted()然后切片  


### 优先级队列  
??
pop时总返回优先级最高的元素  
```python 
import heapq  

class PriorityQueue:
    def __init__(self):
        self._queue = []
        self._index = 0

    def push(self, item, priority):
        heapq.heappush(self._queue, (-priority, self._index, item))
        self._index += 1

    def pop(self):
        return heapq.heappop(self._queue)[-1]
```


### 字典键映射多个值  
eg. {k1: [1,2,3]}  
from collections import defaultdict  
d = defaultdict(list)  		# d[key].append(val), if key not in d: d[key] = []
d = defaultdict(set)		# d[key].add(val)  

注意: 也可以使用dict.setdefault(key, default=None)实现类似功能


### 有序字典  
from collections import OrderedDict  
d = OrderedDict()		# OrderedDict 继承原生dict类, 使用双向链表维护key的顺序, 占用内存为dict的两倍; 3.6之后的字典默认有序  


### 字典运算  
zip(dict.values(), dict.keys())		# 得到((k1,v1),(k2,v2), ...)元组, 然后可以使用min, max, sorted 函数进行操作  

a.keys() & b.keys()		# 两个字典共有的key, '&' 可以换成 '-'  
a.items() & b.items()		# 字典items也支持集合运算  
x = {k:a[k] for k in a.keys() - {k1}}	# 字典推导,排除k1的元素

注意: keys()返回的是key的视图, items()返回的是(key, value)的视图, 这两个支持集合操作; values()不支持集合操作, 因为其值可能不唯一  


### 删除重复元素并保持顺序    
set(list)			# 去除重复元素, 乱序  

list, dict去除重复元素, 保持原始顺序, 这里的key和sorted中的key一致, 参考1.10    
```python
def dedupe(items, key=None):
    seen = set()
    for item in items:
        val = item if key is None else key(item)
        if val not in seen:
            yield val
            seen.add(val)
```


### 命名切片  
name = slice(5, 50)		# b.step = None  
name = slice(5, 50, 2)		# start, stop, step, 可以直接用'.'访问  
new = name.indices(number)	# 对命名切片对象进行缩放, 当start<number, stop=number; 当number<start, start=stop=number; 注意值>=0  


### 统计出现次数  
collections.Counter(hashable)	# 返回字典,key=name,value=出现次数
most_common(n:int)		# 成员方法, 返回频率最高的前n个键值对  
update(hashable)		# 增加更新的值  
+, - 				# 对相同key对应的value进行加减  


### 字典排序  
通过几个key对字典列表[{}, {}, ...]进行排序  
from operator import itemgetter  
sorted_dict = sorted(src_dict, key=itemgetter('key1', 'key2'))  
sorted_dict = sorted(src_dict, key=lambda r: (r['key1', r['key2']))	# 效率低于itemgetter  
min(src_dict, key=itemgetter('key'))	# max类似  


### 自定义类排序 
[instance1, instace2, ...] 
from operator import itemgetter  
sorted_ = sorted(src_instance_list, key=itemgetter('attr1', 'attr2'))  
min, max 同字典排序类似  


### 字典列表分组  
from operator import itemgetter  
from itertools import groupby  
for date, items in groupby(dict_list, key=itemgetter('date'))		# 返回分组的key和该key对应的迭代器  

注意:  
1. 使用groupby需要先对原始数据进行排序, 因为groupby仅仅检查连续的元素, 如果没有排序得到的可能不是想要的结果  
2. 可以使用defaultdict构建多值字典  


### 数据过滤  
使用列表推导  
[n for n in mylist if n > 0]		# 缺点,如果输入结果非常大的时候会产生一个非常大的结果集, 占用大量内存, 可以用生成器迭代产生, 将'[]'换成'()'  
vals = list(filter(is_int, values))	# is_int 是类型判断函数, values为一个可迭代对象, filter返回是一个迭代器  

过滤工具:itertools.compress()  
for itertools import compress  
list(copress(src_list, bool_list))	# src_list 和 bool_list 长度要一致, 取出bool_list为True的index在src_list中的元素  


### 提取字典子集  
{K:v for k, v in _dict.items() if value > 200}		# 字典推导  
{K:v for k, v in _dict.items() if key in {'k1', 'k2'}}	# 字典推导  


### 命名元组  
form collections import namedtuple  
Demo = nametuple('name', ['attr_name1', 'attr_name2'])  
sub = Demo('value1', 'value2')  			# sub.attr_name1 的值为value1  

注意: 命名元组可以代替字典, 但是一般不可更改, 如果需要更改使用_replace(key=value)  
sub._replace(**s)					# sub创建或这更新值, 注意 s 类型为 dict  


### 聚集函数使用生成器  
sum(x*x for x in nums)  
any(), join(), min(), max()  


### 合并字典或映射  
from collections import ChainMap  
c = ChainMap(dict_a, dict_b)  		# 在逻辑上变成一个字典,如果值有重复,则返回第一个dict_a中的值,更新或删除总是影响第一个字典的值  
values = ChainMap()  
values.new_child()  			# 创建一个子字典  
values.parents				# 返回父字典  

注意: 和dict.update合并字典不同的是, ChainMap对字典的修改可以映射到原始字典上, 但是update之后的字典修改对原字典无影响  



## 第二章 字符串和文本  

### 使用多个字符分隔字符串  
使用re.split(pattern, string)  
pattern: 正则表达式, 如r'[;,\s]\s*' 匹配以逗号,分号,空格后面紧跟任意个空格; r'(;|,\s)\s*' 保留分隔字符串, (?:...) 不保留分隔字符串  


### 匹配字符串开头,结尾  
使用startswith(), 和endwith(), 里面的参数可以为多个值,但必须为元组  
也可以使用re.match(patten, string)   

