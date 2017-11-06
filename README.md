tmux配置文件  
==========
## 概念  
tmux不是终端模拟器，不是命令解释器。它只是一个实现多窗口的工具，因为ubuntu默认的终端模拟器不支持多窗口。虽然tmux支持分屏，但是每次打开终端都需要分一下未免太过繁琐，于是它的基友tmuxinator能够保存分屏后的详细配置，下次启动时便是你设置好的样子。文件.tmux.conf是tmux的配置文件，project0.yml是我的分屏配置文件  
## 快捷键  
### 会话  
```
需要加<prefix>前缀
:new session_name new session
s  list session
$  name session
下面的命令让你在shell中操纵tmux
tmux ls   列出所有会话
tmux a    恢复至上一次的会话
tmux a -t foo 恢复名称为foo的会话，会话默认名称为数字
tmux kill-session -t foo  删除名为foo的会话
tmux kill-server  删除所有会话
```
### 窗口  
```
加<prefix>
c create
w list
n next
p previous
f find window
, rename window
& kill window
```
### 页面  
```
加<prefix>
-  横向分屏
|  竖向分屏
x  kill pane
+ break pane into window
z 最大化当前页面
```
### 系统指令  
```
d detach 断开当前会话
r reload 强制重载当前会话
t big clock显示时间
? shortcuts显示快捷键帮助文档
: prompt
```
