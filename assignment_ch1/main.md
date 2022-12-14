# 计算机体系结构基础 - 第 1 章作业

## 1.1 
计算机系统可划分为哪几个层次，各层次之间的界面是什么？你认为这样划分层次的意义何在？

**解**

计算机系统可划分为四个层次：应用程序、操作系统、硬件系统、晶体管。应用程序与操作系统之间的界面是应用程序编程接口 API，操作系统与硬件系统之间的界面是指令系统 ISA，硬件系统与晶体管之间的界面是工艺模型。

这样划分层次，通过抽象的方式降低了上层用户操作计算机的复杂度，通过统一界面的方式提升了各个层次的可移植性和通用性。各个层次之间，在满足界面要求的情况下可以独立发展，促进了计算机的发展。

## 1.2
在三台不同指令系统的计算机上运行同一程序 P 时，A 机器需要执行 $1.0 \times 10^9$ 条指令，B 机器需要执行 $2.0 \times 10^9$ 条指令，C 机器需要执行 $3.0 \times 10^9$，但三台机器的实际执行时间都是 $100$ 秒。请分别计算出这三台机器的 MIPS，并指出运行程序 P 时哪台机器的性能最高。

**解**

A 机器的 MIPS 是 $1.0 \times 10^9 \div 100 \div 10^6 = 10$；  
B 机器的 MIPS 是 $2.0 \times 10^9 \div 100 \div 10^6 = 20$；  
C 机器的 MIPS 是 $3.0 \times 10^9 \div 100 \div 10^6 = 30$。

三者运行同一程序 P 时，花费的时间相同，因此性能相当。

## 1.3
假设某程序中可向量化的百分比为 $P$，现在给处理器中增加向量部件以提升性能，向量部件的加速比是 $S$。请问增加向量部件后，处理器运行该程序的性能提升幅度是多少？

**解**
设原处理器执行这一程序需要 $t$ 秒，则可向量化的部分需要 $tP$ 秒，其余部分需要 $t - tP$ 秒。

增加向量部件后，可向量化的部分仅需 $tP / S$ 秒，总运行时间为 $t - tP + tP/S$，其时间消耗是原来的 $(1 - P + P/S)$ 倍。

性能提升幅度为：$\displaystyle 1 / (1 - P + P/S) - 1 = \frac{PS - P}{S - PS + P}$

## 1.4
处理器的功耗可简单分为静态功耗和动态功耗两部分，其中静态功耗的特性满足欧姆定律，动态功耗在其他条件相同的情况下与频率成正比。现对某处理器进行功耗测试，得到如下数据：关闭时钟，电压 $1.0 \text{V}$ 时，电流为 $100 \text{mA}$；时钟频率为 $1 \text{GHz}$，电压 $1.1 \text{V}$ 时，电流为 $2100 \text{mA}$。请计算此处理器在时钟频率为 $2 \text{GHz}$、电压为 $1.1 \text{V}$ 时的总功耗。

**解**

电压为 $1.1 \text{V}$ 时，处理器静态功耗对应的电流为：
$$
I_{\text{静态}2} = \frac{100 \text{mA}}{1.0 \text{V}}\times 1.1 \text{V} = 110 \text{mA}
$$

时钟频率为 $1 \text{GHz}$，电压 $1.1 \text{V}$ 时，处理器动态功耗对应的电流为：
$$
I_{\text{动态}2} = I_2 - I_{\text{静态}2} = 1990 \text{mA}
$$

由于动态功耗在其他条件相同的情况下与频率成正比，则时钟频率为 $2 \text{GHz}$、电压为 $1.1 \text{V}$ 时，处理器动态功耗对应的电流为：
$$
I_{\text{动态}3} = \frac{2 \text{GHz}}{1 \text{GHz}} \times 1990 \text{mA} = 3980 \text{mA}
$$

