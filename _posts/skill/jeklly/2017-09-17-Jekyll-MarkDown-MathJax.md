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


---

`2017.09.17`       
