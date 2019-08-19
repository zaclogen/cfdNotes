# 2019/7 - 2019/8/5
## 1 第一部分 基本思想和方程
### 第一章 计算流体力学的基本原理
介绍流体力学的基本原理和概念，推导和讨论流体力学的基本控制方程组。

---

# 2019/8/6
### 2 第二章 流体力学的控制方程
本书中最重要的一章，“如果从物理上理解每一个方程(甚至方程中的每一项)的意义，我们又怎么能够指望对数值求解这些方程所得到的CFD结果作出正确的解读呢？”
#### 2.1 引言  
#### 2.2 流动模型
1. 有限控制体
   - 我们不是同时观察整个流场，而是借助控制体，将我们的注意力集中在控制体本身这一有限区域内的流体。
2. 无穷小流体微团
   - 流体微团无限小的含义与微积分中的无限小的含义相同，但是它又必须足够大，大到包含了大量的流体分子，使它能够被看成是连续介质。
3. 注释
   - 区分守恒与非守恒
   - 第三种流动模型，微观处理方法，分子运动论
#### 2.3 物质导数(运动流体微团的时间变化率)
   - 适用于流体微团的模型
   - 描述流体微团在笛卡尔坐标系下的运动
   - 物质导数$\text{D} / \text{D}t$物理上表示跟踪一个运动流体微团的时间变化率
   - 当地导数$\partial / \partial t$物理上表示固定点处的时间变化率
   - <font color = "#dd0000"> 这是红色文字 </font>
   -  迁移导数$V\cdot \nabla$: 由于流体微团从流场中一点运动到另一点，流场的空间不均匀性而引起的时间变化率

#### 2.4 速度散度及其物理意义
   - <font color = "#dd0000">速度散度$\nabla \cdot V$: 每单位体积运动着的流体微团，体积相对变化的时间变化率 </font>
   - 模型：<font color = "#0000dd">随流体运动的控制体，质量固定不随时间变化，密度、体积和控制面随时间改变 </font>
- 思考：

<div align="center">
   <img src="https://i.imgur.com/xXk9T5r.png" height="400" >
</div>

- 左上：有限控制体模型，控制体内流体质量变化，控制体体积和形状不变，空间位置固定；
- 右上：有限控制体模型，控制体内流体质量不变，控制体体积和形状改变，空间位置随流体运动；
- 左下：无穷小流体微团模型，微团内流体质量变化，微团体积和形状不变，空间位置固定；
- 右下：无穷小流体微团模型，微团内流体质量不变，？？（形状和面积是否可视为不变呢？？），空间位置随流体运动。

#### 2.5 连续性方程
- 物理学原理：质量守恒
- 流动模型：图2-2中四个模型


# 2019/8/7
<div align = "center">
<img src="https://i.imgur.com/fTZAA7X.png" height = "400">
</div>

---
1. 空间位置固定的有限控制体模型
``` json
通过控制面S流出控制体的净质量流量 = 控制体内质量减少的时间变化率
```

$$\frac{\partial}{\partial t} \iiint_{\mathscr{V}} \rho \mathrm{d} \mathscr{V}+\iint_{S} \rho V \cdot \mathrm{d} S=0$$

- 控制体有限的体积就是方程具有积分形式的原因
- 控制体空间位置固定决定了守恒形式

---
2. 随流体运动的有限控制体模型
- 控制体有限的体积 => 积分形式
- 控制体随流体运动 => 非守恒形式
- 有限控制体由无数个无穷小的流体微团组成，并具有固定不变的总质量，那么<font color="#dd0000">这些不变质量总的物质导数等于零</font>
- $$\frac{\mathrm{D}}{\mathrm{D} t} \iiint_{\mathscr{V}} \rho \mathrm{d} \mathscr{V}=0$$

---
3. 空间位置固定的无穷小微团模型
<div align = "center">
<img src="https://i.imgur.com/TF2Q2d4.png" height="500">
</div>