此时总电流为：
$$
I_3 = I_{\text{动态}3} +I_{\text{静态}3} = I_{\text{动态}3} +I_{\text{静态}2} = 4090 \text{mA}
$$

故此处理器在时钟频率为 $2 \text{GHz}$、电压为 $1.1 \text{V}$ 时的总功耗为：
$$
P_3 = U_3 \times I_3 = 4499 \text{mW} = 4.499 \text{W}
$$

## 1.5
在一台个人计算机上进行 SPEC CPU2000 的测试，分别给出无编译优化选项和编译优化选项为 `-O2` 的测试报告。

**解**

|SPEC 程序|`-O0` 运行时间 / 秒|`-O0` 分值|`-O2` 运行时间 / 秒|`-O2` 分值|
|:-|:-:|:-:|:-:|:-:|
|164.gzip|76.5|1830|121|1161|
|175.vpr|55.3|2530|101|1380|
|176.gcc|27.9|3938|X|X|
|181.mcf|72.4|2488|90.1|1997|
|186.crafty|28.4|3516|41.1|2430|
|197.parser|93|1935|155|1160|
|252.eon|X|X|232|560|
|253.perlbmk|X|X|72.1|2496|
|254.gap|31.6|3476|31.1|3538|
|255.vortex|46.6|4079|85.3|2227|
|256.bzip2|60.3|2486|129|1166|
|300.twolf|83.6|3587|150|1998|
|SPEC_INT2000||2878 ||1640 |
|168.wupwise|X|X|104|1535|
|171.swim|X|X|164|1886|
|172.mgrid|X|X|334|539|
|173.applu|X|X|286|734|
|177.mesa|33.8|4143|68.3|2051|
|178.galgel|X|X|X|X|
|179.art|23.3|11148|51.2|5078|
|183.equake|X|X|X|X|
|187.facerec|36.7|5176|76.2|2493|
|188.ammp|X|X|173|1273|
|189.lucas|X|X|69|2899|
|191.fma3d|X|X|124|1687|
|200.sixtrack|X|X|257|429|
|301.apsi|54.8|4746|200|1297|
|SPEC_INT2000||5804 ||1471 |


根据分数可以看出，使用 `-O2` 优化后，SPEC CPU2000 的评分大约是无编译优化时 2 倍。但优化造成了大量的测试点运行结果出现偏差，对性能提升可能有副作用。

## 1.6
分别在苹果手机、华为手机以及 X86-Windows 机器上测试浏览器 Octane 的分值，并简单评述。

**解**
|  手机类型   |          型号          |         处理器          | 得分  | 备注                      |
| :---------: | :--------------------: | :---------------------: | :---: | :------------------------ |
|  苹果手机   |        iPhone X        |       A11 Bionic        | 34089 | 结果来自于李国峰同学。    |
|  华为手机   |     HUAWEI P30 Pro     |    HUAWEI Kirin 980     | 18402 | 结果来自于钱瑾珈同学。    |
|  小米手机   |       Xiaomi 10        | Qualcomm Snapdragon 865 | 19528 | 自测。                    |
| X86-Windows | ThinkPad X1 Carbon 6th |   Intel Core i5-8350U   | 36192 | 自测，使用 Chrome 浏览器  |
| X86-Windows | ThinkPad X1 Carbon 6th |   Intel Core i5-8350U   | 30820 | 自测，使用 Firefox 浏览器 |

可以注意到，华为和小米两台手机的得分相差不大，而苹果手机的得分远高于华为和小米。尽管他们都是用的是 ARM 架构的处理器，但处理器的设计水平可能有相当大差异。此外，iOS 与 Android 的系统平台不同，也可能会影响到得分。

苹果手机的测试得分几乎与 X86 机器相同，足以说明苹果的芯片、系统效率非常高。对比来看，在同一机器上使用 Firefox 和 Chrome 导致了 6000 多分的差异，说明浏览器对 JavaScript 的实现对性能也有较大的影响，Chrome 的 JavaScript 引擎要优于 Firefox。