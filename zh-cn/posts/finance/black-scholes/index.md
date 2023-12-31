# Black-Scholes 推导


# 正态分布与对数正态分布
## 正态分布
### 概率密度函数
$$
f(x)=\frac{1}{\sqrt {2\pi \sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$
### 标准化
$$
t=\frac{x-\mu}{\sigma}\\
f(t)=\frac{1}{\sqrt {2\pi}}e^{-\frac{t^2}{2}dt}
$$
### 标准正态分布随机变量累计分布函数
$$
N(U)=\int_{t=-\infty}^U {\frac{1}{\sqrt{2\pi}}e^{-\frac{t^2}{2}dt}}
$$

## 对数正态分布
### 资产价格的对数变化
- 如果把资产价格变化 ($S_T-S_0$) 设定为正态分布的话，资产价格可能为负数
- 通常将资产价格的对数变化 ($lnS_T~-lnS_0$) 设定为正态分布
  $$
  lnS_T-lnS_0=x\backsim\phi(\mu, \sigma^2)
  $$
  因此
  $$
  S_T = S_0e^x
  $$
  称$S_T$服从对数正态分布（取对数后服从正态分布)

### 对数正态分布的期望
- 随机变量e^x^服从对数正态分布，其期望为：
  $$
  E(e^x)=\int_{-\infty}^{\infty}{e^xf(x)dx}= \int_{-\infty}^{\infty}{e^x\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}dx}
  $$

- 标准化，定义$t=\frac{x-u}{\sigma}$，则t是一个服从标准正态分布的随机变量
  $$
  x=\sigma t+\mu, dx=\sigma dt\\
  E(e^x)=\int_{-\infty}^{\infty}{e^x \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}dx}=e^{\mu+\frac{1}{2}\sigma^2}
  $$

# 连续时间布朗运动
## 随机游走
- 
  $$
    z_1-z_0=\epsilon_0\\
    \cdot\\
    \cdot\\
    z_{t+1}-z_t=\epsilon_t\\
    \cdot \\
    \cdot 
  $$

- 
 $$
 z_t-z_0=\sum\limits_{j=1}^{t} \epsilon_{t-j}\\
 z_{t+\Delta}-z_t \backsim\phi(0, \Delta),  \forall \Delta>0
 $$

- 由于$\epsilon_t$独立同分布
  $$
  E(z_t-z_0)=E(\sum\limits_{j=1}^{t} \varepsilon_{t-j})=\sum\limits_{j=1}^{t} E (\varepsilon_{t-j})=0\\
  var(z_t-z_0)=E (\sum\limits_{j=1}^{t} \varepsilon_{t-j})^2=\sum\limits_{j=1}^{t} E(\varepsilon_{t-j})^2=t \times 1=t
  $$

## 随机积分
- $$
  E(dz_t)=0\\
  var_t(dz_t)=E_t[dz_t-E_t(dz_t)]^2=E_t(dz_t)^2=dt\\
  dz_t\backsim \sqrt{dt}
  $$
  $dz_t$的量级与$\sqrt{dt}$的量级一样

- 广义布朗运动
  $$
  dx_t=\mu dt+\sigma dz_t
  $$
  $dx_t$是每时刻粒子的位置变化，$udt$是每时刻粒子运动的趋势项，$\sigma$ 是粒子位置变化的标准差
  $$
  E_t(dx_t)=E_t(\mu dt+\sigma dz_t)=\mu dt\\
  \begin{aligned}
   var_t(dx_t)&=E_t[dx_t-E_t(dx_t)]^2\\
   &=E_t(\mu dt+\sigma dz_t-\mu dt)^2\\
   &=\sigma^2E_t(dz_t)^2\\
   &=\sigma^2dt  
  \end{aligned}
  $$

- 伊藤引理
  反应如果标的资产价格做布朗运动，衍生品的价格是如何运动的
  |        | $dz_t$ | $dt$ |
  | :----: | :----: | :--: |
  | $dz_t$ |  $dt$  |  0   |
  |  $dt$  |   0    |  0   |
  
  如果 $x_t$ 服从 $dx_t=\mu dt+\sigma dz_t$ 的过程，那么$y_t=f(x_t)$会服从什么过程。
  $$
  \begin{aligned}
   dy_t&=\frac{\partial f}{\partial x}dx_t+\frac{1}{2}\frac{\partial^2f}{\partial x^2}dx^2\\
   &=\frac{\partial f}{\partial x}(\mu dt+\sigma dz_t)+\frac{1}{2} \frac{\partial^2 f}{\partial x^2}(\mu dt+ \sigma dz_t)^2\\
   &=(\frac{\partial f}{\partial x} \mu+\frac{1}{2} \frac{\partial^2f}{\partial x^2} \sigma^2)dt+ \frac{\partial f}{\partial x} \sigma dz_t
  \end{aligned}
  $$
  $y_t$作为$x_t$的函数，也在做布朗运动，只不过在$y_t$的漂移项中，还包含了$x_t$的扩散项

