#### 1.1 Node.js特性
- 单线程
触发内部事件，通过非阻塞I/O,事件驱动，宏观并行。

好处：

减少了内存的开销，操作系统的内存换页。

坏处：

一个用户造成线程的崩溃，服务器就崩了。
- 非阻塞I/O
不会傻等I/O语句结束，而会执行后面的语句。




    小乐爱喝茶，废话不说，煮开水。
    出场人物：小乐，水壶两把（普通水壶，简称水壶；会响的水壶，简称响水壶）。
       1 小乐把水壶放到火上，立等水开。（同步阻塞）
         ——   小乐觉得自己有点傻
       2 小乐把水壶放到火上，去客厅看电视，时不时去厨房看看水开没有。（同步非阻塞）
         ——  小乐还是觉得自己有点傻，于是变高端了，买了把会响笛的那种水壶。水开之后，能大声发出呜呜~~~~的噪音。
       3 小乐把响水壶放到火上，立等水开。（异步阻塞）
         ——  小乐觉得这样傻等意义不大
       4 小乐把响水壶放到火上，去客厅看电视，水壶响之前不再去看它了，响了再去拿壶。（异步非阻塞）
         ——  小乐觉得自己聪明了。


  所谓同步异步，只是对于水壶而言。
     普通水壶，同步；响水壶，异步。
     虽然都能干活，但响水壶可以在自己完工之后，提示小乐水开了。这是普通水壶所不能及的。
     同步只能让调用者去轮询自己（情况2中），造成小乐效率的低下。

   所谓阻塞非阻塞，仅仅对于小乐而言。
    立等的小乐，阻塞；看电视的小乐，非阻塞。

    情况1和情况3中小乐就是阻塞的，媳妇喊他都不知道。

    虽然3中响水壶是异步的，可对于立等的小乐没有太大的意义。

    所以一般异步是配合非阻塞使用的，这样才能发挥异步的效用。
    
- 事件机制，事件环

不管新用户的I/O，还是老用户的I/O完成，都将以事件方式进入事件环，等待调度。

#### 并发（concurrency）和并行（parallellism）的区别：

1. 解释一：并行是指两个或者多个事件在同一时刻发生；而并发是指两个或多个事件在同一时间间隔发生。
1.  解释二：并行是在不同实体上的多个事件，并发是在同一实体上的多个事件。
1. 解释三：在一台处理器上“同时”处理多个任务，在多台处理器上同时处理多个任务。如hadoop分布式集群

==Node.js中所有的I/O都是异步的，回调函数套着回调函数。==

#### Node.js适合什么？
**Node.js适合于开发什么样的应用程序呢？**

善于I/O，不善于计算，因为Node.js最擅长的是任务调度，如果你的业务多度的CPU进行计算。实际上也相当于这个计算阻塞了这个单线程。

同时处理大量的并发的I/O，程序内部不需要进行非常复杂的处理的时候，Node.js非常合适，也适合于和web socket配合，开发长连接的实时交互程序。

*适合：*
- 用户表单搜集
- 考试系统
- 聊天室
- 图文直播
- 提供JSON的API（为前端的Augular提供）

缺少健壮性。

control+c 可以终止正在运行的node进程

本地写一个js文件，不能够直接运行，有了node，任何一个js文件都可以通过node

==node就是js一个执行环境==

node.js 没有web容器，不能把一个html放在一个文件夹让node.js运行

URL和真实的物理文件是没有关系的

node.js没有文件夹的概念

#### HTTP模块

```
//引用http模块
var http = require("http");

//创建一个服务器， 回调函数表示接到请求之后应该做的事情

var server = http.createServer(function(req,res){
   console.log("服务器接收到了请求"+req.url);
   res.end();
});

server.listen(3000,"127.0.0.1");
```
res.end里面必须是一个字符串

req.url 属性，表示用户的请求地址。

url.parse可以将一个完整的url地址分为很多部分

host 主机名  post 端口号 pathname 文件的路径不算问号  path 路径 算问号

url.parse()如果第二个参数是true，那么就可以将所有的查询变为对象。就可以直接打点得到这个参数。

fs.readdir(path,callback(err,files));files是个数组，会读取一个文件夹里面的所有文件。


##### 把异步语句变成同步语句

node.js语句是异步语句


```
fs.readdir("./album/",function(err,files){
var wenjianjia = [];
(function iterator(i){
   if(i==files.length){
       console.log(wenjianjia);
       renturn;
   }
    fs.stat("./album/"+files[i],function(err,stats){
        if(stats.isDirectory()){
            wenjianjia.push(files[i]);
        }
        iterator(i+1);
    })
})(0);
});
```

#### 5.静态资源管理文件（直接通过地址访问文件）

```
var http = require("http");
var url = require("url");
var fs = require("fs");

http.createServer(function(req,res){
    var pathname = url.parse(req.url).pathname;
    fs.readFile("./static"+pathname,function(err,data){
        if(err){
        fs.readFile("./static/404.html",function(err,data){
            res.writeHead(404,{"Content-type":"text/html;charset = UTF8"});
            res.end(data);
        });
        return;
        }
        res.end(data);
    });
}).listen(3000,"127.0.0.1");
```
### 4.模块
js与js之间有两种合作的模式：

- 某一个js文件中，提供了函数，共别人使用，只需要暴露函数就行了

