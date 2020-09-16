

### 基础篇

#### 1、简单指令的使用

* mustache 显示文本

* v-once 只显示第一的文本，不支持响应

* v-pre 不解析，原封不动的显示html标签里的内容

* v-html 解析服务器返回的带有html标签的内容

* v-cloak 使得在js没有解析前不显示内容

  

#### 2、v-bind 动态绑定

* 1、基本使用

  * 用法  v-bind：src = “imgURL”
  * 语法糖用法（简写） ：src = “imgURL”

* 2、v-bind 动态绑定class  对象语法

  *  用法 v-bind:class='{类名：boolean，类名：boolean}'  
  * e.g   v-bind:class='{active：isactive}'

  ```js
  {data:{
  	active:true
  }}
  ```

* 3、v-bind 动态绑定class  数组语法

  * e.g   v-bind:class='[active]'

  * 或者 v-bind:class='getClass()'

    ```js
    {
    	data:{
    		active:abcdef
    	}
    	methods:{
    		getClass:function(){
    			return this.active
           }
    	}
    }
    ```

* 4、v-bind 动态绑定style语法

  *  对象语法 

  * 用法 v-bind:style='{属性名：属性值}'

    ```js
    {data:{
    	finalSize: 100
    
    }}
    ```

  * 数组语法

  * 用法 v-bind:style='[basecolor ,baseSize]'

    ```js
    {data:{
    	basecolor: 'color:red',
    	baseSize: 'font-size:100px',
    
    }}
    ```



#### 3、computed计算属性

* 用法：对数据进行处理后再显示

  e.g 

  ```
  <h2>总价格：{{fullPrice}}</h2>
  {
  	data:{
  		books:[
              {id:110,name:'数据结构',price:120},
              {id:111,name:'计算机网络',price:20},
              {id:112,name:'数据库原理',price:1120},
            ],
  
  	}
  	 computed:{
            fullPrice:function(){
              let result = 0;
              for (let item of this.books){
                result+=item.price;
              }
              return result;
         
            }
          }
  }
  ```

* setter和getter

  一个完整的计算属性如下

  e.g

  ```
  {
  	computed:{
            fullPrice:{
           	set:function(){
           	
           	}
              get:function(){
              
              }
            }
          }
  }
  ```

  但在实际生活中，我们基本上不会用set属性，因此可以简写为

  ```
  {
  	computed:{
  		fullPrice:function(){
              
            }
  	}
  }
  ```

* 计算属性和methods的比较

  * 计算属性有一个缓冲，如果数据没有改变，则直接从缓存中读取

  * methods每次都是重新调用，降低了性能

    

#### 4、v-on

* 用法：v-on:click  或者 @click（语法糖）

* 1、v-on 后面的函数不加括号

  ```
  <button @click="abc"></button>
  {
  	methods：{
  		abc（）{
  			console.log("abc");
  		}
  	}
  }
  ```

* 2、v-on后面跟上括号

  * 1 ，同上
  * 2，输出浏览器产生的event对象
  * 3，输出传入的参数

  ```
  1、<button @click="abc（）"></button>
  2、<button @click="abd"></button>
  3、<button @click="abd（hello）"></button>
  {
  	methods：{
  		abc（）{
  			console.log("abc");
  		}
  		abd（argu）{
  			console.log(argu);
  		}
  	}
  }
  ```

* 3、v-on需要参数并且要求输出浏览器的event对象

  ```
  <button @click="abd（hello，$event）"></button>
  ```

#### 5、v-if、v-else、v-else-if

#### 6、v-show，只 展示一次

#### 7、v-for

* v-for绑定key

#### 8、v-model，双向绑定

* v-model与radio
* v-model与checkbox
* v-model与select
* 值绑定
* 修饰符
  * lazy，在失去焦点后绑定
  * number，数字类型
  * trim，去除首尾空格

### 高阶篇

#### 1、组件化

* 创建组件构造器，vue.extend()

  ```
  const ConP = Vue.extend({
  	template:`
  		<div>
  			<p></p>
  		</div>`
  })
  ```

* 注册组件，vue.component()

  ```
  Vue.component('cpn'(标签),ConP(构造器))
  ```

* 使用组件

#### 2、局部组件和全局组件

* 局部组件的注册

  ```
  {
  	methods：{
  		abc（）{
  			console.log("abc");
  		}
  		abd（argu）{
  			console.log(argu);
  		}
  	},
  	components:{
  		//标签名：标签
  		cpn:ConP
  	}
  }
  ```

  

#### 3、父组件和子组件

* 在一个组件的构造里注册另一个组件

  ```
  const ConP = Vue.extend({
  	template:`
  		<div>
  			<p></p>
  		</div>`，
  	components：{
  		cnp：ConP
  	}
  })
  ```

  

