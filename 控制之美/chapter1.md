### 线性时不变系统
对于线性,时不变系统,我们可以认为输出是历史上无数个冲击响应度叠加.对于输入函数$u\left(t\right)$, 认为它是在$\tau$时刻,幅度为$u\left(\tau\right)d\tau$信号度叠加.假设系统对单位冲击激励的响应为$h\left(t\right)$, 那么$\tau$时刻对应的激励就是$h\left(t-\tau\right)u\left(\tau\right)d\tau$, 系统的输出就是所有历史时刻的叠加:
$$x\left(t\right)=\int_0^th\left(t-\tau\right)u\left(\tau\right)d\tau$$
因此,我们只要知道单位冲击响应$h\left(t\right)$,就能求出任何激励的响应.
求解单位冲击响应是困难的,下面先丢掉这个buff,从拉普拉斯变换角度求解线性常微分方程
### 拉普拉斯变换
#### 常微分->代数
拉普拉斯变换一个重要性质是
$$\mathcal{L}\left[\frac{df\left(t\right)}{dt}\right]=sF\left(s\right)-f\left(0\right)$$
这就把微分转化为代数了.
#### 逆变换
响应的拉普拉斯变化通常具有如下形式:
$$\frac{g\left(s\right)}{f\left(s\right)}$$
这里$f\left(s\right),g\left(s\right)$都是关于s的多项式.    
上述形式可以分解成如下形式:
$$\frac{a_1}{s+b_1}+\frac{a_2}{s+b_2}+....$$
而:
$$\mathcal{L}^{-1}\left[\frac{1}{s+a}\right]=e^{-at}$$

### 传递函数
#### 初始值为0
如果所有导数的初始条件为0,那么常微分组成的多项式在拉普拉斯变换后就变为$f\left(s\right)X\left(s\right)$的形式,这里$f\left(s\right)$是关于$s$的多项式.认为$\frac{1}{f\left(s\right)}$就是传递函数
#### 初始值不为0
对于一阶常微分方程,初始值可看作另一个冲击激励的输入.