```
exports.msg = msg;
```
- 某一个js文件中，描述了一个类。 
```
module.exports = People;
```
> 如果没有写./，那么默认是从node_modules文件夹中获取的。


==node_modules文件夹并不一定在同级目录下，在任何直接的祖先级目录中都可以==，甚至可以放到NODE_PATH环境变量的文件夹里面。

*可以使用文件夹直接去管理模块*

每一个 模块文件夹都写一个package.json文件，这个文件的名字不能改，node将会自动读取里面的配置，有一个main项，就是入口文件：

```
{
    "name":"yangtong",
    "version":"1.0.1",
    "main":"app.js"
}
```
package.json文件，要放到模块文件夹的根目录里面

npm的主要职责就是安装开发包和管理依赖项

模块就是一些功能的封装，经常使用的功能，都有人封装成了模块，并且放到了社区，供别人下载，这个社区就叫做npm。

http://www.npmjs.com/ 这是npm的网站

去社区找需求，找api。

==require()别的js文件的时候，将执行那个js文件，fs是从命令提示符找到别人的==

require()中的路径，是从当前的js文件出发，找到别人。

所以，桌面上有一个a.js文件，test文件夹里面有一个b.js,c.js,1.txt

a引用b：

```
var b = require("./test/b.js");
```
b引用c:

```
var b = require("./c.js");
```
fs等其他的模块用到路径的时候，都是相对于cmd光标所在的位置。

所以，如果test文件夹有一个1.txt文件，那么在b.js里面想要读取这个文件的话，推荐使用绝对路径:


```
fs.readFile(_dirname +"/1.txt",function(err,data){
    if(err){
        throw err;
    }
    console.log(data.toString());
});
```
### 5.post请求

```
var alldata = "";
//下面是post请求的接收的一个公式
//node为了追求极致，它是一小段一小段接收的。
//接收了一小段，可能就给别人服务了，防止一个过大的表单阻塞进程。
req.addListener("data",function(chunk){
    alldata += chunk;
    
});
//全部传输完毕
req.addListener("end",function(){
    console.log(alldata.toString());
    res.end("success");
});
```
原生写Post处理，比较的复杂，要写两个监听，文件上传业务比较难写，所以，用第三方模块formidable。


只要涉及文件上传，form标签要加一个属性：

```
<form action = "http://127.0.0.1/dopost" method = "post" enctype = "multipart/form-data">
```

### ejs模板引擎
是npm第三方的包

后台的模板引擎

### Express 框架


Express是后台的一个node框架，所以和jquery、bootstrap不是一个东西。

expressjs.com.cn 中文的官网

### express整体感知：
1. 路由能力
2. 静态文件伺服能力
3. 与模板引擎的配合，清晰直观。

### 路由
用get请求的时候，做什么事情
```
app.get("网址",function(req,res){

});
```
用post请求的时候，做什么事情：

```
app.post("网址",function(req,res){

});
```

处理这个网址的任何请求的时候，请用all：

```
app.all("网址",function( req,res){
    
})
```
==这里的网址，不分大小写==

==所有的GET参数，？后面的都会被忽略，锚点也会被忽略==

### 中间件

如果，我的get、post回调函数中，没有next参数，那么就匹配第一个路由，就不会往下匹配了。如果，想往下匹配的话，那么需要写next()
<!--![image](https://note.youdao.com/yws/api/personal/file/WEBb7c0e95af911bfbe9fbccc5651161e22?method=download&shareKey=485f977937fe382cd3f9d8d88fcd6ee6)-->
这种情况是要匹配两次的，但是两次都请求成功会报错。

解决方法一：express所有路由(中间件)的顺序至关重要，匹配上第一个就不会往下匹配了。具体的往上写，抽象的往下写。

解决方法二：

```
if(检索数据库){
    console.log("1");
    res.send("用户信息")；
}else{
    next();
}
```
所谓的中间件，也就是get、post这些东西，中间件讲究顺序，匹配上第一个之后就不会往下匹配了，next函数才能继续往下匹配。

**app.use()方法为什么会出现？**

get、post请求的只是匹配的，相对来说比较绝对，use方法：app.use('/apple',...),它将会匹配的是"/apple" "/apple/images","/apple/images/news"等等。

app.use也是一个中间件，他的网址不是精确匹配的，而是由小文件夹扩展的。

不写路径的时候，实际上相当于"/" ,就是所有网址


#### 内容渲染

大多数情况下，渲染内容用res.render(),将会根据views中的模板文件进行渲染。

如果想写一个快速测试的页面，当然可以使用res.send();这个函数将会根据内容自动帮我们设置Content-Type头部和200状态码。

如果想使用不同的状态码可以：

```
res.status(404).send("sorry,we cannot find that!");

```
如果想使用不同的Content-Type类型，可以：


```
res.set('Content-Type','text/html');
```

send只能用一次

#### Get请求和post请求参数

get请求的参数在url里面，在原生node里面，需要使用url模块来识别参数字符串，在express中，直接使用req.query对象。

post请求在express中不能够直接获得，必须使用body-parser模块，使用后，将可以直接使用req.body得到参数，如果表单中含有文件上传，那么还是需要使用formidale模块。


```
//设置模板引擎
app.set("view engine","ejs");
```

```
app.use(express.static("./public"));
```


node的编程思维，所有的东西都是异步的，内层函数不是return回来东西，而是调用高层函数提供的回调函数，把数据当做回调函数的参数使用。