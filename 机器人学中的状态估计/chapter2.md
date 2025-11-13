##  贝塞尔修正
均值:    
$$\bar X=\frac{1}{N}\sum_{i=1}^Nx_i$$    
方差: 
$$\sum=\frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)(x_i-\mu)^T=\frac{1}{N-1}\sum_{i=1}^{N}(x_i-\bar{X})(x_i-\bar{X})^T$$
系数为$N-1$被称作贝塞尔修正,它表明实际方差比用估算的均值当作真实均值估算出来的方差要大一点.直观的理解是, 对于函数$f(c)=\sum_{i=1}^{N}(x_i-c)(x_i-c)^T$, 当$c=\bar{X}$时,$f(c)$取得最小值.实际上由于样本有限,$\bar{X}$不一定等于$\mu$, 因此估算出的方差可能偏小,需要乘上$\frac{N}{N-1}$这个修正因子.  
下面来详细推导为什么是$N-1$:  
$$S^2=\frac{1}{N}\sum_{i=1}^N(x_i-\bar{X})(x_i-\bar{X})^T=\frac{1}{N}\sum_{i=1}^N((x_i-\mu)+(\mu-\bar{X}))((x_i-\mu)+(\mu-\bar{X}))^T$$
按照右侧的等式展开化简,容易得到:
$$E[S^2]=\sum+\mu \mu^T-E[\bar{X}\bar{X}^T]$$
我们来计算$E[\bar{X}\bar{X}^T]$:    
展开,有:
$$E[\bar{X}\bar{X}^T]=\frac{1}{N^2}E[(\sum_ix_i)(\sum_ix_i^T)]=\frac{1}{N^2}(\sum_iE[x_ix_i^T]+E[\sum_{i\ne j}x_ix_j^T])$$
如果每次采样相互独立,那么$E[x_ix_j^T]=\mu\mu^T$   
将等式$\sum=\frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)(x_i-\mu)^T$右侧展开,化简,有$\sum=E[XX^T]-\mu\mu^T$
因此$E[XX^T]=\sum+\mu\mu^T$
代入,化简就可以证明$E[S^2]=\frac{N-1}{N}\sum$  

 ## 信息熵
 ### 离散情况
 参考: 李贤平 <<概率论基础>>
 我们衡量一个事件$\alpha$的不确定度,用$H(\alpha)$表示,它需要满足如下三个条件:  
 - $H(\alpha)$关于$\alpha$的概率分布是连续函数
 - 对于等概率事件,$H(\alpha)$随着可能发生的事件增多而增多.
 - 分多次试验,总的不确定度不变,即: $H(p_1,p_2,p_3)=H(p_1,p_2+p_3)+(p_2+p3)H(\frac{p_2}{p_2+p_3},\frac{p3}{p_2+p_3})$
满足上述三个条件的函数,只可能具有如下形式:
$$H(\alpha)=-C\sum_ip_iIn(p_i)$$
我们用$H(\alpha)=-\sum_ip_iIn(p_i)$表示离散概率的不确定度,称为熵.

### 推广到连续情形
假设概率密度函数为$p(x)$, 概率区间长度为l,我们通过如下不严谨的方式将熵推广到连续场景:
我们将区间均分成n个相等的小区间,每个小区间内,概率时恒定的,此时可用离散情况度量其不确定度:
$$H(x)=-\lim_{n \to \infty}\sum_ip(x_i)\frac{l}{n}In(p(x_i)\frac{l}{n})=-\lim_{n \to \infty}\sum_ip(x_i)In(p(x_i))\frac{l}{n}-\lim_{n \to \infty}p(x_i)\frac{l}{n}In(\frac{l}{n})$$
第一个极限,实际上就是积分的定义,第二个极限,由于概率和1,所以极限是0.   
综上:
$$H(x)=-\int p(x)In(p(x))dx$$

### 条件熵,信息量(互信息)
对于两个事件$\alpha, \beta$, 用$H_{\alpha}(\beta)$表示事件$\alpha$已经发生时,事件$\beta$的条件熵,具体定义为:
$$H_{\alpha}(\beta)=\sum_k P(A_k)H_{A_k}(\beta)$$
这也不难推广到连续场景:    
$$H_{\alpha}(\beta)=\int p_{\alpha}(x)H_{A_k}(\beta)dx$$
直观上讲,我们观测到已经发生的事件,会导致事件B的不确定度不变或减少,我们略去证明,直接写出结论:    
$$H_{\alpha}(\beta) \le H(\alpha \beta)=H(\alpha)+H_{\alpha}(\beta) \le H(\alpha)+H(\beta)$$
这也侧面说明熵是非负的,特别的,当某个事件必定发生时(概率为1),熵为0.

我们用:
$$I(\alpha,\beta)=H(\beta)-H_{\alpha}(\beta)$$
来表示事件$\alpha$含有事件$\beta$多少信息.称之为$\alpha$试验中有关$\beta$的信息量.信息量又可以表示为:    
$$I(\alpha,\beta)=H(\beta)-H_{\alpha}(\beta)=H(\beta)-(H(\alpha\beta)-H(\alpha))=H(\alpha)+H(\beta)-H(\alpha\beta)=I(\beta, \alpha)$$
因此信息量又称作是互信息.

我们来推导互信息的表达式:    
注意到$P(A_i)=\sum_jP(A_iB_j)$,所以
$$H(\alpha)=-\sum_iP(A_i)In(P(A_i))=-\sum_i((\sum_jP(A_iB))In(P(A_i)))=-\sum_{i,j}P(A_iB_j)In(P(A_i))$$
同理:    
$$H(\beta)=-\sum_{ij}P(A_iB_j)In(P(B_j))$$
代入到如下表达式,化简,就有:
$$I(\alpha, \beta)=H(\alpha)+H(\beta)-H(\alpha\beta)=\sum_{i,j}P(A_iB_j)In(\frac{P(A_iB_j)}{P(A_i)P(B_j)})$$

我们可以将该公式推广到连续场景:
$$I(\alpha, \beta)=\int_x\int_yp_{\alpha\beta}(x,y)In(\frac{p_{\alpha\beta(x,y)}}{p_{\alpha}(x)p_{\beta}(y)})$$
