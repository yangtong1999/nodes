#### 第三章
标识符：变量、函数、属性的名字、函数的参数
###### 严格模式
ECMScript5引入严格模式概念，ECMScript3中的一些不确定性为得到处理，某些 不安全行为也会抛出错误

```
//使用严格模式，在脚本顶部添加：
"use strict";
```
在函数内部省略var操作符会创建一个全局变量
###### null类型
null表示的是一个空对象指针，意在让保存对象的变量还没有真正保存对象，明确的让该变量保存为null

**永远不要测试某个特定的浮点数值**
###### isNaN()函数
这个函数会帮我们确定一个参数是否"不是数值",任何不能被转换为数值的值都会导致这个函数返回true

###### ParseInt()函数
处理整数，如果第一个字符不是数字符号或者负号的话，返回NaN，也就是说转化一个空字符串的话会返回NaN

```
var num1 = parseInt("1234blue");//1234
var num2 = parseInt("22.5");//22
//指定基数
var num1 = parseInt("10",2);//2 二进制解析
var num2 = parseInt("10",8);//8 八进制解析
```
###### toString()方法
将一个值转化为字符串

```
var age = 11;
var sgeString = age.toString();//字符串"11"
//指定基数
var num = 10;
alert(num.toStrng(2));//"10"
```
###### Object类型
对象可以通过执行new操作符后跟要创建的对象类型名称来创建
###### 操作符
null与undefined是相等的，作用不同

逗号操作符：用于赋值，返回表达式的最后一项


```
var num = (5,5,4,3,0);//num的值为0
```
###### label语句
在代码中添加标签，将来由break，continue调用，与for循环搭配使用

#### 第四章
基本类型值：简单的数据段，按值访问，可以操作保存在变量中的实际的值

基本类型：Undefined，Null，Boolean，Number，String

引用类型值：多个对象构成的对象

**不能给基本类型的值添加属性**

```
var name = "N";
name.age = 7;
alert(name.age);//undefined
```
###### 复制变量值

```
//复制基本类型的值
var num = 5;
var num2 = num1;
//两个num中的值完全独立，一个是另一个副本，两者参与任何的操作不受影响

//复制引用类型的值
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "N";
alert(obj2.name);//"N"
//变量obj1保存了一个对象的实例，然后值被复制过去，也就是说两者指向的是同一个对象

```
###### 传递参数
**所有函数的参数都是按值传递的**


```
function addTen(num){
    num += 10；
    return num；
}
var count = 20;
var result = addTen(count);
alert(count);//20 没有变化
alert(result);//30
//餐宿按值传递，num和count互不认识，他们仅仅是有相同的值
```

###### typeof 操作符
确定一个变量是字符串、数值、布尔值还是undefined的最佳工具，
如果变量的值是一个对象(mew Object())还是null，typeof操作符将会返回"object"

```
var n = null;
var o = new Object();
alert(typeof o);//object
alert(typeof n);//object
```
###### instanceof操作符(检测引用类型的对象的类型)

```
alert(person instanceof Object);//变量person是object吗？
```
###### 执行环境及作用域
作用域链：保证对执行环境有权访问的所有变量和函数的有序访问

活动对象最开始只包括一个变量，即arguments对象，标识符解析沿作用域链一级一级搜索标识符的过程

###### JavaScript没有块级作用域
其他类c语言中，由花括号括起的代码都有自己的作用域，但是Js没有

Js中，if语句中的变量声明会将变量添加到当前的执行环境中

```
if(true){
    var color = "blue";
}
alert(color);
```
for语句创建的变量i即使在for循环执行结束后，也会依旧存在于循环外部的执行环境中

```
for(var i = 0;i < 10;i++){
    doSomething(i);
}
```
**包含引用类型的变量实际上包含的不是对象本身，而是一个指向该对象的指针**
#### 第五章
###### Object类型
创建Object类型的两种方法

```
//第一种
var person = new Object();
person.name = "Nicholas";
person.age = 29;
//第二种
var person(){
    name:"Nicholas",
    age:29
};
//使用对象字面量语法时，如果留其花括号，可以定义只包含默认属性和方法的对象
var person{};
//与new Object（）相同
```
push()方法

```
//push方法为数组添加值
var colors = new Array();
var count = colors.push("red","green");
```
pop()方法

```
var item = colors.pop();
alert(item);
/*数组末尾移除最后一项，减少数组的长度，返回移除的值*/
```
shift()方法从数组前面取得一个值并返回该项

unshift()方法与shift()方法相反，他可以在数组前端添加任意个项并且返回新数组的长度

比较函数

```
function compare(value1,value2){
    return value2 - value1;
}
var values = [0,1,5,10,15];
values.sort(compare);
alert(values);
```
slice()方法