#### 4、语法糖形式

* ```
  Vue.conponent("cpn",{
  	template:`
  		<div>
  			<p></p>
  		</div>`
  })
  ```



#### 5、模板分离

* 1、script

  ```
  <script type="text-tempalte" id="mycpn">
  	<div>
  		<p></p>
  	</div>
  </script>
  
  Vue.conponent("cpn",{
  	template:"#mycpn"
  })
  ```

  

* 2、template

  ```
  <template id="mycpn">
  	<div>
  		<p></p>
  	</div>
  </template>
  
  Vue.conponent("cpn",{
  	template:"#mycpn"
  })
  ```



#### 6、组件中的data必须是一个函数

* ```
  Vue.conponent("cpn",{
  	template:"#mycpn",
  	data(){
  		return:{
  			counter:0
  		}
  	}
  })
  ```

  

#### 7、父子组件通信

* 父传子，pops

  ```
  <div class="" id="app">
  	//绑定父元素
      <cpn :cmovies="movies" :cmessage="message"></cpn>
    </div>
    //定义模板
    <template id="cpn">
      <div>
        <p>{{cmessage}}</p>
        <h2>{{cmovies}}</h2>
      </div>
    </template>
    
    <script>
  
        const cpn = {
          template:'#cpn',
          //数组
          props:['cmovies','cmessage'],
          //对象
          props：{
          	//要求传给cmovies的参数必须是数组
          	cmovies:Array
          	
          	//提供默认值
          	cmovies:{
          		type:String,
          		default:'aaaaa',
          		//必传参数
          		requried:true
          	}
          }
          data(){
            return{
  
            }
          },
          methods:{}
        }
        
        const app = new Vue({
          el: "#app",
          data: {
            message: "This is message",
            movies: ['海绵宝宝','三个白痴','肖申克的救赎','何以为家','养家之人','我和我的祖国'],
            currentIndex: 0
          },
          methods:{
            onclick:function(index){
              this.currentIndex=index;
            }
  
          },
          components:{
            cpn
          }
        });
      </script>
  ```

  

* 子传父，$event

  ```
   <div class="" id="app">
        <cpn @btnclick="itemclick"></cpn>
      </div>
  
      <template id="cpn">
        <div>
          <ul>
            <li v-for="item in categories" @click="btnclick(item)">
              <button>{{item.name}}</button>
            </li>
          </ul>
        </div>
      </template>
      <script>
        //子组件
        const cpn = {
          template: "#cpn",
          props: ["cmovies", "cmessage"],
          data() {
            return {
              categories: [
                { id: "a", name: "海绵宝宝" },
                { id: "b", name: "三个白痴" },
                { id: "c", name: "何以为家" },
                { id: "d", name: "养家之人" },
              ],
            };
          },
          methods: {
            btnclick(item) {
              //发射一个事件,btnclick是事件的名称
              this.$emit("btnclick",item);
            },
          },
        };
  
        //父组件
        const app = new Vue({
          el: "#app",
          data: {
          },
          methods: {
            itemclick(item){
              console.log("123",item);
            }
          },
          components: {
            cpn,
          },
        });
      </script>
  ```


* 父访问子

  * $child

  * $ref

    ```
    <cpn ref="aaa"></cpn>
    {
    	getInfo(){
    		this.$refs.aaa.属性
    	}
    }
    ```

* 子访问父
  
  * $.parent
* 访问根
  
  * $.root

#### 8、v-slot(slot,slot-scope)

* 替换组件中的内容
* 具名插槽<slot name="aa"></slot>
* 作用域插槽，父组件获取子组件的内容

### webpack的使用

#### 1、安装和介绍

* 模块化打包工具
* 安装命令：npm install webpack --save

#### 2、基本使用

* webpack 入口文件 打包好的文件

  e.g webpack index.js dist/bundle.js

#### 3、配置

* 配置webpack.config.js

  ```
  const path = require("path");  //获取文件的目录
  
  module.exports = {
    entry:'./index.js',  //指定入口文件，当前目录下的index.js
    //指定打包后的文件，在当前目录下的dist文件生成bundle.js
    output:{
      path: path.resolve(__dirname,"dist"),
      filename:'bundle.js',
    },
  }    
  ```

* 配置package.json

  * 当前项目需要用node相关

    ```
    npm init
    ```

  * 自动生成文件

    ```
    {
      "name": "meetwebpack",
      "version": "1.0.0",
      "description": "",
      "main": "./js/index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "build": "webpack"  //配置，以后打包用命令 npm run build
      },
      "author": "",
    }
    ```

#### 4、使用css

#### 5、使用less

#### 6、添加图片

* 添加url-loader，file-loader
* 图片配置的命名
  * name:'img/[name].[hash:8].[ext]'

#### 7、ES6转为ES5

