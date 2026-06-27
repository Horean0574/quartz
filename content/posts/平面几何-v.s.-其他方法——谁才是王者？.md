---
title: 平面几何 v.s. 其他方法——谁才是王者？
tags:
  - 数学
  - 几何
  - 平面几何
  - 相似三角形
  - 圆
  - 倍长中线
  - 最值问题
  - 三角几何
  - 动静互换
  - 平面向量
  - 反演变换
  - 阿氏圆
  - 隐圆
  - 中位线
category: 数学
published: 2026-05-05 00:17:42+08
description: 本文作者分享了在高中科技节数学“说数学比赛”活动中遇到的五道有趣的平面几何题，围绕各题的官方解法（多为三角法或解析几何、向量法）与自己设计的纯平面几何解法展开详细讲解。文章通过具体题目实例，展示了动静互换、探照灯模型、反演变换、倍长中线及阿氏圆等多种平面几何思维技巧的应用。作者强调纯几何解法虽计算量小但思维含量丰富，鼓励读者通过多种视角切换提升解题能力。文章最后总结了平面几何的灵活多变和思维训练价值，并鼓励求知者换角度思考问题。
image: https://img.hxrch.top/20260505002629513.webp
updated: 2026-05-05 00:17:54+08
---

> 好久没有写过文章啦！趁着这个五一小长假赶紧来弥补一下。。

# 序言

前段时间我校科技节活动上我们高一年级举办了一场**说数学比赛活动**（本质上是讲题比赛），要求每班派一名讲题代表和一位同学作为智囊到现场抽取题目然后在十五分钟后按抽签顺序上台讲题，试题考察内容覆盖目前为止的全部高中所学，然后由几位评委老师给出分数，比赛结束后几天内老师们会综合各代表上台说数学的表现评定奖项（分为特等奖、一等奖、二等奖和三等奖）。

这里就不卖关子了，虽然我没有代表班级上台说数学，但是我作为我们班的智囊为上台代表提供辅助。当然，我们班最后拿到了唯二的**特等奖**之一！！！（我的功劳也少不了😊。

好了，进入正题：本次说数学活动总共十四题中我发现了**五道**颇有意思的**平面几何**题目，如此热爱平面几何的我就不得不抓住这次机会在比赛结束后要了份题目清单回去仔细琢磨这几道平面几何题，虽然说官方答案都**不是**纯平面几何的解法……（要么三角函数，要么建系或平面向量）但正因如此，这更加激发了我用纯平面几何法解出这几道题的兴趣。那么接下来请看题：

:::danger[注意]
*前方高能预警！*（可能涉及多种平面几何技巧及模型，但请**一定要看到最后**！！！尤其是第五题！）
:::

# 有趣的题目们

## 第一题

### 题面

如图，点$P$为$\angle BAC$内一点，$|PA|=1$，$\angle BAP=30\degree$，$\angle CAP=45\degree$，过点$P$作直线分别交射线$AB,AC$于$D,E$两点，则$\frac{1}{|PD|}+\frac{1}{|PE|}$的最大值为__________.

