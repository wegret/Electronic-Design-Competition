![image-20241124005648668](https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241124005648668.png)



![焊接实物图](焊接实物图.jpg)

------



[TOC]



# 2019年全国大学生电子设计竞赛 综合测评题



## 一. 材料

LM324AD（四运放）*1

SN74LS00D（四与非门）*1



<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241106164241572.png" alt="image-20241106164241572" style="zoom: 33%;" />

## 二. 任务

- [x] 频率为 $19kHz\sim 21kHz$ 连续可调的方波脉冲信号，幅度不小于 $3.2V$
- [x] 与方波同频率的正弦波信号，输出电压失真度不大于 $5\%$，峰峰值 $(V_{pp})$ 不小于 $1V$。
- [x] 与方波同频率占空比 $5\%\sim 15\%$ 连续可调的窄脉冲信号，幅度不小于 $3.2V$
- [x] 与正弦波正交的余弦波信号，相位误差不大于 $5\degree$，输出电压峰峰值 $(V_{pp})$ 不小于 $1V$

各路信号输出必须引至测评板标注位置并需要接入 $1k\Omega$ 负载电阻 $R_L$.

原则上不允许在测评板上增加使用 BJT、FET 和二极管。



## 三. 方案

首先用与非门做出一个$0$到$5V$的方波，然后用RC网络做滤波器做出正弦波。

用方波下降沿或者上升沿微分出来的脉冲信号，再接一个与非门，做出$0$到$5V$的窄脉冲。

用正弦波接移相器做出余弦波。



## 四. 电路设计和仿真结果

### 方波

用2个与非门做出 $20kHz$ 左右 峰峰值 $5V$ 的方波：

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241112203011374.png" alt="image-20241112203011374" style="zoom:80%;" />

![image-20241112203024590](https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241112203024590.png)

### 正弦波

使用RC网络做滤波器，把方波转换成正弦波。

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241116202828005.png" alt="image-20241116202828005" style="zoom: 50%;" />

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241116202803589.png" alt="image-20241116202803589" style="zoom:50%;" />

大致参数计算
$$
23kHz=\frac{1}{2\pi \cdot RC}\\
RC=6.923\times 10^{-6}\\
R=300\Omega\\
C=22\times 10^{-9} F=22nF
$$




### 窄脉冲

用很小的电容做一个微分脉冲信号，把方波的下降沿转换成窄脉冲。窄脉冲过一个与非门，转成 $5V$ 的窄波。

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241113003038853.png" alt="image-20241113003038853" style="zoom: 80%;" />

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241113003158527.png" alt="image-20241113003158527" style="zoom:50%;" />

### 余弦

正弦信号过一个移相器。

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241113005146324.png" alt="image-20241113005146324" style="zoom:67%;" />

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/353f6a37b3beabc478f2a3937df18ca.png" alt="353f6a37b3beabc478f2a3937df18ca" style="zoom:50%;" />





### 合并电路

![image-20241116202927152](https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241116202927152.png)



<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/image-20241116202435143.png" alt="image-20241116202435143" style="zoom:50%;" />





## 五. 实物制作

在实物时对仿真电路也做出了比较多调整（比如根据实验室的现存材料修改了一些电容电阻的值之类的，以及针对噪声和波形不稳部分狠狠加去耦电容。大致方案没有变化）

其中比较重要的一个部分，是波形不稳，波形不稳导致示波器有模糊部分，窄脉冲存在测不出占空比的情况。经过测试，波形不稳可以通过加大去耦电容实现。

波形不稳形如下图：

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/38284724f1437c92a67b1beb13335eb.jpg" alt="38284724f1437c92a67b1beb13335eb" style="zoom: 67%;" />

我通过在电源和地之间加了470uF的去耦电容后解决。

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/1a9f5d06b943008985933fea9bbcb05.jpg" alt="1a9f5d06b943008985933fea9bbcb05" style="zoom: 67%;" />

除此之外，还进行了调参，特别是移相器部分。针对波形的问题做了一些形如（波形不好看就加电容，幅度不对也加电容）的乱搞调参（划掉）总之最后出来的效果是还可以的，这个方案大致应该没什么问题。

方波窄脉冲同上，剩下的正弦余弦如下：

<img src="https://wegret-pic.oss-cn-beijing.aliyuncs.com/55cac8ce6c760036557eb33cbf2875f.jpg" alt="55cac8ce6c760036557eb33cbf2875f" style="zoom: 67%;" />