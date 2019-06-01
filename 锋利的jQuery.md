#### 认识jQuery
```
$(document).ready(function(){
    //...
});
//相当于window.onload方法
```

  \   |window.onload | $(document).ready()
---|---|---
执行时机 |等网页的内容全部加载完之后才能执行|网页中的DOM结构绘制完毕
编写个数|不能同时编写多个|能同时编写多个
简化写法|无|简化为：$(function(){//...});
++jQuery.noConflict()函数将变量$的控制权交给其他JavaScript库++

**jQuery选择器**

当要用jQuery检验某个元素在网页上是否存在，根据获取到的元素长度来判断：


```
if($("#tt").length >0){
  //  doSomething
}
```
##### jQuery实例
例1：给网页中的所有\<p>元素添加onclick事件

```
$("p").click(function(){//获取页面中的所有p元素，给每一个元素添加点击事件
    //doSomething
});
```
例2：使特定的一个表格隔行变色

```
$("#tb tbody tr:even").css("backgroundColor","#888");
/* 获取id为tb的元素，寻找他下面的tbody标签，寻找tbody下索引数是偶数的tr元素，改变他的背景色*/
```
例3：对多选框进行操作，输出多选框的个数

```
$("#btn").click(function(){
    //现使用属性选择器，然后用表单对象属性过滤，最后获取对象的长度
    var items = $("input[name = 'check']:check");
    alert("选中的个数为：" +items.length);
});
```
实例：某网站品牌的展示列表

```
$(function(){
    var $category = $("ul li:gt(5):not(:last)");//取得索引值大于5的品牌集合对象，除掉最后一项
    $category.hide();//取得的隐藏
    var $toggleBtn = $('div .showmore>a');//取得"显示全部品牌"的按钮
    $toggleBtn.click(function(){
    if(#category.is(":visible")){
        $category.hide();
        $(this).find('span')
        .text("显示显示品牌");
        $('ul li').filter(":contains('佳能'),:contains('尼康')")
        .removeClass("promoted");
    }else{
       $category.show();
        $(this).find('span')
        .text("精简显示品牌");
        $('ul li').filter(":contains('佳能'),:contains('尼康')")
        .addClass("promoted"); 
    }
        
    });
    
    
});
```
##### jQuery中的DOM操作
查找元素节点

```
var $li = $("ul li:er(1)");
var li_txt = $(li).text();
alert(li_text);
```
查找元素节点

用选择器找到需要的元素之后，可以使用attr()方法来获取它的各种属性的值


```
var $para = $("p");//获取元素节点
var p_txt = $para.attr("title");//获取它的节点属性
alert(p_txt);
```
创建节点
append()方法插入元素节点

```
var $li_1 = $("<li></li>");
$("ul").append($li_1);
```
可以直接在创建元素节点的时候直接创建属性节点

删除节点

三种方法：
- remove()

当删除节点之后，该节点包括的所有后代节点都被删除

```
$("ul li:eq(1)").remove();//获取第二个元素节点之后，把它从元素节点中删除
```

- detach()

绑定的事件，所有的附加数据都会被保留下来

```
//不会把匹配的元素从jQ中直接删除
$("ul li ").click(function(){
   alert($(this).html());
   
});
var $li = $("ul li:eq(1)").detach;//删除元素
$li.appendTo("ul");//重新追加此元素，绑定的事件还在
```

- empty();

清空节点，清空元素中所有的后代节点


```
$("ul li:eq(1)").empty();
//获取第二个元素节点后，清空元素里面的内容
```
复制节点

clone()方法

```
$("ul li").click(function(){
    $(this).clone().apendTo("ul");//复制当前的节点，并把它追加到ul元素中
});
```
替换节点

replaceWith方法


```
$("p").replaceWith("<strong>你最喜欢的水果是？</strong");
```
替换节点后，绑定的事件会一起消失

包裹节点

wrapAll()方法

会将所有匹配的元素都用一个元素来包裹

wrap()方法

会将所有的元素进行单独的包裹

wrapInner()方法

将每一个匹配的元素的子内容用其他结构化的标记包裹起来。

**属性操作**

attr()方法来获取和设置元素的属性，removeAttr()用来删除元素属性

样式操作

获取样式和设置样式
```
var p_class = $("p").attr("class","high");//设置元素的class为"high"
```
追加样式


```
//addClass()方法追加样式
$("p").addClass("another");//给p元素追加another类
```
CSS规定：

- 如果给一个元素添加多个class值，相当于合并两个的样式
- 如果有不同的class值设置了同一样式属性，后者覆盖前者

移除样式：removeClass()方法

切换样式：toggle方法

控制行为上的重复切换

判断是否含有某个样式：hasClass()方法，有的话返回true，没有返回false

###### 设置和获取HTML、文本和值

html()方法：用来读取设置某个元素中的HTML内容


```
<p><strong>你最喜欢的水果是？</strong></p>
var p_html = $("p").html();
alert(p_html);//<strong>你最喜欢的水果是？</strong>
```
text()方法：用来读取或设置某个元素中的文本内容

```
<p><strong>你最喜欢的水果是？</strong></p>
var p_text = $("p").text();
alert(p_text);//你最喜欢的水果是？
```
val()方法：  类似于JS中的value属性，可以用来设置和获取元素的值，无论元素是文本框，下拉列表，还是单选框，都可以返回元素的值


```
//下面的代码可以使多选框和复选框被选中
$(":checkbox").val(["选择2号","选择3号"]);
```
遍历节点

children()方法

用于取得匹配元素的子元素集合

next()方法

用于取得匹配元素后面紧邻的同辈元素

prev()方法

用于取得匹配元素前面紧邻的同辈元素

```
var $ul = $("ul").prev();
```
siblings()方法

用于取得匹配元素前后的紧邻的同辈元素

closest()

用于取得最近的匹配元素

CSS()方法

获取元素的样式属性,可以同时设置多个样式属性

在此方法中，如果属性中含有"-"符号，如果在设置这些属性的时候没有带引号，就要使用驼峰式写法

offset()方法

获取元素在当前视窗的相对偏移，返回的对象包括两个属性，top和left，只对可见元素有效

position()方法

获取元素相对于最近的一个position样式属性设置为relative或者absolute的父节点相对偏移

##### 案例：某网站的图片提示效果

```
$(function(){
  var x = 10;
  var y = 20;
  $("a.tooltip").mouseover(function(){
      this.myTitle = this.title;
      this.title = "";
      var imgTitle = this.myTitle?"<br/>"+this.myTitle:"";
      var tooltip = "<div id = 'tooltip'><img src = '>"+this.href+"'alt = '产品预览图'/>"+imgTitle+"</div>";
      $("body").append(tooltip);
      $("#tooltip")
      .css({
          "top":(e.pageY+y)+"px";
          "left":(e.pageX+x)+"px";
          
      }).show("fast");
  }
  ).mouseout(function(){
      this.title = this.myTitle;
      $("#tooltip").remove();
  }
  ).mousemove(function(){
      $("#tooltip")
      .css({
          "top":(e.pageY+y)+"px";
          "left":(e.pageX+x)+"px";
      }
      )
  }
  );
})
```
事件绑定

bind()方法

可以匹配元素进行特定事件的绑定

hover()方法

用于模拟光标悬停事件，当光标移动到元素上时，会触发指定的第一个函数，当光标移出这个元素的时候，会触发指定的第二个函数


```
$(function(){
    $("#pane1 h5.head").hover(function(){
        $(this).next().show();
        },function(){
            $(this).next().hide();
            
        }
    
    );
}
);
```
toggle()方法

用于模拟鼠标连续点击事件

有几个函数，每次点击都重复对这几个函数的轮番依次调用

作用2：切换元素的可见状态

##### 事件冒泡
多个元素响应一个事件

两个嵌套的元素，并且绑定了一个事件：click，两个元素都会响应一个事件，从里到外

stopPropagation()方法：停止事件冒泡

preventDefault()方法：阻止元素的默认行为

###### 移除事件

```
$("#deAll").click(function(){
    $("#btn").unbind("click");
}
);
```
unbind()方法

第一个参数是事件类型，第二个参数是将要移除的函数

需要为匿名处理函数指定一个变量
```
$("#delTwo").click(function(){
    $("#btn").unbind("click",myFun2);//删除绑定函数2
}
);
```
one()方法

只触发一次，随后就要解除绑定的情况，结构与bind的结构类似

trigger()方法：模拟用户的操作，例如在用户进入页面的时候，触发click方法，不需要用户   去主动 点击


##### 自定义动画

animate()方法

语法结构：animate(params,speed,callback)

- params:一个包含样式属性及值的映射
- speed：速度参数，可选
- 在完成动画时执行的动画，可选

