![第一题-题面](https://img.hxrch.top/20260502181157947.svg)

### 官方解法：三角法

> **官方思路：** 用正弦定理表示$|PD|,|PE|$，再结合辅助角公式求函数最大值。

设$\angle ADP=\alpha,\angle AEP=\beta$，则有
$$
\alpha +\beta =105\degree
$$
在$\triangle ADP$中，由正弦定理得
$$
\frac{1}{\sin\alpha}=\frac{|PD|}{\sin 30\degree}\Rightarrow\frac{1}{|PD|}=2\sin\alpha
$$
同理，在$\triangle AEP$中，有
$$
\frac{1}{|PE|}=\sqrt{2}\sin\beta
$$
所以
$$
\begin{align}
\frac{1}{|PD|}+\frac{1}{|PE|}&=2\sin\alpha+\sqrt2\sin\beta\\
&=2\sin(105\degree-\beta)+\sqrt2\sin\beta\\
&=(\sqrt3+1)\sin(\beta+45\degree)\\
&\leq\sqrt3+1
\end{align}
$$
当且仅当$\beta=45\degree$时取等，即最终答案为$\sqrt3+1$。

> 由上述步骤，我们不难看到三角法解决这道题的核心就是分别在两个小三角形中利用正弦定理将边化角，再通过角的条件结合辅助角公式便可轻松解出最终结果。这种解法固然简单，也容易想到，不过我还是要介绍我的平面几何解法！

### Mine-平面几何法

如下图，为了求$\frac{1}{|PD|}+\frac{1}{|PE|}$的最大值，我们不得不将其从比值的形式转化为实际存在的线段的形式，正好题目中又给出了一条定长线段$AP$，所以我们便可以借着这个便利来构造相似三角形，以便后续解题。

![第一题-平面几何法](https://img.hxrch.top/20260502181127445.svg)

因此，我们可以在射线$PD$上取一点$M$，使得$\angle AMP=\angle BAP=30\degree$，同理在射线$PE$上取一点$N$，使得$\angle ANP=\angle CAP=45\degree$，连接$AM,AN$。

那么我们不难得到此图中有两对相似三角形：
$$
\triangle AMP\sim\triangle DAP,\qquad\triangle ANP\sim\triangle EAP
$$
于是我们可以得到线段间的比例关系，有
$$
\frac{AP}{PD}=\frac{PM}{AP},\hspace{2em}\frac{AP}{PE}=\frac{PN}{AP}
$$
由此再结合定长线段$AP$，原式就可以进行如下转化：
$$
\begin{align}
\frac{1}{|PD|}+\frac{1}{|PE|}&=\frac{AP}{PD}+\frac{AP}{PE}\\
&=\frac{PM}{AP}+\frac{PN}{AP}\\
&=\frac{MN}{AP}
\end{align}
$$
这时候我们就成功地把原来的复杂表达式转化为了两条线段间的比值——你可能心生疑惑了，$AP$不是长度为$1$的定长线段吗，为什么不继续把这个式子化简称$MN$呢？

诶，这就到了本解法最关键的一步了！因为其实我们会发现，如果将原式继续化简为单动线段$MN$的话，在$\triangle AMN$中其实我们是不太清楚点$M,N$是如何同时运动的，也就是说线段$MN$的两个端点都是动点，我们依旧不太好把握它何时取最值。而同时我们又可以注意到在该式化简之前的形式$\frac{MN}{AP}$中还有另一条线段$AP$，那么我们就可以考虑从这条线段下手，不再讨论线段$MN$了。

——那，如何做到呢？没错，根据**相对运动思想**，这时候<strong style="color:red;">动静互换</strong>就要出场了！

由线段$MN$和线段$AP$一动一静，动静互换后变成线段$MN$为静线段，线段$AP$为动线段，那么此时又因为$\triangle AMN$的形状已经确定（已知两定角），所以点$A$是定点！！如此一来，问题就迎刃而解了：要求$\frac{MN}{AP}$的最大值，只需关注其会变化的分母的最小值，如何呢？当然是**直线外一点与直线上各点连接的所有线段中，垂线段最短**啊。

所以，我们可以知道当且仅当$MN\perp AP$时其长度比例$\frac{MN}{AP}$取得最大值，且动静换回来也是一样的。接下来我们就只需讨论该比例取得最大值时各点线的情况了，那么在取最大值时，我们就有新的已知条件$MN\perp AP$了。

因而在$\mathrm{Rt}\triangle APM$中，由$\angle AMP=30\degree$和$AP=1$，不难得到
$$
PM=\sqrt3
$$
同理，在$\mathrm{Rt}\triangle APN$中，由$\angle ANP=45\degree$和$AP=1$，可以得到
$$
PN=1
$$
然后此时的线段$MN$的长度就已知了：
$$
MN=PM+PN=\sqrt3+1
$$
最终便可得到答案：
$$
\frac{1}{|PD|}+\frac{1}{|PE|}=\frac{MN}{AP}\leq\sqrt3+1
$$

> 小结一下，在这道题中，几何做法相较于传统三角法的计算量小了非常多，在我看来是一种非常不错的解法，只需简单构造两个相似三角形即可解出。

## 第二题

### 题面

（无图）在$\triangle ABC$中，$AB=AC=2$，$\angle BAC=90\degree$，$D,E$为边$BC$上两点，且$\angle DAE=45\degree$，则$\overrightarrow{AD}\cdot\overrightarrow{AE}$的最小值为__________.

### 官方解法：解析几何

> **官方思路：** 首先建立平面直角坐标系，然后结合向量的坐标运算法则及基本不等式求解数量积最小值即可。

![第二题-解析几何](https://img.hxrch.top/20260503073336382.svg)

如图所示，以$BC$的中点$O$为原点，$BC$为$x$轴，射线$OA$为非负$y$轴建立平面直角坐标系，则有
$$
B(-\sqrt2,0),\qquad C(\sqrt2,0),\qquad A(0,\sqrt2)
$$
接下来不妨设点$D$在点$E$的左侧，并设$D(x,0),\ E(y,0)$，则由$\angle DAE=45\degree$，可知$-\sqrt2\leq x\leq0,\ 0\leq y\leq\sqrt2$，据此有
$$
\overrightarrow{AD}=(x,-\sqrt2),\qquad\overrightarrow{AE}=(y,-\sqrt2)
$$
则
$$
\overrightarrow{AD}\cdot\overrightarrow{AE}=xy+2
$$
又因为$\tan\angle DAE=\tan(\angle DAO+\angle EAO)=\tan45\degree=1$，所以
$$
\frac{\tan\angle DAO+\tan\angle EAO}{1-\tan\angle DAO\cdot\tan\angle EAO}=\frac{\frac{-x}{\sqrt2}+\frac{y}{\sqrt2}}{1-\frac{-x}{\sqrt2}\cdot\frac{y}{\sqrt2}}=1
$$
因此有
$$
xy+2=\sqrt2(y-x)\Rightarrow x=\frac{\sqrt2y-2}{\sqrt2+y}
$$
将此式代回原式，得
$$
\overrightarrow{AD}\cdot\overrightarrow{AE}=xy+2=\frac{\sqrt2y^2-2y}{\sqrt2+y}+2=\frac{\sqrt2y^2+2\sqrt2}{\sqrt2+y}
$$
再进行换元，令$t=\sqrt2+y\in[\sqrt2,2\sqrt2]$，则
$$
\begin{align}
\overrightarrow{AD}\cdot\overrightarrow{AE}&=\frac{\sqrt2{(t-\sqrt2)}^2+2\sqrt2}{t}\\
&=\sqrt2t+\frac{4\sqrt2}{t}-4\\
&\geq2\sqrt{\sqrt2t\cdot\frac{4\sqrt2}{t}}-4\\
&=4\sqrt2-4
\end{align}
$$
当且仅当$\sqrt2t=\frac{4\sqrt2}{t}$即$t=2,y=2-\sqrt2$时取等，故$\overrightarrow{AD}\cdot\overrightarrow{AE}$的最小值为$4\sqrt2-4$。

> 这是这道题的较为常规的解法，利用向量的坐标表示转化数量积问题，并在坐标系中直接地利用角度条件，思路直观清晰，虽稍有计算量，但这不影响此方法的实用性。

### Mine-平面几何法

如下图，虽然这个图形看着很复杂，但其实思路非常简明清晰：既然题目要求$\overrightarrow{AD}\cdot\overrightarrow{AE}$的最小值，那我们就先按照数量积的定义将其展开，即$\overrightarrow{AD}\cdot\overrightarrow{AE}=AD\cdot AE\cdot\cos\angle DAE$，由此我们也不难联想到三角形的面积公式$S_{\triangle DAE}=\frac{1}{2}AD\cdot AE\sin\angle DAE$，这时就非常巧了，我们将上述两式作比，便可以得到$\overrightarrow{AD}\cdot\overrightarrow{AE}=\frac{2S_{\triangle DAE}}{\tan\angle DAE}=\frac{2S_{\triangle DAE}}{\tan45\degree}=2S_{\triangle DAE}$，那么这时候这道题就显得非常简单了——因为后面就是<strong style="color:red;">探照灯模型</strong>的内容了！就此我们便可以很容易证出当且仅当$DA=DE$时$\triangle DAE$的面积有最小值，也即此时$\overrightarrow{AD}\cdot\overrightarrow{AE}$有最小值。

![第二题-平面几何法](https://img.hxrch.top/20260503083929334.svg)

由于我们预想的结果是$AD=AE$时$S_{\triangle DAE}$最小，那么**先猜后证**，将此特殊情况与其他一般情况做对比即可。因此，先在$BC$上取点$D',E'$，使得$AD'=AE'$且$\angle D'AE'=45\degree$（构造特殊情况），接下来如上图所示，我们可以先与点$D$在点$D'$右侧的一般情况做对比：

要比较图中$\triangle D'AE'$和$\triangle DAE$的面积大小，而我们又发现这两个三角形有重叠部分$\triangle DAE'$，所以我们可以先把这部分刨去，只关注它们各自独立的部分，意即我们只需要比较$\triangle DAD'$和$EAE'$的面积大小就行了，不难发现
$$
\begin{align}
\angle D'AE'&=\angle DAE=45\degree\\
&\Downarrow\\
\angle D'AE'-\angle DAE'&=\angle DAE-\angle DAE'\\
&\Downarrow\\
\angle DAD'&=\angle EAE'
\end{align}
$$
又因为
$$
AD'=AE'
$$
那么根据三角形面积公式的三角形式（两边夹一角），我们只需比较边$AD$与$AE$的长度即可——但显然，为了严谨说明，我们不能直接从图中直接比较两条线段的长度。那我们可以考虑转变一下思维方向，能不能通过比较角的大小来间接比较边的长度呢？

当然是可以的！我们需要知道，在同一个三角形中还有一个基本公理，就是**大边对大角**，反过来**大角对大边**亦成立。那么在$\triangle DAE$中，为了比较边$AD$和$AE$的大小，我们将其转化为比较$\angle AED$和$\angle ADE$的大小，有
$$
\left\{\begin{align}
&\angle AED=\angle AE'D'-\angle EAE',\\
&\angle ADE=\angle AD'E'+\angle DAD'
\end{align}\right.
$$
再结合其一旁的等腰$\triangle AD'E'$的性质，可得
$$
\angle AE'D'=\angle AD'E'
$$
由作差法，得
$$
\begin{align}
\angle ADE-\angle AED&=(\angle AD'E'+\angle DAD')-(\angle AE'D'-\angle EAE')\\
&=\angle DAD'+\angle EAE'\\
&>0
\end{align}
$$
所以
$$
\angle AED<\angle ADE
$$
那么根据大边对大角，就可以知道
$$
AD<AE
$$
因而，当点$D$在点$D'$右侧时，有
$$
S_{\triangle D'AE'}<S_{\triangle DAE}
$$
接着同理可证当点$D$在点$D'$左侧时该式依然成立，所以对于任意符合题目条件的点$D,E$，都满足
$$
\overrightarrow{AD}\cdot\overrightarrow{AE}=2S_{\triangle DAE}\geq 2S_{\triangle D'AE'}
$$
到这一步，本题就非常轻松了，现在的唯一目的是求出$\triangle D'AE'$的面积。如果是用几何解法的话，因为是在一个等腰直角三角形中，并且其直角顶角夹了一个$45\degree$角，那就可以考虑**半角模型**，在上图中即将$\triangle ACE'$顺时针旋转$90\degree$，得到$\triangle ABG$，除了可以容易证明$\angle GBD'=90\degree$之外，这时还有
$$
\left.\begin{align}
AG&=AE',\\
\angle GAD'&=\angle E'AD',\\
AD'&=AD'
\end{align}\right\}
\Rightarrow\triangle AGD'\cong\triangle AE'D'
$$
所以，由$GD'=D'E',BG=CE'$和$BD'=CE'$，我们就把线段$BD',CE'$和$D'E'$都放到了同一个等腰$\mathrm{Rt}\triangle GBD'$中，因此不妨设
$$
BD'=CE'=BG=x
$$
则
$$
GD'=D'E'=BC-BD'-CE'=2\sqrt2-2x
$$
由等腰直角三角形的性质，有
$$
GD'=\sqrt2BG\Rightarrow2\sqrt2-2x=\sqrt2x
$$
于是可以解得
$$
x=2\sqrt2-2,\qquad D'E'=4-2\sqrt2
$$
此时我们将$\triangle D'AE'$中$D'E'$所对的高$AH$作出来，不难得到$AH=\sqrt2$，于是
$$
S_{\triangle D'AE'}=\frac{1}{2}D'E'\cdot AH=\frac{1}{2}\times(4-2\sqrt2)\times\sqrt2=2\sqrt2-2
$$
最后我们便可得到
$$
\overrightarrow{AD}\cdot\overrightarrow{AE}\geq2S_{\triangle D'AE'}=4\sqrt2-4
$$

> 到此这道题的两种解法就介绍完啦，别看几何法好像过程很多，但是作为一道选填的话，只要我们思路足够清晰，真正的计算量是非常少的，可以很快速地得到答案！！以上的叙述只是确保说明的严谨性与完整度。

## 第三题

### 题面

（无图）已知$\triangle ABC$中，点$D$在边$BC$上，$\angle ADB=120\degree$，$AD=2$，$CD=2BD$。当$\frac{AC}{AB}$取得最小值时，$BD$的长度为__________.

### 官方解法：三角法

> **官方思路：** 用余弦定理表示$AB,AC$，并结合基本不等式求出其取等情况。

![第三题-三角法](https://img.hxrch.top/20260503201101752.svg)

如上图，设$CD=2BD=2m>0$，则在$\triangle ABD$中，有
$$
AB^2=BD^2+AD^2-2BD\cdot AD\cdot\cos\angle ADB=m^2+4+2m
$$
在$\triangle ACD$中，有
$$
AC^2=CD^2+AD^2-2CD\cdot AD\cdot\cos\angle ADC=4m^2+4-4m
$$
所以
$$
\begin{align}
{\Big(\frac{AC}{AB}\Big)}^2&=\frac{4m^2+4-4m}{m^2+4+2m}\\
&=\frac{4(m^2+4+2m)-12(m+1)}{m^2+4+2m}\\
&=4-\frac{12}{(m+1)+\frac{3}{m+1}}\\
&\geq4-\frac{12}{2\sqrt{(m+1)\cdot\frac{3}{m+1}}}\\
&=4-2\sqrt3
\end{align}
$$
当且仅当$m+1=\frac{3}{m+1}$即$m=\sqrt3-1$时取等，所以当$\frac{AC}{AB}$取得最小值时$m=\sqrt3-1$，即
$$
BD=\sqrt3-1
$$

> 由上述步骤，我们不难发现这道题的常规三角函数解法计算量并不算大，并且较为便捷、直接。那接下来再对比一下几何解法（做好心理准备。

### Mine-平面几何法

如下图，由题可知线段$AD$长度确定，但其在$\triangle ABC$内部，不太方便处理，所以可以考虑将其转化为另一个三角形的底边以获得更充分的利用，即通过相似三角形进行转化。最后问题可以变为**共动点顶点**的两条线段的比值最值问题，那么就可以使用<strong style="color:red;">反演变换</strong>构造新的相似三角形对其进行进一步转化，从而继续将两条动线段转化为一条动线段并解决问题。（本质即**双动线段比例最值问题**，可参考这篇[往期文章](https://blog.hxrch.top/posts/%E5%8F%8C%E5%8A%A8%E7%BA%BF%E6%AE%B5%E6%AF%94%E4%BE%8B%E6%9C%80%E5%80%BC%E9%97%AE%E9%A2%98%E5%8F%8D%E6%BC%94%E5%8F%98%E6%8D%A22/)。）

![第三题-平面几何法-1](https://img.hxrch.top/20260503211501171.svg)

如前文所述，第一步我们应该转化定长线段$AD$这一条件，定长转化到一个三角形的底边上。因此我们可以考虑过点$B$作$AC$的平行线交$AD$的延长线于点$G$，思路类似倍长中线，只不过把全等三角形换位相似三角形了——由$CD=2BD$可以得到
$$
\triangle ADC\sim\triangle GDB\Rightarrow
\left\{\begin{align}
&AG=\frac{3}{2}AD=3,\\
&AC=2BG
\end{align}\right.
$$
此时我们不仅将定长线段转化到了底边上，同时还转化了所求比值：
$$
\frac{AC}{AB}=\frac{2BG}{AB}
$$
其中$BG,AB$就是所谓的共动点顶点的两条线段，而此两者另一段点均为定点，因此可以使用前文提及的**双动线段比例最值问题**模型来解决（有需要系统研究的真的可以参考这篇[往期文章](https://blog.hxrch.top/posts/%E5%8F%8C%E5%8A%A8%E7%BA%BF%E6%AE%B5%E6%AF%94%E4%BE%8B%E6%9C%80%E5%80%BC%E9%97%AE%E9%A2%98%E5%8F%8D%E6%BC%94%E5%8F%98%E6%8D%A22/)）。虽然图形看上去复杂，但该模型的核心依然是构造相似三角形对线段比例进行转化，将**两动变为一定一动**。

为此，我们可以构造“母子相似”三角形，即在射线$AB$上取一点$K$并连接$GK$，使得$\angle AGK=\angle ABG$，则由这一组角相等和一组公共角$\angle BAG$，可以得到一组相似三角形：
$$
\triangle BAG\sim\triangle GAK
$$
由此不难得到
$$
\frac{AC}{AB}=\frac{2BG}{AB}=\frac{2GK}{AG}=\frac{2}{3}GK
$$
同时可以得到新构造的点$K$的一些信息：
$$
\frac{AB}{AG}=\frac{AG}{AK}\Rightarrow AB\cdot AK=AG^2=9
$$
此时我们便把点$K$和已知轨迹的点$B$联系了起来。但因为我们已经把原式转化为了$\frac{2}{3}GK$，而且点$G$是一个定点，那么我们只需把点$K$的运动轨迹求出来即可。该怎么办呢？没错，定积定角，**反演变换**（想要进一步了解的可以看往期[这篇介绍反演变换的文章](https://blog.hxrch.top/posts/%E5%87%A0%E4%BD%95%E4%B9%8B%E5%88%A9%E5%88%83%E5%8F%8D%E6%BC%94%E5%8F%98%E6%8D%A21/)）！这就是典型的**线生圆**模型！正如上图，只需过点$A$向$BC$作垂交于点$H$，再过点$K$作$AK$的垂线交刚才所作的$AH$的延长线于点$W$。此时不难发现图中有了新的一组“反A相似”三角形：
$$
\triangle ABH\sim\triangle AWK
$$
由此我们也可以得到$AB\cdot AK$的另一表示方式：
$$
\frac{AB}{AW}=\frac{AH}{AK}\Rightarrow AB\cdot AK=AH\cdot AW
$$
将此式与我们得到的上一条等式等量代换，便可得
$$
AH\cdot AW=9
$$
那这条等式有什么用呢？别急，我们仔细分析，其实会发现其中线段$AH$的长度是定值：只需在$\mathrm{Rt}\triangle ADH$中，由$\angle DAH=30\degree$便可得出
$$
AH=AD\cdot\cos\angle DAH=2\cos30\degree=\sqrt3
$$
如此一来，线段$AW$的长度和位置也都确定了：
$$
AW=\frac{9}{AH}=\frac{9}{\sqrt3}=3\sqrt3
$$
又因为$\angle AKW=90\degree$，所以不难得出点$K$的运动轨迹为以线段$AW$为直径的圆！且其半径可以算出为$\frac{3}{2}\sqrt3$。那么连接$OK,OG$，在$\triangle OGK$中由三角形三边关系可知$GK$最短时点$K$应在点$G$左侧且$K,G,O$三点共线，如下图所示。

![第三题-平面几何法-2](https://img.hxrch.top/20260504001811436.svg)

现在问题就转化为了求此图中线段$BD$的长度。再仔细观察一下这幅图，可以发现$\angle AOG$很像是$90\degree$的样子，如果真是那就可以极大地简化导边步骤，所以可以先尝试证明一下其为直角——巧了！如果我们利用上已知的边长，那么刚好两边夹一角，可以证明一组相似三角形：
$$
\left.\begin{align}
\frac{AD}{AG}=\frac{AH}{AO}=\frac{2}{3},\\
\angle DAH=\angle GAO
\end{align}\right\}
\Rightarrow\triangle DAH\sim\triangle GAO
$$
于是
$$
\angle AOG=\angle AHD=90\degree
$$
惊奇的是，又由于同一个圆内的半径长度相等，即$OA=OK$，我们证明了$\triangle KAO$是等腰直角三角形！那么就应该有
$$
\angle BAH=\angle KAO=45\degree
$$
又因为$AH\perp BC$，所以$\triangle BAH$也是一个等腰直角三角形，即有$AH=BH$，如此下来，线段$BD$的长度就可以轻松求出啦：
$$
BD=BH-DH=AH-DH=\sqrt3-1
$$

> 看到这里，想必大家一定有点疑惑：这道题用代数解法如此简单，为什么还要研究纯平面几何的解法呢？那是因为几何法在我个人看来是比较有趣的，且可操作性非常高，也是真的可以锻炼我们思维能力的一种有效方式。不过若是在正式考场上，则还是建议使用代数法减少思考时间和步骤书写时间（其实这个几何法只是图看着复杂点，基本上没有计算量，就是写过程麻烦些，选填就可以随便用）。

## 第四题

### 题面

（无图）在$\triangle ABC$中，角$A,B,C$所对的边分别为$a,b,c$，$D$是$AB$的中点，若$CD=1$，且$(a-\frac{1}{2}b)\sin A=(c+b)(\sin C-\sin B)$，则当$ab$取最大值时$\triangle ABC$的周长为__________.

### 官方解法：三角法

> **官方思路：** 典型解三角形题目，先用余弦定理得到边与边之间的部分关系，再用正弦定理将条件角化边，最后利用基本不等式探究所求式最值及其取等条件。

![第四题-三角法](https://img.hxrch.top/20260504072234500.svg)

如上图，设$\angle CDA=\theta$，则$\angle CDB=\pi-\theta$，在$\triangle CDA$和$\triangle CDB$中分别应用余弦定理，可得
$$
\cos\theta=\frac{\frac{c^2}{4}+1-b^2}{c},\qquad\cos(\pi-\theta)=\frac{\frac{c^2}{4}+1-a^2}{c}
$$
又因为
$$
\cos\theta+\cos(\pi-\theta)=0
$$
所以整理可得
$$
c^2=2(a^2+b^2)-4
$$
由此我们得到了关于大三角形三边的一条等式了（其实这一步也可以通过**中线长定理**一步实现，不过余弦定理是其本质），接下来由$(a-\frac{1}{2}b)\sin A=(c+b)(\sin C-\sin B)$及正弦定理，得
$$
(a-\frac{1}{2}b)\ a=(c+b)(c-b)
$$
整理即
$$
a^2+b^2-c^2=\frac{ab}{2}
$$
结合上一步得到的等式，可得
$$
a^2+b^2+\frac{ab}{2}=4
$$
又由基本不等式$a^2+b^2\geq 2ab$，当且仅当$a=b$时取等，有
$$
4\geq 2ab+\frac{ab}{2}=\frac{5ab}{2}
$$
解得
$$
ab\leq\frac{8}{5}
$$
即$a=b=\frac{2\sqrt{10}}{5}$时取等，此时
$$
c^2=2(\frac{8}{5}+\frac{8}{5})-4=\frac{12}{5}\Rightarrow c=\frac{2\sqrt{15}}{5}
$$
综上所述，当$ab$取最大值时$\triangle ABC$的周长为
$$
C_{\triangle ABC}=\frac{4\sqrt{10}+2\sqrt{15}}{5}
$$

> 此三角法考查较为综合，涵盖余弦定理和正弦定理，并同时考查了基本不等式，为常规解法。当然以下我会带来计算量稍小的平面几何解法。

### Mine-平面几何法

> 首先声明一下，此题不适宜使用纯几何做法！毕竟题干中那一条三角相关的等式还是借助正余弦定理来转化会好一些，此题的平面几何方法仅限该等式转化后的步骤。

如下图，这种题在初中也很常见，可以转化为一道很经典的面积最值问题~~（当然经常做这类题的同学都知道最值应该在其为以定边为底的等腰三角形时取到）~~，这思路有点类似前文第二题（将数量积转化为面积），这里则是将单纯的边长乘积结合其夹的定角转化为三角形的面积问题，最后即通过动点的运动轨迹证明出何时取最大值；另一方面，这题与前文第三题也有相似之处，同样是作平行线将处在$\triangle CAB$内部的定长线段$CD$转化为底边，但由于点$D$是边$BC$的中点，所以这种做法在这里还有一个特殊的名字：<strong style="color:red;">倍长中线</strong>。

![第四题-平面几何法](https://img.hxrch.top/20260504083958923.svg)

首先我们转化一下题目中的三角等式条件，同样是正弦定理角化边，得
$$
(a-\frac{1}{2}b)\ a=(c+b)(c-b)
$$
整理可得
$$
a^2+b^2-c^2=\frac{ab}{2}
$$
接下来由余弦定理的推论，有
$$
\cos\angle ACB=\frac{a^2+b^2-c^2}{2ab}=\frac{\frac{ab}{2}}{2ab}=\frac14
$$
既然我们已经将三角等式的条件转化为了$\angle ACB$的大小，那现在就按照倍长中线思路，如上图，延长$CD$至点$G$，使得$DG=CD$，连接$AG$，则我们不难通过边角边证明出一组全等三角形：
$$
\left.\begin{align}
CD&=GD,\\
\angle CDB&=\angle GDA,\\
AD&=BD
\end{align}\right\}
\Rightarrow\triangle CDB\cong\triangle GDA
$$
此时我们便会发现$ab$与一个底边确定的$\triangle AGC$的面积成正比，于是$ab$取最大值可转化为$S_{\triangle AGC}$取最大值：
$$
ab=\frac{\frac12ab\sin\angle ACB}{\frac12\sin\angle ACB}=\frac{2S_{\triangle ACB}}{\sin\angle ACB}=\frac{2S_{\triangle AGC}}{\sin\angle ACB}\Rightarrow ab\propto S_{\triangle AGC}
$$
注意上式中$\sin\angle ACB$为定值，但其实我们不需要求出其具体值，只需知道它是一个常数即可，因为我们所求的不是$ab$的最大值，而是在其取最大值的状态下$\triangle ABC$的周长。接下来，为了得到点$A$的运动轨迹，我们继续利用刚才的全等三角形，有
$$
\angle DCB=\angle DGA\Rightarrow BC\parallel AG
$$
因此
$$
\angle GAC+\angle ACB=180\degree\Rightarrow\cos\angle GAC=-\cos\angle ACB=-\frac14
$$
至此我们会发现在$\triangle GAC$中存在定边$GC$和定角$\angle GAC$，那么根据初中数学知识，我们不难分析出点$A$是在一个定圆上运动的，正如上图所示。如果我们把$\triangle AGC$中$GC$边上的高$AH$作出来，就可知当且仅当点$A$为$\overset{\Huge\frown}{GC}$的中点即$AC=AG$时，$AH$取得最大值，又因为底边$GC$为定长线段，故$\triangle GAC$的面积此时也取得最大值，再由$ab$正比与$\triangle GAC$的面积，我们可知当且仅当$AC=AG$即$AC=BC$时$ab$取最大值！那接下来就是解三角形的时刻了，我们不难在$\triangle AGC$中解出（可用余弦定理列方程求解，具体过程就不写了，不属于纯几何板块😓）：
$$
AG=AC=\frac{2\sqrt{10}}{5}\Rightarrow AB=AC=\frac{2\sqrt{10}}{5}
$$
再在$\triangle ACB$中，已知两边夹一角，也可以由余弦定理解得对边
$$
AB=\frac{2\sqrt{15}}{5}
$$
所以当$ab$取最大值时，$\triangle ABC$的周长为
$$
C_{\triangle ABC}=AB+AC+AB=\frac{4\sqrt{10}+2\sqrt{15}}{5}
$$

> 综上所述，我认为虽然此题可以用几何做法来解决，但其优势并没有很明显，仅为有一个明确的方向、更加清晰的思路，计算量在这一道题中并没有体现出量级的优势，并且在开始和结束时并非纯几何法，不过着实可以减少一些不等式、方程间的代换。所以我给这道题的评价是可以酌情使用自己擅长的解法来解决，不必追求几何法（这道题的设计初衷也不是为了几何法来的。。），将此题放在这篇文章中的目的仅为说明其不必全过程代数，是可以有直观解释的。

## 第五题

### 题面

（无图）已知$\triangle ABC$面积为$1$，边$AC,AB$上的中线为$BD,CE$，且$BD=2CE$，则边$AB$长度的最小值为__________.

### 官方解法：三角法

> **官方思路：** 利用线段长度的关系，设其中一条线段，就可以表示相关线段，再引入$\angle BGC=\theta$，利用面积关系找到一个等式，然后由余弦定理求$BE$边，最后转化为角的函数来求最值即可。

![第五题-三角法](https://img.hxrch.top/20260504113610928.svg)

如上图，设$BD$交$CE$于点$G$，依题意得点$G$为$\triangle ABC$的重心。由$BD=2CE$，设$GE=x,\angle BGC=\theta$，则$CG=2x,BD=6x,BG=4x,DG=2x$。再来表示$\triangle BGC$的面积：
$$
S_{\triangle BGC}=\frac23S_{\triangle BDC}=\frac23\cdot\frac12S_{\triangle ABC}=\frac13
$$
又因为
$$
S_{\triangle BGC}=\frac12BG\cdot CG\sin\theta=\frac12\cdot4x\cdot2x\sin\theta=4x^2\sin\theta
$$
所以
$$
4x^2\sin\theta=\frac13\Rightarrow x^2=\frac{1}{12\sin\theta}
$$
由余弦定理，知
$$
\begin{align}
BE^2&=x^2+{(4x)}^2-2x\cdot4x(-\cos\theta)\\
&=17\cdot\frac{1}{12\sin\theta}+8\cos\theta\cdot\frac{1}{12\sin\theta}\\
&=\frac{17+8\cos\theta}{12\sin\theta}
\end{align}
$$
此时进行换元，令$t=\frac{17+8\cos\theta}{12\sin\theta}>0$，并结合辅助角公式，可得
$$
\begin{align}
17&=12t\cdot\sin\theta-8\cos\theta\\
&=\sqrt{64+144t^2}\cdot\sin(\theta-\varphi)\\
&\leq\sqrt{64+144t^2}
\end{align}
$$
于是可解得
$$
t^2\geq\frac{225}{144}
$$
又由$t>0$，可知
$$
t\geq\frac54\Rightarrow BE^2\geq\frac54\Rightarrow BE\geq\frac{\sqrt{5}}{2}
$$
所以
$$
AB=2BE\geq\sqrt5
$$

> 这份官方解析我在第一次看的时候也是真的震惊到我了，其中最关键的一步就是这个换元了，换元之后整理等式然后运用辅助角公式求解其取值范围，这着实非常巧妙。也是这时我才意识到除了二次分式可以用这种方法求取值范围（习惯上称为“万能k法”），类似这种其次弦三角函数的分式也可以换元，而且我发现它们都有一个共同点：等式整理后自带取值范围，这也是这两类分式可以这么求取值范围的原因。不得不说“万能k法”是真的好用啊，我想如果没有此法就只能求导解决了吧。。

### Peer-平面向量法

> 为什么会有这个板块呢？当然是我们年级陈同学的鼎力推荐啊！！！陈同学作为他们班级参赛代表的智囊，在备赛时提出了这一特殊而又引人注目的解法，而由参赛代表孙同学上台讲解。由于这一解法不同于官方的三角法，且计算较少，思路清晰，是很新颖的平面向量解法，所以孙同学和陈同学这一组也拿到了唯二的特等奖之一！

> 以下请欣赏优雅的平面向量！

![第五题-平面向量法](https://img.hxrch.top/20260504124201851.svg)

我们从题目所给的条件入手，首先是为数不多的线段比例关系：
$$
BD=2CE
$$
此时我们就可以考虑把这两条线段改写成向量形式，并用一组基底来分别表示这两个向量：~~为了追求对称美~~，我们选择以$\{\overrightarrow{AB},\overrightarrow{AC}\}$作为这组基底，则这两个向量可以这样表示：
$$
\overrightarrow{BD}=\overrightarrow{AD}-\overrightarrow{AB},\qquad\overrightarrow{CE}=\overrightarrow{AE}-\overrightarrow{AC}
$$
我们再用上中点的条件，有
$$
\overrightarrow{AD}=\frac12\overrightarrow{AC},\qquad\overrightarrow{AE}=\frac12\overrightarrow{AB}
$$
所以
$$
\overrightarrow{BD}=\frac12\overrightarrow{AC}-\overrightarrow{AB},\qquad\overrightarrow{CE}=\frac12\overrightarrow{AB}-\overrightarrow{AC}
$$
于是有
$$
\Big|\overrightarrow{BD}\Big|=2\Big|\overrightarrow{CE}\Big|\Rightarrow\Big|\overrightarrow{BD}\Big|^2=4\Big|\overrightarrow{CE}\Big|^2
$$
即
$$
(\frac12\overrightarrow{AC}-\overrightarrow{AB})^2=4(\frac12\overrightarrow{AB}-\overrightarrow{AC})^2
$$
将该式展开并整理可得
$$
5AC^2=4\overrightarrow{AB}\cdot\overrightarrow{AC}
$$
接下来我们就需要将平面向量带给我们的结论转化为几何条件，即将等式中含向量形式的项改写为纯几何形式，故此设$\angle BAC=\theta$，并展开数量积$\overrightarrow{AB}\cdot\overrightarrow{AC}$，即
$$
5AC^2=4AB\cdot AC\cdot\cos\theta
$$
对此式稍加整理，又因为所求为线段$AB$的最小值，故为了消掉$AC$，这里用$AB$来表示$AC$，便可得
$$
AC=\frac45AB\cos\theta
$$
最后，我们用上题目所给的面积条件，有
$$
S_{\triangle ABC}=\frac12AB\cdot AC\cdot\sin\theta=1
$$
用$AB$替换$AC$并整理，得
$$
AB^2=\frac{5}{2\sin\theta\cos\theta}=\frac{5}{\sin2\theta}
$$
由$\sin2\theta\leq1$可得
$$
AB^2\geq5\Rightarrow AB\geq\sqrt5
$$
验证取等条件：当且仅当$2\theta=\frac{\pi}{2}+2k\pi$即$\theta=\frac{\pi}{4}+k\pi$时取等，而又因为
$$
AC=\frac45AB\cos\theta>0\Rightarrow\cos\theta>0\Rightarrow\theta<\frac{\pi}{2}
$$
所以
$$
\theta\in(0,\frac{\pi}{2})
$$
所以当且仅当$\theta=45\degree$时原式等号成立，故$AB$长度的最小值为$\sqrt5$。

> 是的，用平面向量来解这道题，答案就这么水灵灵地出来了。只需按照题意一步一步利用所给条件，便可轻松化解难题，不但思路简明，而且计算量比纯三角法小一些，不得不说，神来之笔！

### Mine-平面几何法

如下图，我承认这幅图看着确实很复杂，而且比前文每一道题几何法的图都要复杂——但是，其思路还是非常清晰的：我们先将交叉线段$BD,CE$其中的一条进行平移，使两者具有公共端点，以便后续条件的运用，接下来就可以根据线段间的定比运用<strong style="color:red;">阿氏圆</strong>（全称阿波罗尼斯圆，Apollonius圆）相关知识，探究一些线段取得最值的情况，最后得到答案。

> 全场最优雅的表演开始！

![第五题-平面几何法](https://img.hxrch.top/20260504185850258.svg)

首先是平移转化，过点$D$作$DM\parallel CE$交$AB$于点$M$，于是有
$$
\triangle ADM\sim\triangle ACE
$$
因此
$$
\frac{DM}{CE}=\frac{AM}{AE}=\frac{AD}{AC}=\frac12
$$
又因为$BD=2CE$，所以
$$
BD=4DM
$$
这时我们就可以进一步求出点$D$的限定位置了，由$\frac{BD}{DM}=4$为定值，可知点$D$一定在一个阿氏圆上，虽然这个圆位置不固定，但是我们后续可以据此来推出一些最值相关的信息。所以我们需要先把该阿氏圆表示出来，只需根据以下这一阿氏圆的结论（更多详情还请自行查阅互联网，很遗憾我目前还没有写过关于阿氏圆的文章，本文仅作针对此例题的相关分析）：
$$
\boxed{\text{点$D$在以点$D$在直线$AB$上的两个特殊点的连线为直径的圆上}}
$$
那如何理解这句话呢？一步一步来，我们先把这两个**特殊点**找出来：若点$D$在射线$MB$上，记此时点$D$为上图中的点$P$，则有
$$
BP=4PM
$$
另一类情况，若点$D$在射线$MA$上——先别着急设新点，因为其实我们会发现点$A$恰好满足
$$
BA=4AM
$$
所以点$A$恰恰就是我们要找的另一个特殊点！由此一来，线段$AP$理论上就是点$D$所在阿氏圆的直径了，以下通过类似证明角平分线定理的方式证明这一猜想：过点$M$作平行于$BD$直线，分别交$DP$延长线和线段$AD$于点$J,K$，则有
$$
\left\{\begin{align}
\triangle BDP\sim\triangle MJP\Rightarrow\frac{BD}{MJ}=\frac{BP}{MP}=4,\\
\triangle ABD\sim\triangle AMK\Rightarrow\frac{BD}{MK}=\frac{AB}{AM}=4
\end{align}\right.
$$
此时再结合等式$\frac{BD}{DM}=4$，等量代换可得如下一条很重要的等式
$$
DM=MJ=MK
$$
所以点$D$应该在以$M$为圆心、$MJ$为半径的圆上（但请注意这**不是**阿氏圆），即我们证明了
$$
\angle KDJ=90\degree\Rightarrow\angle ADP=90\degree
$$
如此一来，我们就可以在$\mathrm{Rt}\triangle APD$中，求出点$D$的限定位置了。没错，经过我们巧妙的证明，可知其就是以$AP$为直径的圆！这印证了最开始阿氏圆的那条结论。接着我们是时候用上题目所给的剩下两个条件了：$AE=BE,S_{\triangle ABC}=1$，那我们不妨先设$EM=x$，得$AB=4x$，并过点$D$将$\triangle ABD$的高$AH$作出来，由此表示$\triangle ABC$的面积：
$$
S_{\triangle ABC}=2S_{ABD}=2\times\frac12AB\cdot DH=4x\cdot DH=1
$$
于是
$$
DH=\frac{1}{4x}
$$
最后我们再根据点$D$在以$AP$为直径的圆上这一条件，可知$DH$的长度一定有一个**最大值**——这个圆的半径！故我们可以先用$x$将其半径表示出来，然后得到一个**不等式**以解出$x$的最值。于是由$EM=x$的定义，结合点$P$、点$A$的位置，不难得到
$$
BM=3x,\qquad PM=\frac35x,\qquad AM=x
$$
所以可知该圆的半径为
$$
r=\frac12AP=\frac12(PM+AM)=\frac12(\frac35x+x)=\frac45x
$$
现在便可由上述分析，得出该不等式
$$
DH\leq r\Rightarrow\frac{1}{4x}\leq\frac45x
$$
最终解得
$$
x\geq\frac{\sqrt5}{4}
$$
将$x$用$AB$代替，有
$$
AB=4x\geq\sqrt5
$$

> 最优雅的表演结束了——在此我再解释一下此方法的可行性：阿氏圆最特殊之处在于其圆心是恰好在直线$AB$上的，换句话说，它的一条直径$AP$就在直线$AB$上，所以点$D$到$AB$的距离才可以与其拥有固定表示（$r=\frac45x$，无论图上的点如何运动，该等式依然成立）的半径相比较。也正是有了这样的线段长度比较，我们才能得到最后如此简洁的不等式以解决此问题。

# 体会与心得

纵观整篇文章，我为这五道题的平面几何法都标注了一个核心思想，分别是：**动静互换**、**探照灯模型**、**反演变换**、**倍长中线**、**阿氏圆**，其中不乏我们最常见的倍长中线，也有非常罕见的反演变换，由此可知平面几何学的灵活多变真的是让人难以捉摸。不过，我想这才是我们学习平面几何的终极奥义吧，只有通过一题多解的形式，我们的思维才更有可能得到提升。

与如解析几何、三角几何、平面向量等的其他解题方法相比，平面几何法的计算量通常远小于这些方法的，然而思维性却通常远大于其他方法，我想这应该也是“舍得”的一种外在表现吧，舍去计算量，用思维替代。

如果目前你被困于解题这个巨大的天坑之中，我给出的建议是，可以换种角度，从一个新的视角重新审视同一道题目，也许新的灵感就出现呢！

最后，对于本篇文章如有疑惑或者一些更好的解法，欢迎在下方评论区中发表你的看法~ 我在看到后尽量第一时间回复，当然也可以相互讨论解决问题哦。每一个人的求知欲都是值得被保护的！

最后此处以苏联数学家阿纳托利·纳乌莫维奇·雷巴科夫（Анатолий Наумович Рыбаков）的一句话结束本篇文章：*时间是个常数，但对勤奋者来说，是个“变数”。用“分”来计算时间的人比用“小时”来计算时间的人时间多59倍。*
