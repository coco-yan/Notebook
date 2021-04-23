<h1 style="color:pink;font-size:30px;text-align:center;">MD语法总结</h1> 

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [杂项 1](#杂项-1)
- [数学 2](#数学-2)
- [图表 3](#图表-3)
  - [流程类 3.1](#流程类-31)
  - [高级图 3.2](#高级图-32)
- [幻灯片](#幻灯片)

<!-- /code_chunk_output -->

# 杂项 1
**字体缩进颜色**

<center><font size=9 face="华文行楷" color=orange>华文行楷居中</font></center> 

```html
<center><font size=9 face="华文行楷" color=orange>华文行楷居中</font></center> 
```

缩进采用html语法   

```html
<p style="text-indent:1em">你好呀</p>
<p style="text-indent:2em">你好呀</p>
```

 导入文件 
` @import "path" {width="300px" height="200px" title="图片的标题" alt="我的 alt"}`
(这样可以设置图片大小)

<kbd>ese</kbd>
按键 `<kbd>ese</kbd>`

上标   30^th^        
下标   H~2~O




- 可以跨表格操作

First Header | Second Header
:-------: | :-------------:
Content from cell 1| Content from cell 2
Content in the first column | Content in the second column
>         |  跨表格
ab        |   



# 数学 
各种用法查询 [Katex](https://katex.org/docs/supported.html) 以及 [MathJax](http://docs.mathjax.org/en/latest/) 在此仅补充常用的.
**注意,数学符号渲染引擎可更改**
$$
\begin{pmatrix}
   a & b \\
   c & d
\end{pmatrix}
$$












# 图表 3
## 流程类 3.1
- **flow** [flowchart.js](https://flowchart.js.org/)
- **sequence** [sequence.js](https://bramp.github.io/js-sequence-diagrams/)
- **Mermaid** Mermaid
## 高级图 3.2
- **vega** [Vega](https://vega.github.io/vega/examples/)


1. ***flowchart***
```flow
st=>start: Start:>http://www.google.com[blank]
e=>end:>http://www.google.com
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes
or No?:>http://www.google.com
io=>inputoutput: catch something...
para=>parallel: parallel tasks
st->op1->cond
cond(yes)->io->e
cond(no)->para
para(path1, bottom)->sub1(right)->op1
para(path2, top)->op1
```

---



2. ***sequence***

```sequence {theme=hand}
Title: Here is a title
A->B: Normal line
B-->C: Dashed line
C->>D: Open arrow
D-->>A: Dashed open arrow
```
```
Title: Here is a title
A->B: Normal line
B-->C: Dashed line
C->>D: Open arrow
D-->>A: Dashed open arrow
```


```sequence
# Example of a comment.
Note left of A: Note to the\n left of A
Note right of A: Note to the\n right of A
Note over A: Note over A
Note over A,B: Note over both A and B
```
```
Note left of A: Note to the\n left of A
Note right of A: Note to the\n right of A
Note over A: Note over A
Note over A,B: Note over both A and B
```

# 幻灯片
```
---
presentation:
  width: 800
  height: 600
  theme: "serif.css"
---

<!-- slide -->
...

<!-- slide -->


```
