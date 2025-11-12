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