#### 8、使用vue的配置

* 安装uve

  ```
  npm install --save vue
  ```

* 改为runtime-complier

  ```
  module.exports = {
    entry:'./index.js',  //指定入口文件，当前目录下的index.js
    //指定打包后的文件，在当前目录下的dist文件生成bundle.js
    output:{
      path: path.resolve(__dirname,"dist"),
      filename:'bundle.js',
    },
    resolve:{
    	alias：{
    	'vue$':"vue/dist/vue.esm.js"
    }
    }
  }  
  ```

#### 9、打包

* 安装vue-loader

#### 10、plugin

* 添加版权信息

  ```
  plugins:[
  	new webpack.BannerPlugin("最终版权归")
  ]
  ```

* 安装html-webpack-plugin

  * 解决发布的文件夹中没有index.html
  * 可以将打包好的js添加到body中

* 安装js的压缩插件

  ```
  npm install uglifyjs-webpack-plugin --save-dev
  ```



#### 11、搭建本地服务器

* npm install webpack-dev-server --save-dev

* 配置

  ```
  devServer:{
  	contentBase:'\dist',  //指定服务的文件夹  
  	inline: true,  // 即时刷新
  }
  
  ```

  ```
  “dev”:"webpack-dev-server --open"
  ```

备注：vscode里面live server

#### 12、webpack配置文件分离

* npm install webpack-merge --save-dev

* 将配置文件分为，base.config.js，pro.config.js，dev.config.js

  ```
  const uglifyjsWebpackPlugin = reuqire("uglifyjs-webpack-plugin")
  const webpackMerge = require("webback-merge")
  const baseConfig = require("base.config")
  module.exports = webpackMerge(baseconfig,{
  	plugins:[
  		new uglifyjsWebpackPlugin();
  	]
  })
  ```

  ```
  //指定配置文件，pack.json
  {
  	"build": "webpack --config build/pro.config.js" //后面为配置文件的地址
  }
  ```



### 箭头函数的使用

#### 1、基本使用

* （）=>{ return }

* 两个参数

  ```
  const sum = (num1,num2) => {
  	return num1+num2
  }
  ```

* 一个参数

  ```
  const mul = num1 =>{
  	return num1*num2
  }
  ```

* 函数体中只有一行代码

  ```
  const sum = num1 => num1+num1
  ```

#### 2、this的指向

* 在外层作用域中，一层层查找，直到有this的的定义

### 前端历史

#### 1、后端渲染、后端路由

* 后端渲染：直接由服务器渲染页面返回给浏览器展示
* 后断路由：存储url和页面的映射表

#### 2、前后端分离

* 发送请求后，到静态资源服务器下载html+css+js，由ajax通过api向服务器请求数据，再由js渲染

#### 3、前端路由

* 只有下载所有的html+css+js（只有一套），当url发生改变的时候，根据前端路由的映射表去分离之前下载的资源

### 浏览器的返回和前进

#### 1、hash

* location.hash = "aaa"

#### 2、H5 中的history

* history.pushState({},'','home')
* history.back()
* history.forward()
* histroy.go()

### vue CLI

#### 1、安装

```
npm install @vue/cli -g
```

#### 2、使用

* 拉取vue cli 2模板

  ```
  npm install -g @vue/cli-init
  ```

* vue cli2 创建项目

  ```
  vue init webpack my-project
  ```

* vue cli3 创建项目

  ```
  vue create hello-world
  ```


* runtime-only和runtim+complier的区别

  * rumtime+complier:template->ast(抽象语法数)->render->vdom(虚拟dom)->UI
  * runtime-only:render->vdom(虚拟dom)->UI

* render的使用

  ```	
  render:function (createElement){
  	//普通用法：createElement('标签',{标签属性},[内容])
  	return createElement('h2',{class:'box'},['Hello World'])
  	
  	//传入组件
  	return creatElement(cpn)
  }
  ```

### vue-router的基本使用

* router-link

  * to="/home"  转到首页
  * tag="button" 渲染成button
  * replace 不允许浏览器的返回和前进
  * active-class=“active”   将点击时自动添加的class（router-link-active）改名为active

* router-view

* 重定向 redirect

* 更改模式 mode：‘history’

* 路由代码跳转

  ```
  {
  	methods:{
  		btn(){
  			this.$router.push('/home')
  		}
  	}
  }
  ```

* 动态路由

  * 为网页最后面拼接上用户id

    ```
    path: '/user/:abc'
    ```

  * 显示用户id

    ```
    $route.params.abc
    ```

* 路由懒加载

  ```
  ()=>import('../compoments/Home.vue')
  ```

  

* 嵌套路由

* 参数传递

  * params

  * query

    ```
    <router-link :to={path:'/home',query:{
    name:'123'
    }}></router-link>>
    ```

