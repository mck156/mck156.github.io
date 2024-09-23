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
			pokemons: ["皮卡丘","杰尼龟","小火龙"],// 初始化的状态值 可以不需要之前上面const定义
		}
	}
	componentDidMount() {
		// 用fetch获取api的数据
		fetch("https://pokeapi.co/api/v2/pokemon")
		.then(res => res.json()) // 把获取到的数据转化为json格式
		// .then(json => console.log(json.result)); 如果直接用赋值的方式来操作，那么可以替换为下面这条。但state里面改变了，页面却没有更新。
		/*.then(json => {
			this.state.pokemons = json.results;
			console.log(this.state)
		});*/
		.then(json => {
			this.setState({
				pokemons: json.results,
			});
			console.log(this.state);
		});
	}
	render() {
		return (
			<div>
				<h1>宝可梦</h1>
				<input type="search" />
				<ul>/* <html>{插值表达式}</html>
				        */
					{
						/*这里加上this.state*/
						this.state.pokemons.map( pokemon => <li>{ pokemon }</li> )
					}
				</ul>
			</div>
		)
	}
}
```
> - map里面li是后来引用的，页面从静态变成动态的了，即存在状态。数组的内容放在react状态里，可以动态进行操作，需要定义状态值。
> - 获取API数据放在这个数组中，什么时候把获取到的API呈现在页面里？先呈现外面的轮廓，再把外面获取回来的数据呈现在页面上，用户看不到先数据后轮廓的现象了。
> - componentDidMount是组件挂载完毕后再执行这个方法里面的内容
> - react特点，不会像以前那样频繁操作DOM，用直接赋值的方式改变对象属性，对象的内存位置还是没有改变。最简单就是创建一个新的对象。

