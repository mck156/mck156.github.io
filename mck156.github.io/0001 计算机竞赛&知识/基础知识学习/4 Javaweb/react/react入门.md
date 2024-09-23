搜索框和列表
设置css，分成两个部分，即组件
把单独的html+css+js写在组件里，类似的功能复制组件代码。如果把html css js分开，这里需要复制一点那里复制一点就非常麻烦容易搞混。所有组件都可以归属于根组件。
```js
<script>
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<h1>宝可梦</h1>);
</script>
```
这样不加引号直接写，浏览器不认识
加个babel 把React写的代码转化成原生JS
```js
<script type="text/babel">
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<h1>宝可梦</h1>);
</script>
```
如果把所有代码写render很恶心，render方法是传一个组件，组件有名字。
创建组件：类组件和函数组件
```js
root.render(<App />);
```
