# -进程脚本进阶
## 查看进程进程ps  
- ps [OPTION]  
- 支持三种选项  
    UNIX选项   如-A  -e  
    BSD选项   如a
    GNU选项 如--help  
-选项：默认显示当前终端中的进程  
   a 选项包括所有终端中的进程  
  x 选项包括不链接终端的进程  
  u选项显示进程所有者的信息  
  f选项显示进程树，相当于--forest  
  k|--sort 属性 对属性排序，属性前加-表示倒序  
  o 属性...选项显示定制的信息pid、cmd、%cpu、%mem  
  L显示支持的属性列表

  ps输出属性  
VSZ:Virtual memory SiZe，虚拟内存集，线性内存  
RSS：ReSident Size，常驻内存集  
STAT：进程状态  
R:running   运行
S:interruptable sleeping  可中断
D:uninterruptable sleeping  不可中断
T:stopped  停止
Z:combie  僵尸
+:前台进程  
l：多线程进程  
L：内存分页并带锁  
N：低优先级进程  
<：高优先级进程  
s：session leader，会话（子进程）发起者  

ps axo pid,%cpu,%mem,cmd

renice -n -20 4070  把“4070”的优先级改成-20

dd if=/dev/zero of=/dv/null

# 系统工具  
- uptime  
显示当前时间，系统已启动的时间、当前上线人数，系统平均负载（1、5、10分钟的平均负载，一般不会超过1）
- 系统平均负载：  
指在特定时间间隔内运行队列中的平均进程数  
- 通常每个CPU内核的当前活动数不大于3，那么系统的性能良好。如果每个CPU的任务数大于5，那么此主机的性能又严重问题  
- 如果linux主机是1个双核CPU，当Load Average为6的时候说明机器已经被充分使用  

## 进程管理工具  
- top：有许多内置命令  
排序：
P：以占据的CPU百分比，%CPU  
M：占据内存百分比，%MEM  
T：累计占据CPU时常，TIME+  
首部信息显示：
uptime信息： l命令  
tasks及cpu信息：t命令  
cpu分别显示：1（数字）  
memory信息：m命令  
退出命令：q  
修改刷新时间间隔：s
终止指定进程：k
保存文件：W

## 进程管理工具
-选项：
-d#  指定刷新时间间隔。默认为秒  
-b全部显示所有进程   
-n# 刷新多少次后退出  
-H 线程模式，示例：top -H -p1'pidorf mysqld'  
- htop命令：EPEL  
选项：
-d#  指定延迟时间  
-u UserName 仅显示指定用户的进程  
-s COLUME：以指定字段进行排序  
子命令：
s：跟踪选定进程的系统调用  
l：显示选定进程打开的文件列表  
a：将选定的进程绑定至指定CPU核心  
t：显示进程树  

## 内存空间  
-内存空间使用状态：  
   free[OPTION]
 -b 以字节为单位  
  -m以MB为单位  
-g 以GB为单位  
-h 易读格式  
-o 不显示-/+buffers/cache行  
-t 显示RAM +swap的总和  
-s n 刷新间隔为n秒  
-c n刷新n次后即退出  

## 条件选择if语句
-选择执行
-注意：if语句可嵌套
-单分支
   if判断条件;then
        条件为真的分支代码
   fi
-双分支
    if判断条件；then
       条件为真的分支代码
   else
    条件为假的分支代码
   fi
## if语句  
-多分支
 if判断条件1；then  
 条件1为真的分支代码  
elif判断条件2；then  
  条件2为真的分支代码    
elif判断条件3；then  
  条件3为真的分支代码  
 else  
  以上条件都为假的分支代码  
  fi  
-逐条件进行判断，第一次遇到为“真”条件时，执行其分支，而后结束整个if语句  
## 条件判断：case语句  
case变量引用 in  
PAT1）  
     分支1  
    ；；  
PAT2）  
        分支2  
    ；；  
...  
*)  
      默认分支  
     ；；  
esac  

case支持glob风格的通配符：  
*：任意长度任意字符  
？：任意单个字符  
[]:指定范围内的任意单个字符  
a|b：a或b  

ffor循环  
- for 变量名 in 列表；do  
循环体  
  done  
-执行机制：  
依次将列表中的元素赋值给“变量名”；每次赋值后即执行一次循环体；直到列表中的元素耗尽，循环结束  

## for循环  
-列表生成方式：  
（1）直接给出列表  
（2）证书列表：  
（a）{start..end}  
(b)$(seq[start[step]]end)  
(3)返回列表的命令   
$（COMMAND） 
 	(4)使用glob，如：*.sh  
（5）变量引用；  
$@,$*  
killalll bash   断开  
seq 打出来   
-n 不换行  

rename "jpg"   "log" *  
把ipg后缀 改成log 后缀  
最后加 wait  后台执行的程序退出  
## SHELL脚本编程进阶    
- until：CONDITION；do    
- done   
- 进入条件：CONDTIONw为fale  
- 退出条件：CONDITION为true   
## 循环控制语句continue  
- 用于循环体中  
- continue [N]：提前结束第N层的本轮循环，而直接进入下一轮判断；最内层为第1层  
while CONDTITON1;do  
CDD1  
...  
if CONDITION2；then  
continue  
fi  
     CMDn  
...  
done  
## 循环控制语句break  
- 用于循环体中  
- break [N]:提前结束第N层循环，最内层为第1层  
while CONDTITION1;do   
CMD1  
...  
if CONDITION2;then  
    break  
fi  
CMDn  
....  
done  

## 特殊用法  
- while 循环的特殊用法（便历文件的每一行）  
while read line;do  
循环体   
done < /PATH/FROM/SOMEFILE文件中的每一行，且将行赋值给变量line  
## select循环与菜单  
- select variable in list  
do  
循环体命令  
done  
- select 循环主要用于创建菜单，按数字顺序排列的菜单项将显示在标准错误上，并显示ps3提示符，等待用户输入  
- 用户输入菜单列表中的某个数字。执行相应的命令  
- 用户输入被保存在内置变量REPLY中  
- select是个循环体，因此要记住用break命令退出循环，或用exit命令终止脚本。也可以按ctrl+c退出循环  
- select经常和case联合使用  
- 与for循环类似，可以省略in list，此时使用位置参量  

## 定义函数  
- 函数由两部分组成：函数名和函数体  
- help function  
- 语法一：  
f_name (){  
...函数体...  
}  
- 语法二：  
function f_name{  
...函数体...  
}   
- 语法三：  
function f_name(){  
...函数体...  
}