* 导航守卫

  * 动态修改标题

    ```
    {
    	meta: {
    		title: '首页'
    	}
    }
    
    router.beforeEach((to,from,next)=>{
    	document.title = to.matched[0].meta.title
    	next()
    })
    ```

* 保持组件的状态

  * keep-alive

  * activated，组件活跃时

  * deactivated，组件不活跃时

  * beforeRotuerLeave，离开路由时

  * 某些组件需要每次被点击是重新创建

    * exclude，include

      ```
      <keep-alive exclude="Home,User"></keep-alive>
      ```

### Promise

* 封装异步请求，避免回调地狱

* 简单使用

  ```
  new Promise((resolve,reject)=>{
  	setTimeout(function(){
  		//成功
  		resolve()
  		//失败
  		reject()
  	},)
  	
  }).then(()=>{
  	//请求成功，执行
  }).catch(()=>{
  	//请求失败，执行
  })
  ```

  ```
  new Promise((resolve,reject)=>{
  	setTimeout(function(){
  		//成功
  		resolve()
  		//失败
  		reject()
  	},)
  	
  }).then(()=>{
  	//请求成功，执行
  },()=>{
  	//请求失败，执行
  })
  ```

* 链式调用

  * 普通

    ```
    new Promise((resolve,reject)=>{
    	setTimeout(function(){
    		//成功
    		resolve()
    		//失败
    		reject()
    	},)
    	
    }).then(()=>{
    	//请求成功，执行
    	
    	//新的一个网络请求
    	return Promise((resolve,reject)=>{
    			//成功
    			resolve()
    	})
    }).then(()=>{
    
    })
    ```

  * 简写，当新的网络请求不是异步请求时

    ```
    new Promise((resolve,reject)=>{
    	setTimeout(function(){
    		//成功
    		resolve()
    		//失败
    		reject()
    	},)
    	
    }).then(()=>{
    	//请求成功，执行
    	
    	//新的一个网络请求
    	return Promise.resolve()
    }).then(()=>{
    
    })
    ```

  * 更加简单

    ```
    new Promise((resolve,reject)=>{
    	setTimeout(function(){
    		//成功
    		resolve()
    		//失败
    		reject()
    	},)
    	
    }).then(()=>{
    	//请求成功，执行
    	
    	//新的一个网络请求
    	return resolve()
    }).then(()=>{
    
    })
    ```

* 需要多个请求才能进行下一步操作时

  ```
  Promise.all([
  	new Promise((resolve,reject)=>{
  		//请求一
  	}),
  	new Promise((resolve,reject)=>{
  		//请求二
  	}),
  ]).then(res=>{
  	//res是一个数组，存储前面两次请求得到的数据或者结果
  	//下一步操作
  })
  ```

  

### Vuex

* 状态管理管家

* 响应式布局
  * 必须提前被store管理
  * 否则，在添加对象或者属性时使用Vue.set，Vue.delete

* State

  * 单一状态树
  * 所有信息都放在一个store里面

* Getters

  * 需要处理之后才能展示的信息

* Mutaions

  * 同步方法

  * 参数：payload 载荷

  * 1、普通提交

    ```
    this.$store.commit("increment",count)
    ```

  * 2、特殊封装

    ```
    this.$store.commit({
    	type: "increment",
    	count
    })
    ```

  * 常量

    * 导出一个常量

      ```
      export const incremnet = 'increment'
      ```

    * mutaions里面使用

      ```
      [increment](){
      	//内容
      }
      ```

    * methods里面使用

      ```
      this.$store.commit(increment)
      ```

* Action

  * mutation里面的异步操作

* Mudule

  * 简化state

  * 定义的模块最终被加载到state中

  * 使用方法

    ```
    {
    	module: {
    		a: moduleA
    	}
    }
    ```

    

### Axios

* 基本使用

  ```
  axios({
  	url: ''
  	//针对get请求
  	method: 'post', //或者get 
  	params: {
  		type: 'pop',
  		
  	}
  }).then(res=>{
  	//下一步操作
  })
  ```

* 并发请求

  ```
  axios.all([
  	axious(),
  	axious()
  ]).then(axios.spread((res1,res2)=>{
  	//操作
  }))
  ```

* 配置信息

  ```
  //设置全局配置
  axios.default.baseUrL = ''
  axios.default.timeout = 5000
  ```

* 创建实例

  * 不同的baseurl和超时时间等

    ```
    const instant = axios.creat({
    	baseurl: ''
    })
    ```

* 网络请求的封装

  * 回调

  * promise

    ```
    import axios from 'axios'
    export function request(config){
    	const instance = axios.creat({
    		url: '',
    		timeout: ''
    	})
    	
    	return instance(config)
    } 
    ```

* 拦截器

  * 请求拦截
  * 响应拦截

### tabbar