#### AJAX
AJAX = Asynchronous JavaScript and XML(异步的JavaScript和XML)

**优点：在不重新加载页面的情况下，可以与服务器交换数据并更新部分网页内容**
##### 创建XMLHttpRequest对象
XMLHttpRequest对象：用于在后台与服务器交换数据，是AJAX的基础

创建XMLHttpRequest对象的语法：

```
//现代浏览器均内建XMLHttpRequest对象
variable = XMLHttpRequest();
//老版本的浏览器(IE5和IE6)，使用ActiveX对象：
variable = new ActiveXObject("Microsoft.XMLHTTP");
```
为了应对所有的现代浏览器，包括IE5和IE6，检查浏览器是否支持XMLHttpRequest对象，不支持的话，创建ActiveXObject：

```
var xmlhttp;
if(window.XMLHttpRequest)
{
    //IE7+,FIrefox,CHrome,Opera,Safari浏览器执行代码
    xmlhttp = new XMLHttpRequest();
}else{
    //IE5和IE6执行代码
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
```
###### 向服务器发送请求
将请求发送到服务器，使用XMLHttpRequest对象的open()和send()方法：

```
xmlhttp.open("GET","ajax_info.txt",true);
xmlhttp.send();
```
**open()方法：**

规定请求的类型，URL以及是否异步处理请求

method:请求的类型：GET和POST

URL：文件在服务器上的位置

async：true(异步)或false(同步)

**send(string)方法**

string:仅用于POST请求

**GET还是POST？**

GET相对于POST方法更简单也更快，并且在大部分的事件下都能用

在以下情况中使用POST请求：

1. 无法使用缓存文件(更新服务器上面的文件或者数据库)
1. 向服务器发送大量的请求(POST没有数据量的限制)
1. 发送包含未知字符的用户输入的时候

**异步**

open方法的URL参数是服务器上的文件的地址，可以是任何类型的文件

通过AJAX，JavaScript无需等待服务器的响应，而是：

- 在等待服务器响应的时候执行其他的脚本
- 当响应就绪之后对响应进行处理

**Asnyc=true**

当Asnyc=true时，请规定在响应处于onreadystatechange事件中的就绪状态下执行的函数：

```
xmlhttp.onreadystatechange = function(){
    if(xmlhttp.readyState==4&&xmlhttp.status ==200){
        document.getElementById("myDIV").innerHTML = xmlreponseText;
    }
}
xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
xmlhttp.send();
```
**Asnyc=false**

不推荐使用anysc=false，对于一些小的请求是可以的

**当使用async = false 时，请不要编写onreadystatechange函数，把代码放在send()语句后面即可**

```
xmlhttp.open("GET","/try/ajax/ajax_info.txt",false);
xmlhttp.send();
document.getElementById('MyDiv').innerHTML = xmlhttp.responseText;
```
**服务器响应**

XMlHttpRequest对象的reponseText或reponseXML属性


属性 | 描述
---|---
reponseText | 获得字符串形式的响应数据
reponseXML| 获得XML形式的响应数据


```
<html>
<head>
<meta charset="utf-8">
<script>
function loadXMLDoc()
{
  var xmlhttp;
  var txt,x,i;
  if (window.XMLHttpRequest)
  {
    // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
  }
  else
  {
    // IE6, IE5 浏览器执行代码
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
  xmlhttp.onreadystatechange=function()
  {
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
      xmlDoc=xmlhttp.responseXML;
      txt="";
      x=xmlDoc.getElementsByTagName("ARTIST");
      for (i=0;i<x.length;i++)
      {
        txt=txt + x[i].childNodes[0].nodeValue + "<br>";
      }
      document.getElementById("myDiv").innerHTML=txt;
    }
  }
  xmlhttp.open("GET","cd_catalog.xml",true);
  xmlhttp.send();
}
</script>
</head>

<body>

<h2>我收藏的 CD :</h2>
<div id="myDiv"></div>
<button type="button" onclick="loadXMLDoc()">获取我的 CD</button>
 
</body>
</html>
```
**onreadystatechange事件**

当请求被发送到服务器的时候，我们需要执行一些基于响应的业务。

每当readyState改变时，就会触发onreadystatechange事件，readyState属性存有XMLHttpRequest的状态信息

下面是XMLHttprequest对象的三个重要的属性：

属性 | 描述
---|---
onreadystatechange | 存储函数(或者函数名)，readyState属性改变的时候，触发这个函数
readyState| 存有XMLHttpRequest的状态，0~4发生变化：0：请求没有初始化  1：服务器连接已建立  2：请求已接收  3.请求处理中 4：请求已完成，且响应已就绪
status|200"OK" ,  404"为找到页面"

```
//当readyState = =4且状态为200时，表明响应已就绪
xmlhttp.onreadystatechange = function(){
    if(xmlhttp.readyState==&&xmlhttp.status ==200){
        document.getElementById("myDiv").innerHTML = xmlhttp.reponseText;
    }
}
```
一个实例：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script>
function showCustomer(str)
{
  var xmlhttp;    
  if (str=="")
  {
    document.getElementById("txtHint").innerHTML="";
    return;
  }
  if (window.XMLHttpRequest)
  {
    // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
  }
  else
  {
    // IE6, IE5 浏览器执行代码
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
  xmlhttp.onreadystatechange=function()
  {
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
      document.getElementById("txtHint").innerHTML=xmlhttp.responseText;
    }
  }
  xmlhttp.open("GET","/try/ajax/getcustomer.php?q="+str,true);
  xmlhttp.send();
}
</script>
</head>
<body>

<form action=""> 
<select name="customers" onchange="showCustomer(this.value)" style="font-family:Verdana, Arial, Helvetica, sans-serif;">
<option value="APPLE">Apple Computer, Inc.</option>
<option value="BAIDU ">BAIDU, Inc</option>
<option value="Canon">Canon USA, Inc.</option>
<option value="Google">Google, Inc.</option>
<option value="Nokia">Nokia Corporation</option>
<option value="SONY">Sony Corporation of America</option>
</select>
</form>
<br>
<div id="txtHint">客户信息将显示在这...</div>

</body>
</html>
```
当用户在上面的下拉列表中选择某个客户时，会执行名为 "showCustomer()" 的函数。该函数由 "onchange" 事件触发：

showCustomer() 函数执行以下任务：
- 检查是否已选择某个客户
- 创建 XMLHttpRequest 对象
- 当服务器响应就绪时执行所创建的函数
- 把请求发送到服务器上的文件
- 请注意我们向 URL 添加了一个参数 q （带有输入域中的内容）

由上面的 JavaScript 调用的服务器页面是 PHP 文件，名为 "getcustomer.php"。


"getcustomer.php" 中的源代码负责对数据库进行查询，然后用 HTML 表格返回结果



