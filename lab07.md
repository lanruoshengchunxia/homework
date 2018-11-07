# 封面
实验名称：简单程序&简单循环<br>
学号：18342048<br>
姓名：李佳

# 目录
## 实验目标
## 实验步骤与结果
1) 任务 1：简单程序<br>
（1）打开网页 The PIPPIN User’s Guide ，然后输入 Program 1：Add 2 number<br>
（2）点step after step。观察并回答下面问题：<br>
PC，IR 寄存器的作用。<br>
ACC 寄存器的全称与作用。<br>
用“LOD #3”指令的执行过程，解释Fetch-Execute周期。<br>
用“ADD W” 指令的执行过程，解释Fetch-Execute周期。<br>
“LOD #3” 与 “ADD W” 指令的执行在Fetch-Execute周期级别，有什么不同。<br>
（3）点击“Binary”,观察回答下面问题<br>
写出指令 “LOD #7” 的二进制形式，按指令结构，解释每部分的含义。<br>
解释 RAM 的地址。<br>
该机器CPU是几位的？（按累加器的位数）<br>
写出该程序对应的 C语言表达。<br>

2) 任务 2：简单循环<br>
（1） 输入程序Program 2，运行并回答问题：<br>
用一句话总结程序的功能<br>
写出对应的 c 语言程序<br>
（2） 修改该程序，用机器语言实现 10+9+8+..1 ，输出结果存放于内存 Y<br>
写出 c 语言的计算过程<br>
写出机器语言的计算过程<br>
用自己的语言，简单总结高级语言与机器语言的区别与联系。<br>

## 实验小结

# 实验目标
理解冯·诺伊曼计算机的结构<br>
理解机器指令的构成<br>
理解机器指令执行周期<br>
用汇编编写简单程序<br>

# 实验步骤与结果
## 任务 1：简单程序

![](https://github.com/lanruoshengchunxia/swi-homework/raw/gh-pages/images/硬件编程1.png)

### 点step after step。观察并回答下面问题：
1) IR：指令寄存器，用来保存当前正在执行的一条指令 <br>
PC：程序计数器，存放下一条指令在内存中的地址 <br>
2) ACC(Accumulator)：累加寄存器，功能是当运算器的算术逻辑单元(ALU)执行全部算术和逻辑运算时，为ALU提供一个工作区，暂时存放ALU运算结果<br>
3) Main memory <br>
→ fetch instruction  PC根据地址从RAM取出指令 LOD#3<br>
→ Registers 指令传入IR<br>
→ Decode instruction 指令传入Decoder  <br>
→ Get data  无需取址，数字3传入MUX<br>
→ Execute the instruction 数字3传入ALU后传入ACC<br> 
→ Main memory<br>

4) Main memory <br>
→ fetch instruction PC根据地址从RAM中取出指令 ADD W<br> 
→ Registers 指令传入IR<br>
→ Decode instruction 指令传入Decoder <br>
→ Get data ALU从ACC中取值,IR再次访问RAM中的W，从W中取值，W的值读入ALU<br>
→ Execute the instruction ALU执行加法，结果传入ACC<br> 
→ Main memory<br>

5) LOD #3只需访问RAM一次,而ADD W需要两次访问RAM

![](https://github.com/lanruoshengchunxia/swi-homework/raw/gh-pages/images/硬件编程2.png)
### 点击“Binary”,观察回答下面问题:
1) 00010100 00000111<br>
前八位称命令指示，第四位为寻址模式，例子中为1，表述操作数是数值；后八位称为操作数，表示数值或地址，例子中表示数值7。整个例子表示加载数值3。
2) 只用于暂时存放程序和数据，一旦关闭电源或发生断电，其中的程序和数据就会丢失
3) 16位
4) int w=3;<br>
int x=7;<br>
int y=x+w;<br>


## 任务 2：简单循环
![](https://github.com/lanruoshengchunxia/swi-homework/raw/gh-pages/images/硬件编程3.png)
### 输入程序Program 2，运行并回答问题：
1) 使X不断减1直到X等于0；
2) int x;
if(x>0){
    x--;
}
### 修改该程序，用机器语言实现 10+9+8+..1 ，输出结果存放于内存 Y
1) int x=10;<br>
int y=0;<br>
if(x>0){<br>
    y+=x;<br>
    x--;<br>
}<br>

2) 汇编：<br>
LOD #10<br>
STO W<br>
LOD Y<br>
ADD W<br>
STO Y<br>
LOD W<br>
JMZ 20<br>
SUB #1<br>
STO W<br>
JMP 4<br>
HLT<br>


机器：<br>



# 实验小结
1) 理解冯·诺伊曼计算机的结构<br>
![](https://github.com/lanruoshengchunxia/swi-homework/raw/gh-pages/images/冯诺依曼.png)<br>
2) 理解机器指令的构成<br>
机器指令通常由操作码和操作数两部分组成，操作码指出该指令所要完成的操作，即指令的功能，操作数指出参与运算的对象，以及运算结果所存放的位置等。
3) 理解机器指令执行周期<br>
Main memory 
→ fetch instruction 
→ Decode instruction 
→ Registers 
→ Get data 
→ Execute the instruction 
→ Main memory<br>
4) 用汇编编写简单程序<br>




