---
title: Markdown语法
date: 2020-03-15 03:52:45
author: rainbow
categories:
  - 前端
tags:
  - markdown
summary: markdown语法总结

img: 
cover: false
coverImg: # https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo/photo_mid/1.jpg

top: false
toc: true
mathjax: true

abbrlink: 1011929149
password:
---

# Markdown语法

## 简明教程

### 1.标题

#### 代码

```c
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

####  演示

![1](https://tva1.sinaimg.cn/large/00831rSTly1gcu3hw7gftj30b209gaac.jpg)

### 2.分级标题

#### 代码

注：`=``-`最少可以只写一个，兼容性一般

```md
一级标题
===================
二级标题
-------------------
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcu3whxby5j308y05gaa2.jpg)

### 3.TOC

#### 代码

注：根据标题生成目录，兼容性一般

```md
[TOC]
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcupuljt9fj308m0fq74n.jpg)

### 4.引用

#### 代码1(单行式)

```md
> hello world!
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcu43nefgtj30bb0383ya.jpg)

#### 代码2(多行式)

```md
> hello world!
hello world!
hello world!
```

或者

```md
> hello world!
> hello world!
> hello world!
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcuioz5ty7j307t03tmx0.jpg)

#### 代码3(多层嵌套)

```md
> aaaaaa
>> bbbbbb
>>> cccccc
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcwvi0invij308605o0sl.jpg)

### 5.行内标记

#### 代码

```md
标记之外`helloworld`标记之外
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcwvjaa5r9j309g024jr8.jpg)

### 6.代码块

注：与上文空一行

#### 代码1

```md
​```c
	int main(){
		printf("hello world!");
	}
​```
```

#### 演示

![8](https://tva1.sinaimg.cn/large/00831rSTly1gcuj08o6haj30dc04c0so.jpg)

#### 代码2(自定义高亮)

注：根据不同的语言配置不同的代码着色

```md
​```javascript
	var num = 0;
	for(var i = 0; i < 5; i++){
		num+=i;
	}
	console.log(num);
​```
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcujb3kxnhj30dg05p0st.jpg)

### 7.插入链接

#### 代码1(内链式)

```md
[百度1](http://www.baidu.com/"百度一下")
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcwvjo0azuj303j026a9u.jpg)

#### 代码2（引用式）

注：第二行一般放在文末

```md
[百度2][2]
[2]:http://www.baidu.com
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcwvjxr9ldj307o02g745.jpg)

### 8.插入图片

#### 代码(1内链式)

```md
![girl](/12.png)
```

#### 演示

![girl](https://tva1.sinaimg.cn/large/00831rSTly1gcujqbht7mj307l09jtbv.jpg)

#### 代码2(引用式)

```md
![girl][01]
[01]:Markdown语法/12.png '描述'
```

#### 演示

![girl][01]

[01]:https://tva1.sinaimg.cn/large/00831rSTly1gcujqbht7mj307l09jtbv.jpg  "描述"


## 进阶语法

### 9.视频插入

注：md语法本身不支持视频插入，常用做法是 插入HTML的iframe框架，通过网站自带的分享功能获取，或者伪造播放界面，实质是插入视频图片，然后通过点击跳转到相关页面

#### 代码1

`<iframe height=498 width=510 src='https://player.youku.com/embed/XMTE0NTQ1OTUy' frameborder=0 allowfullscreen="true"></iframe>`

#### 演示

<iframe height=498 width=510 src='https://player.youku.com/embed/XMTE0NTQ1OTUy' frameborder=0 allowfullscreen="true"></iframe>

#### 代码2

```md
![](https://tva1.sinaimg.cn/large/00831rSTly1gcuk75pri9j315j0prn15.jpg)
[天道]](https://v.youku.com/v_show/id_XMTE0NTQ1OTUy.html)
```



#### 演示

<img src="https://tva1.sinaimg.cn/large/00831rSTly1gcwvm3ki6aj315j0prq43.jpg" style="zoom:50%;" />

[天道](https://v.youku.com/v_show/id_XMTE0NTQ1OTUy.html)

### 10.序表

注：序号与正文用一个空格隔开

#### 代码1(有序)

```md
1. one
2. two
3. three
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcukrizd9wj307z03kglh.jpg)

#### 代码2(无序)

```md
- one
* two
+ three
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcuksxk289j308f042jr9.jpg)

#### 代码3(序表嵌套)

```md
1. one
	1. one-1
	2. two-2
2. two
	* two-1
	* two-2
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gculfz8ooej308f0623yh.jpg)

#### 代码4(序表嵌套代码块)

```md
* one

		var a = 10;
```
#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gculgh1k6xj30aq038745.jpg)
### 11.任务列表

注：与上文隔开一行

#### 代码

- [ ] 选项一
- [x] 选项二
- [ ] 选项三
#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gculk3oq4xj308y03imx2.jpg)

### 12.表情

:smile::laughing::heart_eyes::grin::wink::stuck_out_tongue_closed_eyes::+1:

[表情代码地址](https://www.webfx.com/tools/emoji-cheat-sheet/)

### 13.表格

注：`:`代表对齐方式，`:`与`|`之间不要有空格，否则对其会有些不兼容

#### 代码1

```md
| a        |     b     |       c |
| :------- | :-------: | ------: |
| 左对齐   |   居中    |  右对齐 |
| ======== | ========= | ======= |
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gculvctkfpj30ky04c748.jpg)

