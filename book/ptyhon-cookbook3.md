# python cookbook3 笔记


- 解压可迭代对象
data = [1,2,[3,4]]
a,b,c = data		# 常规解压  
a,b,(c,d) = data 	# 解压所有所有值  
a,*_ = data		# 忽略某些值  

注意: 操作对象为 字符串,文件对象,迭代器,生成器  


- 保留最后N个元素
deque = collections.deque(maxlen=N)	# 长度为N的队列  
deque.append(val)
deque.pop()
deque.appendleft(val)			# 列表头插入O(N)
deque.popleft()				# 列表头删除N(N)


- 获取最大或最小的N个元素
heapq.nlargest(n,iterable, key)		# 前N个最大元素, n: 个数, iterable: 数据, key: 同sorted中key一致  
heapq.nsmallest(n, iterable, key)	# 前N个最小元素   

heapq.heapify(heap_list) 		# 堆排序, AESC, inplace
heapq.heappop(heap_list)		# 弹出元素  
heapq.heappush(heap_list, data)		# 插入堆, 保持堆的顺序不变

注意: 查找最大/最小元素数量较少, 使用heapq合适; 查找唯一最大/最小使用max()或min(); 查找元素和集合大小接近sorted()然后切片  


- 优先级队列
!!  
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


- 字典键映射多个值  
eg. {k1: [1,2,3]}  
from collections import defaultdict  
d = defaultdict(list)  		# d[key].append(val), if key not in d: d[key] = []
d = defaultdict(set)		# d[key].add(val)  

注意: 也可以使用dict.setdefault(key, default=None)实现类似功能
