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
## tmuxinator  
假如你需要经常创建tmux会话，它包含三个窗格：vim、debug和shell，并且每个窗格需要不同的大小。又或者，你又临时投入另一项工作，需要打开多个终端。你可能会想，如果仅需一条命令就可以做的该多好，好的，tmuxinator出场了  
Tmuxinator 是一个 Ruby 的 gem 包，可用于创建 Tmux 的会话。它的工作方式是先在配置文件中定义会话中的细节，然后用 1 条命令创建出这些会话。下面就让我们看看如何安装 Tmuxinator 以及如何添加配置来为指定项目开启一个会话。可以通过运行如下命令安装 Tmuxinator 的 gem 包  
```
gem install tmuxinator
```
安装好之后，就可以在终端中使用tmuxinator或者缩写mux来启动Tmuxinator了  

* 首先让我们创建一个工程：  
```
mux new project0
```
tmuxinator会在~/.config/.tmuxinator/目录中创建project0.yml文件，编辑project0.yml，写入下列内容(重点提醒：书写时要使用空格缩进，且严格按照图示缩进对其，否则会报语法错误！)：  
```
# ~/.tmuxinator/project0.yml
name: project0
root: ~/
windows:
  - editor:
      layout: main-vertical
      panes:
        - vim
        - top
  - ls: ls
  - netconfig: ifconfig
```
* 启动刚刚创建的项目：  
```
mux start project0
```
你会看到，我们的tmux自动的启动了一个tmux会话，它包含三个窗口，其中第一个窗口包含两个窗格，每个窗体/窗格均执行了指定任务  

### 在tmuxinator中配置layout  
我们可能会需要指定窗格的排班规则，tmuxinator支持设置tmux中的5种默认layout样式：  
```
even-horizontal
         Panes are spread out evenly from left to right across the window.

even-vertical
         Panes are spread evenly from top to bottom.

 main-horizontal
         A large (main) pane is shown at the top of the window and the
         remaining panes are spread from left to right in the leftover
         space at the bottom.  Use the main-pane-height window option to
         specify the height of the top pane.

 main-vertical
         Similar to main-horizontal but the large pane is placed on the
         left and the others spread from top to bottom along the right.
         See the main-pane-width window option.

 tiled   Panes are spread out as evenly as possible over the window in
         both rows and columns.
```
但是默认的5种样式不能让我们自由的设定每个窗格的大小，所以我们要使用自定义的layout，在tmux中可以使用C-b + 方向键调整窗格的大小。tmuxinator中可以直接使用tmux中的layout值，在终端输入tmux list-windows可以查看每个窗口的layout值，我们只需将这个值写入tmuxinator项目配置配置中的layout即可  