- 随机积分
  $$
  \int_{t=0}^{T}{dz_t}=\lim\limits_{n \to 0} [(z_{\Delta}-z_0)+(z_{2\Delta}-z_{\Delta})+\cdots+(z_T-z_{T-\Delta})]=z_T-z_0 \backsim \phi(0, T)\\
  \int_{t=0}^T=dx_t=\mu \int_{t=0}^T dt+ \sigma \int_{t=0}^T dz_t\\
  x_T-x_0=\mu T+\sigma \int_{t=0}^T dz_t\\
  E_0(x_T-x_0)=\mu T\\
  var(x_T-x_0)=\sigma^2 T
  $$

- 几何布朗运动
  $$
  dS_t=\mu S_t dt+ \sigma S_t dz_t\\
  $$
  也即：
  $$
  \frac{dS_t}{S_t}=\mu dt+\sigma dz_t
  $$

## BS公式的偏微分方程推导
- 假设市场中存在股票和无风险债券两种资产，其价格分别为$S_t$与$B_t$。两种资产价格的运动方程为
  $$
  dS_t=\mu S_tdt+\sigma S_tdz_t\\
  dB_t=rBdt
  $$
  构建无风险组合：
  $$
  V(t, S_t)=-f(t,S_t)+ \frac{\partial f}{\partial S}S_t
  $$
  包含1单位衍生品的空头，以及$\frac{\partial f}{\partial S}S_t$股的股票多头。

- 由伊藤引理可以求出组合价值的微分为
  $$
  \begin{aligned}
  dV(t,S_t)&=-df(t,S_t)+\frac{\partial f}{\partial S}dS_t\\
  &=-(\frac{\partial f}{\partial t}dt+\frac{\partial f}{\partial S}dS_t+\frac{1}{2}\frac{\partial^2 f}{\partial S^2}dS^2_t)+\frac{\partial f}{\partial S}dS_t\\
  &=-\frac{\partial f}{\partial t}dt-\frac{1}{2} \frac{\partial^2 f}{\partial S^2}(\mu S_t dt+\sigma S_t dz_t)^2\\
  &=-\frac{\partial f}{\partial t}dt-\frac{1}{2}\frac{\partial^2 f}{\partial S^2}\sigma^2 S^2_t(dz_t)^2\\
  &=-(\frac{\partial f}{\partial t}+\frac{1}{2}\frac{\partial^2 f}{\partial S^2} \sigma^2 S^2_t)dt
  \end{aligned}
  $$
 
  由于组合无风险，所以组合的价值理应按照无风险利率r增长，即：
  $$
  dV(t,S_t)=rV(t,S_t)dt
  $$
  于是有，
  $$
  -(\frac{\partial f}{\partial t}+\frac{1}{2} \frac{\partial^2 f}{\partial S^2} \sigma^2S^2_t)dt=rV(t,S_t)dt
  $$
  将$V(t,S_t)$带入，有
  $$
  -(\frac{\partial f}{\partial t}+\frac{1}{2} \frac{\partial^2 f}{\partial S^2} \sigma^2S^2_t)dt=r[-f(t,S_t)+ \frac{\partial f}{\partial S}S_t]dt
  $$
  上式两边$d_t$前的系数一定要相等，所以有，
  $$
  \frac{\partial f}{\partial t}+rS_t \frac{\partial f}{\partial S}+\frac{1}{2}\sigma^2S^2_t \frac{\partial^2 f}{\partial S^2}=rf
  $$
  结合边界条件可以解出，比如欧式买入期权的边界条件是$f(T, S_T)=max(S_T-K,0)$