基于当前数组中的一项或者多项创建一个新数组，接受两个参数，返回项的起始位置和结束位置

```
var colors = ["red","green","blue","yellow","purple"];
var colors2 = colors.slice(1,4);
alert(colors2);//green,blue,yellow,purple
//不会影响原始数组
```
splice()方法 最强大的数组方法

```
var colors = ["red","green","blue"];
//删除
var removed = colors.splice(0,1);//两个参数分别是删除的第一项和删除的最后一项
//插入
removed = colors.splice(1,0,"red","purple");//三个参数分别是起始位置，要删除的项数，要插入的项
//替换
removed = colors.splice(1,1,"red","purple");//插入两项，删除一项

```
indexOf()方法和lastIndexOf方法

两个方法都接受两个参数：要查找的项和表示查找起点位置的索引

indexOf方法从数组开头查找，lastIndexOf()方法从数组的末尾开始查找

Function类型
```
function sum(num1,num2){
    return sum1 + sum2;
};
alert(sum(10,10));//20

var anotherSum = sum;
alert(anotherSum(10,10));//20

sum = null;
alert(anotherSum(10,10));//20
//当把sum赋给anotherSum时，使用不带有圆括号的函数名是访问函数指针，而非调用函数，也就是说两者指向的是同一个函数而并非是赋值，当把sum清除的时候，anotherSum依旧可以正常调用
```
 call()或者apply方法可以扩充函数的作用域
 
 
```
window.color = "red";
var o = {color:"blue"};
function sayColor(){
    alert(this.color);
};
sayColor();//red

sayColor.call(this);//red
sayColor.call(window);//red
sayColor.call(o);//blue
```
###### 基本包装类型（Boolean、Number、String）
自动创建的基本包装类型的对象只存在于一行代码执行的瞬间，然后立即被销毁，意味着我们不能再运行时为基本类型值添加属性和方法。

```
var s1 = "some text";
s1.color = "red";
alert(s1.color);//undefined
//第二行代码试图为s1添加一个color属性，当第三行代码再次访问时，color不见了，原因是第二行创建的String对象在执行第三行代码的时候被销毁了，第三行重新创建自己属性，该对象没有颜色属性

```
min()和max()方法

确定一组数值中的最大值和最小值

```
//最大值
var max = Math.max(3,54,32,16);
alert(max);//54
//最小值
var min = Math.min(3,54,32,16);
alert(min);
```
几个舍入方法

Math.ceil()执行向上舍入(取大值)

Math.floor()执行向下舍入(取小值)

Math.round()执行标准舍入(四舍五入)

random()方法

返回一个0-1之间的一个随机数
#### 第六章
构造函数模式(缺点：针对每一个实例都会创建同一组新的方法)


```
function Person(name,age,job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function(){
        alert(this.name);
    }
}

var person1 = Person("Nicholas",29,"Software Engineer");
var person2 = Person("Greg",27,"Doctor");
//构造函数以大写字母开头
//person1和person2都保留了Person的一个不同的实例
```
hasOwnproperty()方法检测一个对象存在于实例中还是原型对象中，当给定属性存在于对象实例中时，返回true

in操作符和hasOwnproperty函数确定属性是否是原型对象中的属性

```
function hasPrototypeProperty(object,name){
    return !object.hasOwnproperty(name)&&(name in object);
}
```
Object.keys()方法可以接受一个对象作为参数，返回一个包含所有可枚举属性的字符串数组

```
var keys = Object.keys(Person.propertype);
alert(keys);
```
组合使用构造函数模式和原型模式，构造函数定义实例属性，原型模式定义方法以及共享的属性

```
function Person(name,age,job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.friend = ["S","C"];
}
Person.prototype{
    constructor:Person;
    sayName:function(){
        alert(this.name);
    }
}
var person1 = new Person("N",29,"S");
var person2 = new Person("G",27,"D");

person1.friend.push("V");
alert(person1.friends);//"S,C，V"
alert(person2.friends);//"S,C"
//两者的friends不相同，但是两者的sayName相同

```
组合继承(最常用的继承)

```
function SuperType(name){
    this.name = name;
    this.colors = ["red","blue","green"];
}

SuperType.propertype.sayName = function(){
    alert(this.name);
};
function SubType(name,age){
    //继承属性
    SuperType.call(this.name);
    this.age = age;
}

//继承方法
SubType.prototype = new SuperType();
SubType.prototype.constructor = subType;
SubType.prototype.sayAge = function(){
    alert(this.age);
};
var instance1 = new SubType("Nicholas",29);
instance1.colors.push("black");
alert(instance1.colors);//"red,blue,green,black"
instance1.sayName();//"Nicholas"
instance1.sayAge();//29

var instance2 = new SubType("G",7);
alert(instance2.colors);//"red,blue,green"
instance2.sayName();//"G"
instance1.sayAge();//7

```
#### 第七章
递归