- **好像大部分教科书，都是根据这个模型推导的方程**
- 注意图2-7中，x方向的净流出量为，图上有错误
- $$\left[\rho u+\frac{\partial(\rho u)}{\partial x} \mathrm{d} x\right] \mathrm{d} y \mathrm{d} z-(\rho u) \mathrm{d} y \mathrm{d} z=\frac{\partial(\rho u)}{\partial x} \mathrm{d} x \mathrm{d} y \mathrm{d} z$$
- y方向的净流出量为：
- $$\left[\rho v+\frac{\partial(\rho v)}{\partial y} \mathrm{d} y\right] \mathrm{d} x \mathrm{d} z-(\rho v) \mathrm{d} x \mathrm{d} z=\frac{\partial(\rho v)}{\partial y} \mathrm{d} x \mathrm{d} y \mathrm{d} z$$
- z方向的净流出量为：
- $$\left[\rho w+\frac{\partial(\rho w)}{\partial z} \mathrm{d} z\right] \mathrm{d} x \mathrm{d} y-(\rho w) \mathrm{d} x \mathrm{d} y=\frac{\partial(\rho w)}{\partial z} \mathrm{d} x \mathrm{d} y \mathrm{d} z$$
- 守恒方程为：
-  $$\frac{\partial \rho}{\partial t}+\left[\frac{\partial(\rho u)}{\partial x}+\frac{\partial(\rho v)}{\partial y}+\frac{\partial(\rho w)}{\partial z}\right]=0$$
或(偏微分形式)

$$\frac{\partial \rho}{\partial t}+\nabla \cdot(\rho V)=0$$

- 微团的无穷小 => 偏微分形式
- 微团空间位置固定 => 守恒形式
- **总结**：<font color="#dd0000">由空间位置固定的流动模型直接导出的控制方程定义为守恒型方程</font>

---

1. 随流体运动的无穷小微团模型
- 流体微团模型，这个流体微团有固定的质量，但它的形状和体积会在它向下游运动时变化
-  $$\frac{\mathrm{D}(\rho \delta \mathscr{V})}{\mathrm{D} t}=\delta \mathscr{V} \frac{\mathrm{D} \rho}{\mathrm{D} t}+\rho \frac{\mathrm{D}(\delta \mathscr{V})}{\mathrm{D} t}=0$$
(*全导数分部展开)

**或**

$$\frac{\mathrm{D} \rho}{\mathrm{D} t}+\rho\left[\frac{1}{\delta \mathscr{V}} \frac{\mathrm{D}(\delta \mathscr{V})}{\mathrm{D} t}\right]=0$$

其中方括号内为**体积相对变化的时间变化率**, 即**速度散度**

$$  \frac{\mathrm{D} \rho}{\mathrm{D} t}+\rho \nabla \cdot V=0 $$
- 微团的无穷小 => 偏微分形式
- 微团随流体运动 => 非守恒形式
- 总结：由随流体运动的流动模型直接导出的控制方程定义为**非守恒型方程**

---

5. 方程不同形式之间的转化
- 上述四个方程是同一个方程(连续性方程)的四种不同形式
- 守恒形式下，积分 => 微分 使用散度定理(高斯定理)
- 微分形式下，守恒 => 非守恒 使用物质导数(输运方程)
  - $$\nabla \cdot(\rho \boldsymbol{V}) \equiv(\rho \nabla \cdot \boldsymbol{V})+\left(\boldsymbol{V} \cdot \nabla_{\boldsymbol{\rho}}\right)$$
  - 体积分的积分限由同样的运动微团确定，所以物质导数可以写到积分号之内
  - $$ \frac{\mathrm{D}}{\mathrm{D} t} \iiint_{\mathscr{V}} \rho \mathrm{d} \mathscr{V}=\iiint_{\mathscr{V}} \frac{{\mathrm{D}} (\rho \mathrm{d}\mathscr{V})} {\mathrm{D} t} = 0 $$
 
    - $\mathrm{d} \mathscr{V}$在物理上代表一个自身可变的无穷小控制体，$\rho$和$\mathrm{d} \mathscr{V}$乘积的物质导数为：
    - $$ \iiint_{\mathscr{V}} \frac{{\mathrm{D}} \rho } {\mathrm{D} t} \mathrm{d}\mathscr{V} + \iiint_{\mathscr{V}} \rho \frac{\mathrm{D}(\mathrm{d}\mathscr{V})}{\mathrm{D} t}= 0 $$
    - 变换可得到速度的散度：
    - $$ \iiint_{\mathscr{V}} \frac{{\mathrm{D}} \rho } {\mathrm{D} t} \mathrm{d}\mathscr{V} + \iiint_{\mathscr{V}} \rho \left [\frac{1}{\mathrm{d} \mathscr{V}}\frac{\mathrm{D}(\mathrm{d}\mathscr{V})}{\mathrm{D} t}\right ] \mathrm{d}\mathscr{V}= 0 $$