## 鞅方法推导
- 利用随机积分直接把价格的公式接出来。
- 对于无风险债券家的对数$ln(B_t)$的微分：
  $$
  d(\ln B_t)=\frac{1}{B_t}dB_t=\frac{1}{B_t}B_t dt=rdt
  $$
  上式左右两边同时求积分可得
  $$
  \int_{t=0}^T {d(\ln B_t)}=\int_{t=0}^T {rdt}
  $$
  这便是无风险债券在T时刻价格的公式
  接下来再利用伊藤定理来求解出股票价格的公式
  $$
  \begin{aligned}
  d(\ln S_t)&=\frac{1}{S_t}dS_t -\frac{1}{2}\frac{1}{S^2_t} \\
  &=\mu dt+\sigma dz_t-\frac{1}{2S^2_t}(\mu S_t dt+\sigma S_tdz_t)^2\\
  &=\mu dt+\sigma dz_t-\frac{1}{2}\sigma^2 dt\\
  &=(\mu-\frac{1}{2}\sigma^2)dt+\sigma dz_t
  \end{aligned}
  $$
  对上式左右两边同时求积分可得
  $$
  \int_{t=0}^T{d(\ln S_t)}=\int_{t=0}^T{(\mu -\frac{1}{2}\sigma^2)dt}+\sigma \int_{t=0}^T {dz_t}\\
  \ln S_T - \ln S_0 = (\mu- \frac{1}{2} \sigma^2)T + \sigma \int_{t=0}^T {dz_t}\\
  S_T = S_0e^{(\mu- \frac{1}{2} \sigma^2)T + \sigma \int_{t=0}^T {dz_t}}
  $$
  其中$(\mu- \frac{1}{2} \sigma^2)T + \sigma \int_{t=0}^T {dz_t}$是一个正态分布的随机变量，均值为$(\mu- \frac{1}{2} \sigma^2)T$，方差为$\sigma^2T$，根据对数正态分布的性质有，
  $$
  E(S_T)= S_0 e^{\mu T}
  $$
  这里的股票价格并不符合鞅性，即$E(S_T) \neq S_0 e^{rT}$。这是在真实世界的概率测度下求取的期望，自然不存在鞅性的结论。不过我们知道，当市场中不存在套利机会时，一定存在一个等价鞅测度，股票价格在这个测度下符合鞅性。也就是说，$\widetilde{E}(S_T)=S_0e^{rT}$，在等价鞅测度下，股票价格应该满足：

  $$
  S_T = S_0e^{(\mu- \frac{1}{2} \sigma^2)T + \sigma \int_{t=0}^T {d\widetilde{z}_t}}
  $$

  T时刻，行权价为K的欧式买入期权在0时刻的价格在等价鞅测度下，有
  $$
  C_0=e^{-rT} \widetilde{E} \lbrace max \lbrace S_T-K, 0 \rbrace \rbrace
  $$
  $\ln S_T$是一个正态分布的随机变量
  $$
  \ln S_T \backsim [\ln S_0 +(r-\frac{1}{2}\sigma^2)T, \sigma^2 T ]
  $$
  将$lnS_T$ 写成
  $$
  \ln S_T = a+ b\mu
  $$
  其中$\mu \backsim \phi (0,1)$，而a, b两个参数分别为
  $$
  a= \ln S_0 +(r-\frac{1}{2}\sigma^2)T\\
  b= \sigma \sqrt{T}
  $$
  令
  $$
  e^{a+bU}=K
  $$
  可以解出
  $$
  U=\frac{\ln K -a}{b}=\frac{\ln K-\ln S_0 +(r-\frac{1}{2}\sigma^2)T}{\sigma \sqrt{T}}
  $$
  计算期望
  $$
  \begin{aligned}
  \widetilde{E} \lbrace max \lbrace S_T-K, 0 \rbrace \rbrace &= \int_{U}^{+\infty} {(e^{a+b\mu}-K)\frac{1}{\sqrt {2\pi}}e^{-\frac{1}{2}\mu^2}du }\\
  &=\frac{1}{\sqrt {2\pi}}\exp [-\frac{1}{2}(u-b)^2+a+\frac{1}{2}b^2]du-K \int_{U}^{+\infty} {\frac{1}{\sqrt {2\pi}}e^{-\frac{\mu^2}{2}}du}\\
  &=e^{a+\frac{1}{2}b^2} \int_{U-b}^{+\infty}{\frac{1}{\sqrt{2\pi}}\exp[-\frac{1}{2} (u-b)^2]}d(u-b)-KN[-U]\\
  &=e^{a+\frac{1}{2}b^2}[1-N(U-b)]-KN[1-N(U)]\\
  &=e^{rT}S_0N(b-U)-KN(-U)
  \end{aligned}
  $$
  其中$a+\frac{1}{2}b^2=\ln S_0+rT$
  就有
  $$
  C_0 = e^{-rT} \widetilde{E} \lbrace max \lbrace S_T-K,0 \rbrace \rbrace =S_0 N(b-U)-e^{-rT}KN(-U)
  $$
  如果定义
  $$
  d_1 = b-U=\sigma \sqrt{T}- \frac{\ln K -a}{b}=\frac{\ln K-\ln S_0 +(r-\frac{1}{2}\sigma^2)T}{\sigma \sqrt{T}} = \frac{\ln \frac{S_0}{K}+（r+\frac{1}{2}\sigma^2)T}{\sigma \sqrt {T}}\\
  d_2 = -U = d_1-b = d_1-\sigma \sqrt {T}
  $$
  则有
  $$
  C_0 = S_0N(d_1)-e^{-rT}KN(d_2)
  $$