```
  /*阶乘函数*/
function factorial(num){
    if(num <= 1){
        return 1;
    }else{
        return num*factorial(num - 1);
    }
}
```
arguments.callee 是一个指向正在执行的函数的指针(严格模式下不可以)

```
//用命名函数的方法完成递归，可以把函数赋值给另一个变量
var factorical = (function f(num){
    if (num <= 1){
        return 1;
    }else{
        return num*f(num - 1);
    }
});
```
###### 闭包

有权访问另一个函数作用域中的变量的函数

**闭包只取得包含函数中任何变量的最后一个值**

```
function createFunctions(){
    var result = new Array();
    for(var i=0;i < 10;i++){
        result[i] = function(){
            return i;
        }
    }
    rerurn result;
}
//每个函数都返回10
```
创建一个匿名函数强制让闭包函数符合预期

```
function createFunctions(){
    var result = new Array();
    for(var i=0;i <10;i++){
        result[i] = function(num){
            return function(){
                return num;
            };
        }(i);
    }
    return result;
}
```
关于this对象
this对象是针对于函数的执行环境绑定的：在全局对象中，this等于window，当函数被某个对象的方法调用的时候，this等于那个对象

匿名函数的执行具有全局性，this对象通常指向window


```
var name = "The Window";

var object = {
    name: "My Object",
    
    getNameFunc: function(){
        return function (){
            return this.name;
        }
    }
};

alert(object.getnameFunc()());//"The Window"
//每个函数在被调用的时候都会自动取得两个特殊变量：this和arguments。内部函数在搜索这两个变量的时候，只会搜索到其活动对象为止
```

```
//把外部作用域保存到一个闭包能够访问到的变量里，就可以让闭包访问该对象
var name = "The Window";
var object = {
    name:"My object",
    getNameFunction(){
        var that = this;
        return function(){
            return that.name;
        };
    }
};

alert(oblect.getNameobject()())://"My object"
```
用作块级作用域(私有作用域)的匿名函数语法如下

```
(function(){
    //这里是块级作用域
})();//前面将函数声明包含在一对圆括号中，表示它实际是一个函数表达式，紧随其后的圆括号会立即调用这个函数
```
无论在什么时候，临时需要一些变量，就可以使用私有作用域

```
function outputNumbers(count){
    (function(){
        for (var i = 0;i<count;i++){
            alert(i);
        }
        
    })();
    alert(i);//导致一个错误
}
```
###### 私有变量
私有变量包括函数的参数、局部变量、在函数内部定义的其他函数

有权访问私有变量和私有函数的公有方法叫做特权方法

1.在构造函数中定义特权方法

```
function(){
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false;
    }
    
    //特权方法
    this.publicMethod = function(){
        privateVeriable++;
        return privateFunction();
    };
}

```
###### 静态私有变量
在私有作用域中定义私有变量或者函数来创建特权方法


```
(function(){
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false;
    }
    
    //公有/特权方法
    MyObject.prototype.publicMethod = function(){
        privateVeriable++;
        return privateFunction();
    };
})();
```
这个模式特点：私有变量和私有函数都是由实例共享的，所有实例使用一个函数


```
(function(){
   var name ="";
   Person = function(value){
       name = value;
   };
   Person.prototype.getName = function(){
       return name;
   };
   Person.prototype.setName = function(value){
       name = value;
   };
})();

var person1 = new Person("N");
alert(person1.getName());//"N"
person1.setName("G");
alert(person1.getName());//"G"

var person2 = new Person("M");
alert(person1.getName());//"M"
alert(person2.getName());//"M"
//在这种模式下，变量name变成一个静态的、由所有实例共享的属性，在一个势力中使用setName()会影响所有的实例
```
###### 模块模式
为单例创建私有变量和方法

```
//以对象字面量的形式创建单例对象
var singleton = {
    name:value,
    method:funtion(){
        //这里是方法的代码
    }
};
```
模块模式的语法形式如下；

```
var singleton = function(){
    //私有变量和私有函数
    var privateVariable = 10;
    function(){
        return false;
    }
    //特权/公有方法和属性
    return  {
        publicProperty:type,
        publicMethod:function(){
            privateVariable++;
            return privateFunction();
        }
    };
}();
```
##### 第八章BOM
###### window对象
1.全局对象不能通过delete操作符删除，而直接在window对象上定义的属性可以

尝试访问未声明的变量会抛出错误，通过查询window对象，可以知道某个未声明的变量是否存在

