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
class App extends React.Component { // 可以把所有组件的东西写进这个类里面
	render() {
		return <h1>宝可梦</h1>;
	}
}
root.render(<App />);// App这里是类组件
```
如果return的是个大括号，意味着返回的是一个js对象，js没有直接在里面写html的语法。
```js
class App extends React.Component { // 可以把所有组件的东西写进这个类里面
	render() {
		return (
			<div> //外面必须有一个爸爸，即div把下面这些标签包裹起来
				<h1>宝可梦</h1>
				<input type="search" />
			</div>
		)
	}
}
```
jsx不止写html，还可以写js
```js
const pockmons = ["皮卡丘","杰尼龟","小火龙"] // 数组要写在类里面，又因为在初始化就要有，所以要写在constructor里
class App extends React.Component {
	render() {
		return (
			<div>
				<h1>宝可梦</h1>
				<input type="search" />
				<ul> /* 一个个写标签不太现实
				        <html>{插值表达式}</html>
				        */
					<li>{ pokemons[0] }</li>
					<li>{ pokemons[1] }</li>
					<li>{ pokemons[2] }</li>
					// 替换方案
					{
						pokemons.map( pokemon => <li>{ pokemon }</li> )
					}
				</ul>
			</div>
		)
	}
}
```
替换方案
```js
class App extends React.Component {
	constructor() {
		super();
		this.state /*对象*/ = { // state对象里可以定义各种状态了。
			pokemons: ["皮卡丘","杰尼龟","小火龙"],// 初始化的状态值
		}
	}
	render() {
		return (
			<div>
				<h1>宝可梦</h1>
				<input type="search" />
				<ul>/* <html>{插值表达式}</html>
				        */
					{
						pokemons.map( pokemon => <li>{ pokemon }</li> )
					}
				</ul>
			</div>
		)
	}
}
```
> - map里面li是后来引用的，页面从静态变成动态的了，即存在状态。数组的内容放在react状态里，可以动态进行操作，需要定义状态值。
> - 