---

6. 积分形式与微分形式的重要注释
- 实质区别：
  - 积分形式允许在（空间位置）固定的控制体内出现间断
  - 微分形式的控制方程假定流动参数是可微的，从而必须是连续的
  - 积分 => 微分 运用了散度定理，散度定理要求数学上的连续性
- 积分形式方程更基础更重要。在流动包含真实的间断（如激波）时，这一点尤其重要

---

# 2019/8/8

### 2.6 动量方程
- 物理学原理 牛顿第二定律$F = m a$
- 流动模型  2-2b运动流体微团模型(与连续性方程不同，推导动量方程较复杂), 因为该模型推导动量方程和能量方程尤其方便

<div align="center">
<img src="https://i.imgur.com/EIMmO3j.png" height="400">
</div>

- 作用与微团上力的总和 = 微团的质量乘以微团运动时的加速度
  - 体积力：直接作用在流体微团的整个体积微元上的力，而且作用是超距离的，如重力、电磁力、磁场力
  - 表面力：直接作用在流体微团的表面。只能由两种原因引起：
    - 1. 由包在流体微团周围的流体所施加的，作用于微团表面的**压力分布**；
    - 2. 由于外部流体推拉微团而产生的，以摩擦的方式作用于表面的**切应力和正应力分布**。

---
#2019/8/9
上午快速阅读完成第二章流体力学控制方程，回头还要详细阅读做笔记
下午打算读一个小时的书
下午没看多少，在鼓捣pdf转html的事，还搞了下vim_ahk上面的快捷键

---

#2019/8/12
今天阅读了3.4节不同偏微分方程的一般性质，只快速阅读，未做细致整理

#### 3.4.1 双曲型方程
- 概念
  - 左行，右行
  - 影响区，依赖区
  - 时间推进
- 典型双曲型流动
  - 定常无粘超声速流动(欧拉方程)
  - 非定常无粘流动(欧拉方程)
#### 3.4.2 抛物型方程
- 与双曲型方程一样，适合于推进求解
- 典型流动模型
  - 定常边界层流动
    - 边界层内，NS方程简化为边界层方程(抛物型的),
  - “抛物化”粘性流动
    - PNS 抛物化纳维-斯托克斯方程
      - 不能计算沿流向存在分离区的粘性流动
  - 非定常热传导
  - 
#### 3.4.3 椭圆型方程
- 与特征线有关的解法不适用
- 没有有限的影响区和依赖区，信息可以向任何方向传播到任何地方
- P点可以影响区域内的每一个点，所以P点的解反过来也会受到整个封闭边界abcd的影响。这样，P点的解需要与流场中所有的点同时求解。
- 区域内的解依赖所有的边界，必须在整个边界上给定边界条件，这些边界条件可以有以下形式：
  - Dirichlet条件：在边界上指定未知函数u和v
  - Neumann条件：在边界上指定未知函数的导数，如$\partial u / \partial x$
  - Dirichlet条件和Neumann条件的混合条件
- 常见流动模型：
  - 定常亚声速无粘流动
  - 不可压无粘流动

3.5和3.6节未整理

---
# 2019/8/13
## 第二部分 基本数值方法
偏微分方程的离散化称为有限差分方法
积分形式方程的离散化称为有限体积法
### 第4章 离散化的基本方法
#### 4.1 引言

- 离散化：
  一个封闭形式的数学表达式，如函数，或函数的微分方程、积分方程，在某个区域里被看成连续的、有无穷多个值。离散化的实质就是用另外一个类似的表达式来近似它，但是这个近似表达式只在区域内有限多个离散点或控制体上规定了取值。