```
//抛出错误，oldValue没有定义
var newValue = oldValue;
//不会抛出错误，因为这是一次属性查询
var newValue = window.oldvalue;
```
###### 间歇调用和超时调用
setTimeout()方法(超时调用)

两个参数：要执行的代码，和以毫秒数表示的时间(在执行前需要等待多少毫秒)


```
var timeout = setTimeout(function(){
    alert("Hello World!");
},1000);//一秒后显示一个警告框
//取消超时调用
clearTimeout(timeoutId);
```
**不建议以字符串为第一个参数，传递字符串可能导致性能损失**

间歇调用：指定的时间间隔重复的执行代码，直到间歇调用被取消或者页面被卸载

setInterval()方法

```
var num = 0;
var max = 10;
var intervalId = null;

function increamentNumber(){
    num++;
    
    //如果执行次数达到了max设定的值，则取消后面尚未执行的调用
    if(num ==max){
        cleearInterval(intervalId);
        alert(Done);
        
    }
}
intervalId = setInterval(increamentNumber,500);
```
最好不要使用间歇调用，可以使用超时调用模拟间歇调用来达到目的

```
var num = 0;
var max = 10;

function increatementNumber(){
    /*如果执行次数未达到max设定的值，则执行另一次超时调用*/
    if(num <max){
        setTimeout(increatementNumber,500);
    }else{
        alert("Done");
    }
}
setTimeout(increatementNumber,500);
```
###### alert()方法
接受一个字符串并把它显示给用户，包含指定的文本和
"OK"确定按钮，显示用户他们无法控制的消息
###### confirm()方法
显示OK 键和一个取消键，让用户决定是否执行给定的操作

```
if( confirm("Are you sure?") ){
    alert("I'm so glad you're sure");
}else{
    alert("I'm sorry to hear you're not sure");
}
```
###### prompt()方法
提示用户输入一些文本

除OK和Cancel按钮之外，显示一个文本输入区域

两个参数：要显示给用户的文本提示和文本输入区域的默认值
###### location对象
assign()方法


```
location.assign("链接")；
//立即打开新的URL并在浏览器的历史记录中生成一个记录
location.href("链接")和上面的方法等同
```
#### 第十章DOM
文档节点是每个节点的根节点(html元素)

html元素通过元素节点表示，特性节点通过特性节点表示

Js中所有的节点类型都继承自Node类型，所有的节点类型共享着相同的属性和基本方法

每个节点都有一个nodeType属性，用于表明节点的类型

 每个节点都有一个childNodes属性，保存一个NodeList属性

###### focus()方法
获得焦点


```
var buttons = document.getElementById("myButton");
buttons.focus();
```
不支持innerHTML的元素有：\<col\>、\<colgroup\>、\<head\>、\<html\>、\<table\>、\<tbody\>和\<tr\>
##### 表单脚本
###### 提交表单
type类型设置为"submit",用户单击提交按钮或图像按钮，就会提交表单


```
//通用提交按钮
<input type = "submit" value = "Submit">
//自定义提交按钮
<button type = "submit">Submit Form</button>
```
提交表单

```
var form = document.getElementById("myForm");
//提交表单
form.submit();
```
###### 重置表单

```
//通用重置按钮
<input type = "reset" value = "Reset Form">
```
每个表单都有elements属性，该属性是表单中所有表单元素(字段)的集合

```
var form = document.getElementById("myForm");
var colorFileds = form.elements["color"];
alert(colorFileds.length);//3
```
autofocus属性

在支持这个属性的浏览器中，只要设置这个属性，不用JavaScript就可以自动把焦点移动到相应字段


```
<input type = "text" autofocus>
```
###### 文本框脚本

```
//显示25个字符，但是不能超过50个字符
<input type ="text" size="25" maxlength="50">
```
\<textarea>元素始终会呈现一个多行文本框，要指定文本框的大小，可以使用rows和cols特性。

rows特性指定的是文本框的字符行数

cols指定的是文本框的字符列数


```
<textarea rows="25" cols="5">initival value<textarea>

```
###### 选择文本
在文本框获得焦点的时候选择其所有的文本

```
EventUtil.addHandler(textbox,"focus",function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    target.select();
});
```
必填字段

```
<input type = "text" name = "usename" required>
```
###### 错误处理
try-catch语句

处理异常的一种标准方式

```
try{
    //可能会导致错误的代码
}catch(error){
    //在错误发生时该怎么处理
}
```
例子：

```
try{
    window.someNonexistenFunction();
}catch(error){
    alert(error.message);
}
```
==只要代码中包含finally子句，那么无论是try还是catch语句中的语句都将被忽略==

 










