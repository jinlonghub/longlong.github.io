---
layout: post
title: "Jekyll-MarkDown-MathJax"
date: 2017-09-17 09:00:00 +0800 
categories: Jekyll
tag: Jekyll
---
* content
{:toc}

<!-- more -->
<!-- TOC -->

## Jekyll：简单的博客形态的静态站点生产机器   

---
  
>[http://jekyll.com.cn/](http://jekyll.com.cn/)  

---

## MarkDown基本语法         

---

>[MarkDown语法中文说明](http://wowubuntu.com/markdown/#list)     
>[MarkDown入门参考](http://xianbai.me/learn-md/index.html)    

---
    
## MathJax：在MarkDown网页中添加数学公式       

---

>[MathJax入门指南](http://mathjax-chinese-doc.readthedocs.io/en/latest/start.html)   


---

- 在MarkDown中添加数学公式最简单方法：
  1. 在Markdown中添加MathJax引擎。    
  2. 使用Tex在md文件中写公式。 

  - 在Markdown中添加MathJax引擎方法：在页面文件的的 `<head>` 块中添加如下设置。    
    如果需要的话也可以放置到 `<body>` 块中，但是head是更好的选择。这样就会从分发服务器中加载最新版本的MathJax，并配置它识别用Tex和MathML符号书写的公式。如果浏览器原生支持MathML格式，MathJax就会生成用MathML输出，不然的话就用HTML和CSS去显示公式。这是最常见的配置，它可以满足大部分人的需求。但是其他配置也是可以用的，你可以提供参数去配置MathJax，使其更满足你的要求。    

> `<script type="text/javascript"  `    
>   `src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default">`    
> `</script>`    

  - 然后使用Tex在md文件中写公式：    
    - 行间公式：`$$公式$$`      
    - 行内公式：本来Tex中使用`\(公式\)`表示行内公式，但因为Markdown中`\`是转义字符，所以在Markdown中输入行内公式使用`\\(公式\\)`，如下代码：    

    > `$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$`   
    > `\\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\)`   

    行间公式（显示结果）：公式前文字 $$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$ 公式后文字。    

    行内公式（显示结果）：公式前文字 \\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\) 公式后文字。    

---

## MarkDown输入数学公式具体语法 

>[MarkDown输入数学公式具体语法](http://oiltang.com/2014/05/04/markdown-and-mathjax/)

```cpp
1．如何插入公式

LaTeX的数学公式有两种：行中公式和独立公式。行中公式放在文中与其它文字混编，独立公式单独成行。

行中公式可以用如下两种方法表示：

＼(数学公式＼)　或　￥数学公式￥（要把人民币符号换成美元符号）

独立公式可以用如下两种方法表示：

＼[数学公式＼]　或　￥￥数学公式￥￥（要把人民币符号换成美元符号）

例子：＼[J\alpha(x) = \sum{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha}＼]

显示： J<em>\alpha(x) = \sum</em>{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha}

2．如何输入上下标

^表示上标, _表示下标。如果上下标的内容多于一个字符，要用{}把这些内容括起来当成一个整体。上下标是可以嵌套的，也可以同时使用。

例子：x^{y^z}=(1+{\rm e}^x)^{-2xy^w}

显示： x^{y^z}=(1+{\rm e}^x)^{-2xy^w}

另外，如果要在左右两边都有上下标，可以用\sideset命令。

例子：\sideset{^12}{^34}\bigotimes

显示： \sideset{^1<em>2}{^3</em>4}\bigotimes

3．如何输入括号和分隔符

()、[]和|表示自己，{}表示{}。当要显示大号的括号或分隔符时，要用\left和\right命令。

例子：f(x,y,z) = 3y^2z \left( 3+\frac{7x+5}{1+y^2} \right)

显示： f(x,y,z) = 3y^2z \left( 3+\frac{7x+5}{1+y^2} \right)

有时候要用\left.或\right.进行匹配而不显示本身。

例子：\left. \frac{{\rm d}u}{{\rm d}x} \right| _{x=0}

显示：  \left. \frac{{\rm d}u}{{\rm d}x} \right| _{x=0} 

4．如何输入分数

例子：\frac{1}{3}　或　1 \over 3

显示： \frac{1}{3} 　或  1 \over 3

5．如何输入开方

例子：\sqrt{2}　和　\sqrt[n]{3}

显示： \sqrt{2} 　和　 \sqrt[n]{3}

6．如何输入省略号

数学公式中常见的省略号有两种，\ldots表示与文本底线对齐的省略号，\cdots表示与文本中线对齐的省略号。

例子：f(x1,x2,\ldots,xn) = x1^2 + x2^2 + \cdots + xn^2

显示： f(x<em>1,x</em>2,\ldots,x<em>n) = x</em>1^2 + x<em>2^2 + \cdots + x</em>n^2

7．如何输入矢量

例子：\vec{a} \cdot \vec{b}=0

显示： \vec{a} \cdot \vec{b}=0

8．如何输入积分

例子：\int_0^1 x^2 {\rm d}x

显示： \int_0^1 x^2 {\rm d}x

9．如何输入极限运算

例子：\lim_{n \rightarrow +\infty} \frac{1}{n(n+1)}

显示： \lim_{n \rightarrow +\infty} \frac{1}{n(n+1)}

10．如何输入累加、累乘运算

例子：\sum{i=0}^n \frac{1}{i^2}　和　\prod{i=0}^n \frac{1}{i^2}

显示： \sum<em>{i=0}^n \frac{1}{i^2} 　和　 \prod</em>{i=0}^n \frac{1}{i^2}

11．如何进行公式应用

先要在［mathjax］后添加：

＜script type="text/x-mathjax-config"＞ MathJax.Hub.Config({ TeX: {equationNumbers: { autoNumber: ["AMS"], useLabelIds: true}}, "HTML-CSS": {linebreaks: {automatic: true}}, SVG: {linebreaks: {automatic: true}} }); ＜/script＞

例子：＼begin{equation}\label{equation1}r = rF+ \beta(rM – r_F) + \epsilon＼end{equation}

显示：\begin{equation}\label{equation1}r = rF+ \beta(rM – r_F) + \epsilon\end{equation}

引用：请见公式( \ref{equation1} )

12．如何输入希腊字母

例子： \alpha　A　\beta　B　\gamma　\Gamma　\delta　\Delta　\epsilon　E \varepsilon　　\zeta　Z　\eta　H　\theta　\Theta　\vartheta \iota　I　\kappa　K　\lambda　\Lambda　\mu　M　\nu　N \xi　\Xi　o　O　\pi　\Pi　\varpi　　\rho　P \varrho　　\sigma　\Sigma　\varsigma　　\tau　T　\upsilon　\Upsilon \phi　\Phi　\varphi　　\chi　X　\psi　\Psi　\omega　\Omega

显示：  \alpha  \beta  \gamma  \Gamma  \delta  \Delta

\epsilon  \varepsilon 　 \zeta  \eta  \theta  \Theta 　

\vartheta  \iota  \kappa  \lambda  \Lambda 　 \mu  \nu  \xi

\Xi 　 \pi  \Pi 　 \varpi 　 \rho  \varrho 　

\sigma  \Sigma  \varsigma 　 \tau  \upsilon  \Upsilon  \phi

\Phi 　 \varphi 　 \chi  \psi  \Psi 　 \omega  \Omega

13．如何输入其它特殊字符

关系运算符：  \pm ：\pm

\times ：\times

\div ：\div

\mid ：\mid

\nmid ：\nmid

\cdot ：\cdot

\circ ：\circ

\ast ：\ast

\bigodot ：\bigodot

\bigotimes ：\bigotimes

\bigoplus ：\bigoplus

\leq ：\leq

\geq ：\geq

\neq ：\neq

\approx ：\approx

\equiv ：\equiv

\sum ：\sum

\prod ：\prod

\coprod ：\coprod

集合运算符：  \emptyset ：\emptyset

\in ：\in

\notin ：\notin

\subset ：\subset

\supset ：\supset

\subseteq ：\subseteq

\supseteq ：\supseteq

\bigcap ：\bigcap

\bigcup ：\bigcup

\bigvee ：\bigvee

\bigwedge ：\bigwedge

\biguplus ：\biguplus

\bigsqcup ：\bigsqcup

对数运算符：  \log ：\log

\lg ：\lg

\ln ：\ln

三角运算符：  \bot ：\bot

\angle ：\angle

30^\circ ：30^\circ

\sin ：\sin

\cos ：\cos

\tan ：\tan

\cot ：\cot

\sec ：\sec

\csc ：\csc

微积分运算符：  \prime ：\prime

\int ：\int

\iint ：\iint

\iiint ：\iiint

\iiiint ：\iiiint

\oint ：\oint

\lim ：\lim

\infty ：\infty

\nabla ：\nabla

逻辑运算符：  \because ：\because

\therefore ：\therefore

\forall ：\forall

\exists ：\exists

\not= ：\not=

\not> ：\not>

\not\subset ：\not\subset

戴帽符号：  \hat{y} ：\hat{y}

\check{y} ：\check{y}

\breve{y} ：\breve{y}

连线符号：  \overline{a+b+c+d} ：\overline{a+b+c+d}

\underline{a+b+c+d} ：\underline{a+b+c+d}

\overbrace{a+\underbrace{b+c}<em>{1.0}+d}^{2.0} ：\overbrace{a+\underbrace{b+c}{1.0}+d}^{2.0}

箭头符号：  \uparrow ：\uparrow

\downarrow ：\downarrow

\Uparrow ：\Uparrow

\Downarrow ：\Downarrow

\rightarrow ：\rightarrow

\leftarrow ：\leftarrow

\Rightarrow ：\Rightarrow

\Leftarrow ：\Leftarrow

\longrightarrow ：\longrightarrow

\longleftarrow ：\longleftarrow

\Longrightarrow ：\Longrightarrow

\Longleftarrow ：\Longleftarrow

要输出字符　空格　#　$　%　&　_　{　}　，用命令：　\空格　#　\$　\%　\&　_　{　}

14．如何进行字体转换

要对公式的某一部分字符进行字体转换，可以用{\rm 需转换的部分字符}命令，
其中\rm可以参照下表选择合适的字体。
一般情况下，公式默认为意大利体。 
\rm　　罗马体　　   　　　　　
\it　　意大利体    
\bf　　黑体　　  　　　　　　
\cal 　花体   
\sl　　倾斜体　　  　　　　　
\sf　　等线体   
\mit 　数学斜体　　  　　　　
\tt　　打字机字体   
\sc　　小体大写字母  

``` 

---

`2017.09.17`       
