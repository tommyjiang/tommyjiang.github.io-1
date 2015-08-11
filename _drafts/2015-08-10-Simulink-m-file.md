---
layout: post
title: Matlab 中利用 m 文件修改 Simulink 中模型参数的方法
categories: [技术]
tags: [电力系统, Matlab]
icon: code
---
介绍在 Matlab 中利用 m 文件修改 Simulink 中模型参数的方法。

### 电力系统仿真工具
我个人博士论文的隐名评审意见中有如下评语：

```
除第二章的简单实验外，本文的所有结论均源于仿真，这大大降低了本文的创新性和说服力。
```

说实话，和任何事一样，博士毕业其实是实力和运气综合作用的结果，尤其是研究生院负责的论文盲审环节，虽然可以填最多3个需要回避的老师，但也容易送到学术观点有争议或者导师的“宿敌”手中。比如我个人的这个评审意见——审我论文的这位老师很有可能是电力电子方向而不是电力系统方向的，因为电力系统方向的老师肯定清楚，目前电力系统领域的绝大多数研究，只能依靠仿真，因此不太会给出上述评语。但我还是应该感谢下这位老师，因为他虽然在评审时给了我2个C（一共4小项），但最后总评很厚道地给了个B，不然我还要继续在学校读博……

说回电力系统的仿真工具，我个人了解的有以下软件：BPA、PSASP、Matlab/Simulink、PSCAD、PSS/E、PowerFactory、RTDS、RT-Lab、PXI……这方面可以参考[武大曹博的PPT](http://wenku.baidu.com/link?url=lyB8iBkcX7HUakjhmgnWHX0xNV7-E3RIWFrzxDXEgmgs4NYdomg6YlY2hBDBSOuXJ8JWKW0Amu6lZMeB_8HzXz4yjLper1sGNdGPOJajAQO)，里面有关于各软件的详细说明和对比。就我个人而言，更喜欢用*纯代码*进行仿真，原因是纯代码调试起来更为方便，而且也更容易进行版本管理。但电力系统仿真中应用纯代码的情形毕竟较少，一般与优化相关的研究更偏好用纯代码，但动态仿真绝大多数时候还是要用 GUI 仿真软件。

Matlab/Simulink 就是一个常用的仿真工具，它的突出优点是可以和 Matlab 代码完美对接。但利用 Simulink 模型进行仿真时，如果需要在某些时刻改变系统参数，利用 GUI 界面进行设置会比较麻烦，可以利用 m 文件实现，具体方法如下。

### m 文件修改 Simulink 模型参数的方法
利用 m 文件修改 Simulink 模型参数方法的总体思想如下：首先在初始参数下仿真 t_1 时间，记录该时间结束时系统所有状态量的值，之后更改系统参数，以之前记录的系统所有状态量的值作为初值，重新进行仿真，如此循环往复。

可以在 m 文件中利用`set_param`函数设置 Simulink 模型仿真的相关参数：

```matlab
set_param('ModelName','LoadInitialState','off',...
          'SaveFinalState','on','SaveCompleteFinalSimState','on','FinalStateName','xFinal',...
          'StartTime','0','StopTime','1');
```

其中`ModelName`为 Simulink 模型的文件名，注意第一次仿真时初值均为0，因此`LoadInitialState`这个选项要设置为`off`，之后的仿真中则需要均设置为`on`。第2行对应的是保存系统状态量终值的相关设置，其中`FinalStateName`为终值存储的变量名，之后仿真的初值需要设置为该变量名。

### 相关问题

#### 仿真继续时提示仿真时间与初始值时刻不同

利用以上代码实现 m 文件修改 Simulink 模型参数继续仿真的过程中，会遇到如下警告：

```
Warning: The start time of model 'Exp2_1_SimModel' is different from the start time saved in the initial SimState. The start time has therefore been reset to 0. 
```

但最后的仿真结果对应的变量中，时间是从0开始一直到仿真结束时刻，并未出现上述警告中提到的将仿真起始时间设置为0。我又试了试直接在 Simulink 中加载初始值然后仿真，并未出现上述警告。由于该警告对仿真结果并无影响，因此可以暂时忽略，之后如果解决了当然最后，解决不了也无大碍。

#### Simulink 模型中参数无法改变

电力系统的仿真一般采用 Simulink 中的 SimPower 模块，我搭了一个单相半桥 PWM 的仿真模型，可以改变该模型中的调制比参数 m 以及电容电压 V_DC，但无法改变反电势电源的电压幅值 Vs 和支路电阻/电感，修改后者后 Matlab 会报以下错误：

```
Simulink cannot load the initial SimState because the model,'Exp2_1_SimModel', was changed after the SimState was saved. Run the simulation again and resave the SimState.
```

目前还没找到太好的解决方法，只能采用变通的方法。例如修改反电势电源电压幅值可以等效为修改调制比 m，二者对应的电流波形是相同的。
