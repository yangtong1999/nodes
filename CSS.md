###### 背景
background-color不能继承，所有的背景属性都不能够继承，默认值为transparent(透明)

**背景重复**

background-repead属性

repeat-x:向X方向平铺，repeat-y:向Y方向平铺，no-repead：不允许图像在任何方向上平铺

一个图片背景居中：

```
background-position:center;
```
###### 文本
**text-indent**
可以继承的属性，
用于块级元素，不能用于行内元素
```
//将段落第一行缩进，可以为负值
p{
    text-indent:5em;
}
```
行内元素的缩进可以用padding来实现
###### text-align
影响一个元素中文本行相互之间的对齐方式

left、right、center会导致元素中的文本分别左对齐，右对齐和居中

###### word-spacing属性
改变字之间的标准间隔，接收正值和负值

###### text-transform属性
处理文本的大小写

属性有四个值：


