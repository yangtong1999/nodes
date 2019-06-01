Vue下，数据与DOM已经被建立了关联，所有的东西都是响应式的，用控制台可以随时修改实例的值，上例子会相应的更新

**v-bind:title = "message"**

该指令的意思是将该元素节点的==title==特性与实例的==message==属性保持一致

**v-if：**

控制v-if的值为true或者false，来达到控制一个元素是否显示

**v-for指令**

绑定数组的数据来渲染一个项目列表

v-on指令可以添加一个事件监听器，通过它调用在Vue中定义的方法


```
<button v-on:click = "ass">点击哈哈<button>
var App5 = new Vue({
    el:'#app-5',
    data:{
      message:"HEllo Vue.js"
    },
    methods:{
        ass:function(){
            alert("hello");
        }
    }
});
```
**v-model指令**

轻松实现表单输入和应用状态之间的双向绑定

Vue注册组件：


```
Vue.component('todo-item',{
props:['todo'],
 template:'<li>{{todo.text}}</li>'
})
```