#### 代码2(简约写法)

```md
| a        |     b     |       c |
| :------- | :-------: | ------: |
| 左对齐   |   居中    |  右对齐 |
| ======== | ========= | ======= |

```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gculxsb215j30kh0450so.jpg)

#### 代码3(特殊表格)

注：markdown对合并单元格，以及其他特殊格式表格，markdown是无能为力的 所以常规的做法是使用`HTML标`签，但这样编写的效率极低。

但是借助工具的话，所有问题都迎刃而解。

在线生成HTML代码[Tables Generator](http://www.tablesgenerator.com/)(国外的站)

![](https://tva1.sinaimg.cn/large/00831rSTly1gcum24lurej30ux0hrjso.jpg)

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcumky1r6lj30kk02rt8j.jpg)

### 14.支持内嵌CSS样式

#### 代码

```html
<p style="color: #AD5D0F;font-size: 30px; font-family: '宋体';">内联样式</p>
```

#### 演示

![](https://tva1.sinaimg.cn/large/00831rSTly1gcuml6cfnhj305e02d3ye.jpg)

### 15.语义标记

| 代码              | 效果            |
| ----------------- | --------------- |
| `*斜体*`          | *斜体*          |
| `_斜体_`          | _斜体_          |
| `**加粗**`        | **加粗**        |
| `***斜体+加粗***` | ***斜体+加粗*** |
| `**_斜体+加粗_**` | **_斜体+加粗_** |
| `~~删除线~~`      | ~~删除线~~      |

### 16.语义标签

| 代码                   | 效果                |
| ---------------------- | ------------------- |
| `<i>斜体</i>`          | <i>斜体</i>         |
| `<b>加粗</b>`          | <b>加粗</b>         |
| `<em>强调</em>`        | <em>强调</em>       |
| `上<sup>标</sup>`      | 上<sup>标</sup>     |
| `下<sub>标</sub>`      | 下<sub>标</sub>     |
| ` <kbd>键盘文本</kbd>` | <kbd>键盘文本</kbd> |

### 17.公式

注：代码块居中，行内公式左对齐

#### 代码

```md
$$ 
	x = y^2 + 1 
$$
$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $
$$ x = y^2 + 1 $$
```



#### 演示

$$
x = y^2 + 1 
$$


$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

$$ x = y^2 + 1 $$

### 18.分隔符

注：最少三个`---`或`***`或`* * *`

#### 代码

```md
***
---
* * *
```

#### 演示

***

---

* * *

### 19.脚注

#### 代码

```md
Markdown[^1]
[^1]:Markdown是一种纯文本标记语言               // 在文章最后显示脚注
```

#### 演示

Markdown[^1]

[^1]:Markdown是一种纯文本标记语言

### 20.自动邮箱链接

#### 代码

` <xxx@outlook.com> `

#### 演示

<xxx@outlook.com>

### 21.流程图

#### 代码1

```md
st=>start: 启动
e=>end: 结束           
op1=>operation: 方案一
sub3=>subroutine: 重新制定方案
cond1=>condition: 行不行？|request
io=>inputoutput: 结果满意

st->op1->cond1
cond1(no,right)->sub3(right)->cond1(no,right)
cond1(yes)->io->e
```


#### 演示

```flow
st=>start: 启动
e=>end: 结束           
op1=>operation: 方案一
sub3=>subroutine: 重新制定方案
cond1=>condition: 行不行？|request
io=>inputoutput: 结果满意

st->op1->cond1
cond1(no,right)->sub3(right)->cond1(no,right)
cond1(yes)->io->e
```





### 22.时序图

#### 代码

```md
sequence
A->>B: 你好
Note left of A: 我在左边     // 注释方向，只有左右，没有上下
Note right of B: 我在右边
B-->A: 很高兴认识你
```

#### 演示

```sequence
A->>B: 你好
Note left of A: 我在左边
Note right of B: 我在右边
B-->A: 很高兴认识你
```

#### 代码详解

注：`A->>B`后面可以不写文字，但一定要写`:`

Note left of A代表注释在A的左边

| 符号 | 含义     |
| ---- | -------- |
| `-`  | 实线     |
| `>`  | 实心箭头 |
| `--` | 虚线     |
| `>>` | 空心箭头 |


### 23.Markdown编写工具

- PC端    [Typora](https://typora.io/)

- Android端    [纯纯写作](https://writer.drakeet.com/)