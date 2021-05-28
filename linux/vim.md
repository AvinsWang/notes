# vim shortcut


## global
:h		# help
:sav		# save as
:clo		# close current window, but can't close last window
K		# open man in cursor word


## cursor movement, 鼠标移动  
h j k l		# move curosr  

- 页面中移动  
H		# move to head of current page  
M		# move to middle of current page  
L		# move to tail of current page  

- 单词跳转
w/W		# jump to head of next word  
e/E		# jump to end of next word  
b/B		# jump to head of previous word  

%		# jump to matching character, eg, () {} []  

- 行首,行尾跳转  
0		# jump to head of the line  
^		# jump to first no-blank character  
$		# jump to end of the line  
g_		# jump to last no-blank character  

- 文档跳转  
gg		# go to head of document  
G 		# go to end of document  
5gg/5G		# go to line 5

- 声明跳转  
gd		# move to local declaration, 本地声明  
gD		# move to global declaration, 全局声明  

- 字符跳转  
fx		# 跳转到下一个字符x
tx		# 跳转到下一个字符x之前
Fx		# 跳转到上一个字符x
Tx		# 跳转到上一个字符x之后
;		# 重复f,t,F,T操作
,		# 撤销f,t,F,t操作

- 段落跳转
}		# 下一段落尾部
{		# 上一段落尾部

- 屏幕移动   
zz		# 鼠标所在行居中, 鼠标不移动  
Ctrl+e		# 鼠标所在行下移一行  
Ctrl+y		# 鼠标所在行上移一行  
Ctrl+b		# 上移一屏  
Ctrl+f		# 下移一屏  
Ctrl+u		# 上移半屏
Ctrl+d		# 下移半屏  


## 
