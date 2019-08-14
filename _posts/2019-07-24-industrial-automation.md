---
layout: post
title:  "工业自动化"
date:   2019-07-24 12:30:00 +0800
author: 西伯利亚虎
categories: technical
---
本文从实践的角度对工业自动化作简单介绍。

## 自动控制的硬件——控制柜

目前，工业自动控制能够实现操作员远程地通过按钮或程序控制机器的运转，用以实现的标准方式是控制柜，例如高压柜、低压柜、配电柜、变频柜、电气柜、PLC柜等。控制柜通常是与冰箱尺寸类似的箱体，内部有用于固定器件的板子。各种器件的连接关系由图纸（Drawing）表示，使用CAD软件绘制，如AutoCAD、EPLAN。

- [AutoCAD Electrical](https://www.autodesk.com.cn/products/autocad/included-toolsets/autocad-electrical)：由AutoDesk公司开发，包含在AutoCAD中，参考资料较多。
- [EPLAN Electric](https://www.eplan.cn/cn/solutions/product-overview/eplan-electric-p8/):通常需专门培训，方便之处是可以自动生成项目的报表，以及给图纸不同地方的同一器件添加交叉引用标签。

控制柜图纸中的常用器件包括
- CPU，这是PLC程序载入的地方；
- 电源，24VDC或220VAC，通常PLC柜的CPU和I/O接口分开供电，CPU用柜内电源，I/O接口用其它柜的电源；
- 选择开关（SA），通常用于在就地手动控制与自动控制间切换；
- 按钮（如SS），在电路图上有常开与常闭两种；
- 继电器（如KA、KH），实现控制电路与受控电路的电气隔离；
- 交流接触器（KM），控制电机，相当于继电器，实现弱电控制强电；
- 电动机（M）；
- 断路器（如QL），分为微型断路器、塑壳断路器等，用于限流，空气开关也是一种断路器；
- 信号灯（如HG、HR）；
- 端子（如1、2），是用于固定接线的端点；
- 隔离器（GL），接在四线制仪表的模拟输入（AI）后，或模拟输出（AO）后，两种情况下均可能省略；
- 配电器（PD），接在两线制仪表的AI后，所谓四线制仪表是指供电线与信号线分离的仪表，两线制仪表是指供电线作为信号线的仪表，需要使用配电器供电。

国内使用的控制柜器件的主要厂商有德国的西门子公司（Siemens）、法国的施耐德公司（Schneider，看名字会让人误以为是家德国公司）和美国的罗克韦尔公司（Rockwell Allen-Bradley，简称AB）。

### 控制柜举例

现在以下面从[土木在线](https://bbs.co188.com/thread-1842375-1-1.html)摘取的电动阀门控制电气图为例，描述其含义。

![electric valve](/assets/electric-valve.jpg)

图纸中动力电压为三相220V交流电，该控制柜是**低压电气柜**，图纸中如SQ1、SQ2所示的小框内为柜外接线，其他部分为柜内接线。

左侧是通过换相实现三相交流异步电机正反转的主回路图。
右侧是控制回路图。
开关SA起切换就地手动控制与自动控制的作用，后者依赖另一个PLC柜控制。
手动控制模式下，SF为正转按钮，SR为反转按钮。SF闭合时，继电器KM1启动电机正转，同时实现自锁，使得正转按钮抬起后，电机维持正转。当正转使得阀门开到位后，SQ1动作，信号灯HG1亮，KM1回路断开，电机停止正转。SR触发电机反转直至阀门关到位的过程与此类似。

由上面的分析可见，自动控制的核心是PLC。
PLC全称是Programmable Logic Controller，译作可编程逻辑控制器，是一个集成了CPU、IO等模块的系统，集成在**PLC柜**中。
PLC柜比上面图纸中的低压柜复杂得多，通常需要十几到几十张图纸描述，包括柜体图、数字输入（DI）原理图和接线图、数字输出（DO）原理图和接线图、模拟输入（AI）原理图和接线图、模拟输出（AO）原理图和接线图等等。
一个PLC柜可集成上百个这样的DI/O和AI/O接口。

常用的控制柜还有**变频柜**。在变频柜内部可以观察到AC-DC和DC-AC两个较大的转换器，柜子下部可能放有体积较大的电抗器。

除控制系统外，工厂的供电系统也由控制柜组成。电厂送至工厂的电并不是220VAC的市电，而是数kV的高压电。工厂通常使用的是相电压为220VAC的三相电，为此需要将高压电接入**高压柜**降压。高压柜内有多根截面积为几十到上百mm$^2$的母线，母线通常由铜制作，外表面镀锡防止氧化，故呈银白色。工厂电可能需要经过不只一个柜子降压，随后接到**配电柜**上。配电柜内部有数十至上百个断路器，将电分配给不同用电设备使用。

## 自动控制的软件——PLC编程和HMI

自动控制的软件分为下位机软件和上位机软件两类。
下位机软件用来PLC编程，程序编写好后载入CPU中；上位机软件用来制作人机界面（HMI），提供给操作员使用。
不同公司有不同的上位机和下位机软件。

西门子公司的软件生态：
- 西门子公司自动控制的软硬件产品以SIMATIC为品牌。PLC编程软件是[SIMATIC Step 7系列](https://new.siemens.com/global/en/products/automation/systems/industrial/controller-sw.html)。最新的是Step 7 TIA Portal（中文译作博途，TIA是Totally Integrated Automation的首字母缩写），这一软件集成了PLC编程软件和HMI软件，支持的CPU有经典的S7-300系列、S7-400系列，和最新的S7-1200系列、S7-1500系列、ET 200系列等。
- 在TIA Portal以前，西门子公司支持S7-300系列、S7-400系列的PLC编程软件是STEP 7 V5.5。
- 在TIA Portal以前，西门子公司的HMI软件是WinCC。

施耐德公司的软件生态：
- 施耐德公司的PLC编程软件是Unity Pro系列。
- 施耐德公司的HMI软件是[Intouch](https://www.wonderware.com/zh-cn/hmi-scada/intouch/)软件，由Wonderware开发。

> Wonderware的历史：Wonderware公司最初于1987年在美国加州成立，后于1998年被Siebe plc收购（此处的plc是指public limited company，类似于国内的上市公司），1999年随BTR plc和Siebe plc的合并成为合并后的Invensys plc的一部分，而Invensys plc于2014年被施耐德公司收购，2017年又随施耐德工业软件业务与Aveva合并而成为Aveva的一部分，施耐德在合并后的Aveva公司持有60%的股份。

不同公司的软件功能相近，但使用方法不尽相同。这里以施耐德公司的PLC编程软件Unity Pro XL和HMI软件Intouch为例稍作介绍。

### 使用Unity Pro XL进行PLC编程

使用Unity Pro XL进行PCL编程，首先需要新建工程，选择CPU类型和硬件组态，包括供电电源、I/O模块等，随后才可以开始编程。

Unity Pro XL支持多种编程语言，包括LD（Ladder Diagram梯形图）、FBD（功能块图）、IL（指令表）、ST（结构化文本）等，在MAST中新建段时可以对不同的语言进行选择。
其中LD与电气图纸类似，ST与高级程序设计语言类似，使用较为方便。
这些不同语言的段可以一起编译，例如可以使用ST语言调用LD封装的FB（功能块），也可以使用LD语言调用ST封装的FB。
关于这些编程语言的具体介绍可参照[参考手册][programming manual]。

[programming manual]: https://download.schneider-electric.com/files?p_enDocType=User+guide&p_File_Name=35006144_K01_000_22.pdf&p_Doc_Ref=35006144K01000

LD编程的基本方式是选择FB放置到编辑页面上，然后添加连线并添加FB各个输入输出关联的变量，这些变量可以是声明过的变量，也可以是I/O模块的接口。
基本的FB位于菜单栏下的工具区，更多的FB通过工具区的`类型库管理器`可以找到，也可以在`导出的功能块类型`（Derived FB Type）中封装自己定义的FB。用户还可以在`导出的数据类型`（Derived Data Type）中封装自己定义的数据类型，如布尔数组。
常用的FB包括：
- `常开/常闭触点`，对应图纸中的按钮或继电器被控回路，关联EBOOL型变量；
- `线圈`，对应图纸中的继电器，关联EBOOL型变量；
- `TON/TOF/TP`，三个定时器FB，定时模式不同，共同点是均以IN、PT为输入，以Q为输出，其中IN和Q关联EBOOL型变量，PT关联TIME变量或`t#1s`形式的TIME常量；
- `SR`，即SR触发器，以S1、R为输入，以Q为输出，三者均关联EBOOL型变量；
- `EQ/GE/GT/LE/LT/NE_INT/REAL`，比较整型或实型变量间的大小关系；

ST编程与C语言等高级程序设计语言类似，支持多种操作符，支持条件语句、循环语句。下面是交通信号灯ST程序的示例：

```
(* Traffic Lights *)

(* SR trigger block *)
SR_1 (S1 := run_lights, R := stop_lights);

if SR_1.Q1 then
    (* all lights turn green at the same time *)

    (* the "left" light, on 2s, off 4s *)
    TON_1 (IN := TON_2.Q, PT := t#2s);
    TON_2 (IN := NOT TON_1.Q, PT := t#4s);
    left := NOT TON_1.Q;

    (* the "straight" light, on 3s, off 3s *)
    TON_3 (IN := TON_4.Q, PT := t#3s);
    TON_4 (IN := NOT TON_3.Q, PT := t#3s);
    straight := NOT TON_3.Q;

    (* the "right" light, on 4s, off 2s *)
    TON_5 (IN := TON_6.Q, PT := t#4s);
    TON_6 (IN := NOT TON_5.Q, PT := t#2s);
    right := NOT TON_5.Q;

else

    left := 0;
    straight := 0;
    right := 0;

end_if;
```

这段程序实现的功能是，在开启状态下，左转、直行、右转三个信号灯同时变绿、依次变红；在关闭状态下，三个信号灯均为红色。

不论使用何种编程语言，变量或FB在使用前都需要声明。在LD语言中，FB在添加到编辑页面时自动声明；而在ST语言中，变量和FB都需要在基本变量和基本FB实例处手动添加。
变量声明后需要分配地址，Unity Pro XL对

- EBOOL变量地址的表示是`%m`+数字，例如`%m1`；
- INT、REAL变量地址的表示是`%mw`+数字，例如`%mw21`。

在`数据类型`窗口中可以查看变量的物理地址，如`000001`。

完成编程后，在工具栏中选择`生成更改`或`重新生成所有项目`，观察程序是否成功编译。成功编译的程序才能用于仿真或实际运行。
仿真前，需要在`PLC`菜单下选择`仿真模式`；实际运行前，需要在`PLC`菜单下选择`标准模式`，并填写PLC的地址，以与PLC连接。

### 使用Intouch制作HMI

使用Intouch制作HMI，首先需要新建window（窗口）。在window上，可以放置椭圆、矩形、按钮等元素，这些元素继而可以关联到不同的变量，常用的如I/O布尔型、I/O整型、I/O实型。

为在仿真或实际运行中检测Unity Pro XL中的变量，Intouch的变量需要与Unity Pro XL的变量共享物理地址。设置Intouch变量的项目名（地址）时，需要注意有+1的地址偏移，例如Unity Pro XL中`000001`的物理地址在Intouch中对应项目`000002`。
Intouch变量的访问名属性用以区分不同CPU的变量，因为一个HMI可以连接多个PLC柜。

Intouch与Unity Pro XL的仿真需依赖SMC软件中的DAServer起桥梁作用，SMC由Wonderware开发。在Unity Pro XL和DAServer中需要设置相同的IP地址，然后才能开始在Unity Pro XL的PLC菜单下选择连接，在Intouch中选择运行，开始仿真。

在仿真时，注意确保Unity Pro XL下面的提示条均为绿色，显示`HMI读写模式`、`相等`、`上载信息完好`。仿真时修改程序后，需要在Unity Pro XL中重新点击`编译`、`上传至PLC`、`运行`，保证提示条如前述显示。

### 西门子公司的PLC编程软件

STEP 7 V5.5和TIA Portal的使用与Unity Pro XL类似，均需要首先对柜体和组态进行选型，继而开始编程。
支持的编程语言与Unity Pro XL基本相同，均遵循IEC（国际电工委员会，International Eletrotechnical Commission）的相关标准。
不同之处是，编程时将一个文件中的程序限制为多个程序段，且在程序不太复杂时可以自动由一种编程语言的程序转换为另一种编程语言的程序。

西门子公司软件与Unity Pro XL相比，手册在软件中的整合程度更好，在软件中即可查看手册中的各项内容，而Unity Pro XL虽然也支持F1查看帮助，但仍需要额外的用户手册与参考手册。

