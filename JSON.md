##### 语法
Json的语法可以表示以下三种类型的值：

1.简单值；表示字符串，数值，布尔值和null，但是JSON不支持undefined这个特殊值

2.对象：表示的是一组无序的键值对儿

3.数组：有序的值得列表

###### 简单值
JSON字符串必须使用双引号(单引号会导致语法错误)

```
"Hello world"
```
###### 对象

```
//虽然有两个name属性，但是他们属于不同的对象，同一个对象不应该出现两个同名属性
{
    "name":"Nicholas",
    "age":29,
    "school":{
        "name":"M",
        "location":"MA"
    }
}

```
###### 数组

```
[25,"hi",true]
```

```
[
  {
      "title":"P",
      "authors":["N za"],
      "edition":3,
      "year":2011
  },
  {
      "title":"P",
      "authors":["N za"],
      "edition":2,
      "year":2009
  }

]
```
###### 解析与序列化
JSON两个方法：stringify()方法与parse()方法

分别用于将JavaScript对象序列化为JSON字符串和JSON字符串解析为原生JavaScript值

```
var book = {
    title:"P",
    authors:[
      "N za"
    ],
    edition:3,
    year:2011
};
var jsonText = JSON.stringify(book);
//此方法输出的字符串不包含任何空格字符或者缩进，所有的函数及原型程远都会被忽略
```

```
//将JSON字符串直接传递给JSON.parse()可以得到相应的JavaScript值
var bookcopy = JSON.parse(jsonText);
```
###### JSON.stringify()的两个参数
第一个参数是一个过滤器，可以是一个数组，也可以是一个函数

第二个参数是一个选项，表示是否在JSON字符串中保持缩进

###### 过滤结果

```
//第二个参数是一个数组的情况下
var book = {
    title:"P",
    authors:[
      "N za"
    ],
    edition:3,
    year:2011
};
var jsontext = JSON.stringify(book,["title","edition"]);
//两个属性与要序列化的对象的属性是相对的
```

第二个参数是一个函数的情况
```
var book = {
    title:"P",
    authors:[
      "N za"
    ],
    edition:3,
    year:2011
};

var jsontext = JSON.stringify(book,function(key,value){
    switch(key){
        case "authors":
        return value.join(".")
        
        case "year":
        return 5000
        
        case "edition":
        return undefined;
        
        default:
        return value;
    }
});

```
###### 字符串缩进
JSON.stringify()方法的第三个参数用于控制结果中的缩进和空白符

```
var jsonText = JSON.stringify(book,null,4);
//只要传入有效的控制缩进的参数值，结果字符串就会包括换行符
//缩进字符串最长不超过10个字符长
```
###### toJSON()方法
返回自身的JSON数据格式，可以为任何对象添加这个方法

```
var book = {
    title:"P",
    authors:[
      "N za"
    ],
    edition:3,
    year:2011，
    toJSON:function(){
        return this.title;
    }
};
var jsontext = JSON.stringify(book);
//在book对象上定义了一个toJSON()方法，该方法返回图书的书名。可以让此方法返回任何值，它都能正常的工作
```
###### 解析选项
JSON.parse()接收一个参数，参数是一个函数，成为还原函数