- 偏微分方程的解析解是封闭形式的表达式，它给出了未知函数在区域内的连续变化。
- 数值解只在区域内的离散点上给出了结果，这些离散点叫做网格点。
#### 4.2 有限差分基础
- 代数差分 = 有限差分
- 用代数差分代替偏导数
  - 用泰勒级数展开可以推导出导数的有限差分一般形式
  - $$u_{i+1, j}=u_{i, j}+\left(\frac{\partial u}{\partial x}\right)_{i, j} \Delta x+\left(\frac{\partial^{2} u}{\partial x^{2}}\right)_{i, j} \frac{(\Delta x)^{2}}{2}+\left(\frac{\partial^{3} u}{\partial x^{3}}\right)_{i, j} \frac{(\Delta x)^{3}}{6}+\cdots$$
  - 泰勒级数：
    - $x$的连续函数$f(x)$在$x$点有各阶导数，于是，函数$f$在$x + \Delta x$处的值可以由$x$点处的泰勒级数计算
    - $$f(x+\Delta x)=f(x)+\frac{\partial f}{\partial x} \Delta x+\frac{\partial^{2} f}{\partial x^{2}} \frac{(\Delta x)^{2}}{2}+\cdots+\frac{\partial^{n} f}{\partial x^{n}} \frac{(\Delta x)^{n}}{n !}+\cdots$$
    - 含义
    - $$f(x + \Delta x) = \underbrace{f(x)}_{\text{最初的估计\\(不太好)}} + \underbrace{\frac{\partial f}{\partial x}\Delta x}_{加上斜率的影响} + \underbrace{\frac{\partial ^2 f}{\partial x ^2}\frac{(\Delta x)^2}{2}}_{加上曲率的影响} + \cdots $$
- 构造有限差分的两种方法
  - 泰勒级数分析
  - 多项式近似

---

# 2019/8/14
#### 4.3 差分方程
- 差分方程与原微分方程并不相同, 它们完全是两个不同的东西
- 差分方程是一个代数方程
- 通常, 有限差分求解的含义是指用差分方程表示偏微分方程,然后求解差分方程,得到未知函数在每个离散网格点上的数值,而这些网格点都分布在所求解的物理区域内.
#### 4.4 显式方法与隐式方法
未整理
# 2019/8/15
0
# 2019/8/16
#### 误差与稳定性分析
1. 稳定性
   1. 数值误差是执行一组给定的计算时所产生的误差.
   2. 当计算从一个推进步进行到下一步时,如果某个特定的数值误差被放大了, 那么计算就变成不稳定.如果误差不增长,甚至在从一个推进步进行到下一步时,误差还在缩减,那么计算通常就是稳定的.
2. 误差
   1. 离散误差, 偏微分方程的精确解(解析解)与相应的差分方程(无舍入误差的解)之间的差.离散误差就是差分方程的截断误差再加上对边界条件进行数值处理时引进误差(从概念上讲,离散误差不能等同于截断误差)
   2. 舍入误差, 对数值进行多次重复计算产生的数值误差. 因为计算机通常要将数值舍入到某个有效数字.
   3. 关系
      1. A = 偏微分方程的精确解
      2. D = 差分方程的精确解
      3. N = 在某个具有有限精度的计算机上实际计算出来的解
      4. 离散误差 = A - D
      5. 舍入误差 = $\epsilon$ = N - D
      6. ![](https://i.imgur.com/L2V72BN.png)
3. 误差分析
   1. von Neumann(冯诺伊曼)稳定性方法,研究线性差分方程的稳定性性质 具体见122页


- CFL条件的物理解释: 要保证稳定性,数值解的依赖区域必须全部包含解析解的依赖区域
- 从稳定性考虑, 柯朗数必须小于等于1(C <= 1); 但从精度考虑, C尽可能接近1才更合适.
#### 4.6 小结

### 第5章 网格生成与坐标变换
#### 5.1 引言
- 网格: 分布在整个流场内的离散点
- 标准的有限差分法需要均匀网格
- 贴体坐标系$\xi$和$\eta$(在物体表面生成坐标线)
- ![物理平面与计算平面](https://i.imgur.com/V7loUPI.png)
- 流动控制方程在计算平面里用有限差分方法求解, 计算得到的信息将利用网格点之间的一一对应直接带回到物理平面. 因此需将物理平面的控制方程变换到计算平面表示的物理方程.
- 
- 