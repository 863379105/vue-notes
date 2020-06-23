# vue学习笔记（一）

## 1.开始一个vue的实例

- ###  通过script标签引入vue文件

```js
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

或者：

```js
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

- ### 在html中创建一个VUE实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
</head>
<body>
    <div id="app">
        
    </div>
    <script>
        var app = new Vue({
          el : '#app', //vue会自动查找相匹配的元素，将要渲染的模版挂载在该元素下
          template : `<div id="app">{{ message }}</div>`,
          data : {
          	message : 'hello world!'
        	}
        })
    </script>
</body>
</html>
```

- ### 浏览器渲染效果

![hello](/Users/lb/Desktop/Code_Space/notes/VUE学习笔记/images/hello.png)

## 2.new Vue()的几点总结：

- ### 关于"el":

  - ##### el是模版挂载的位置

  - ##### el : '#app', //vue会自动查找相匹配的元素，将要渲染的模版挂载在该元素下

- ### 关于"template":

  - ##### 如果实例化的时候，传入template，则在渲染的时候优先使用template中的模版进行挂载并渲染

  - ##### template中的模版将会替换el中的挂载对象，并渲染在页面中

  - ##### template的模版只允许有一个顶级根结点

  - ##### template的渲染顺序：template => Vdom => html

- ### 关于data

  - ##### 在data中声明的数据在Vue实例中都可以通过"{{ }}"进行读取

## 3.template 和 render()

	### 	template和render()都是用于渲染模版的，但两者有一定差异

  - ##### template的渲染顺序：template => Vdom => html

    ##### render()的渲染顺序：Vdom => html

    ##### 相比之下，render()的渲染效率更高，只通过两个步骤对试图进行渲染

		- ##### 相比于template，render()更接近Vue的底层实现，渲染速度更快，提供的方法也更为复杂，更为灵活

## 4.render()的使用

 - ##### 实例化一个Vue()对象

   ```js
   var app = new Vue({
     el : '#app',
     render : function(creatElement){
       return creatElement()
     },
     data : {
       message : 'hello world'
     }
   })
   ```

   

 - ##### createElement参数

   ```js
   // @returns {VNode}
   createElement(
     // {String | Object | Function}
     // 一个 HTML 标签名、组件选项对象，或者
     // resolve 了上述任何一种的一个 async 函数。必填项。
     'div',
   
     // {Object}
     // 一个与模板中 attribute 对应的数据对象。可选。
     {
       arrts:{ id : "app"}//可传入标签的一些属性
     },
   
     // {String | Array}
     // 子级虚拟节点 (VNodes)，由 `createElement()` 构建而成，
     // 也可以使用字符串来生成“文本虚拟节点”。可选。
     [
       '先写一些文字',
       createElement('h1', '一则头条'),
       createElement(MyComponent, {
         props: {
           someProp: 'foobar'
         }
       })
     ]
   )
   ```

   