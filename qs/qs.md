## 闭包
闭包说的通俗一点就是打通了一条在函数外部访问函数内部作用域的通道。
正常情况下函数外部是访问不到函数内部作用域变量的，
表象判断是不是闭包:函数嵌套函数,内部函数被 return 内部函数调用外层函数的局部变量
优点：可以隔离作用域，不造成全局污染
缺点：由于闭包长期驻留内存，则长期这样会导致内存泄露
如何解决内存泄露：将暴露在外部的闭包变量置为 null
适用场景：封装组件，for 循环和定时器结合使用,for 循环和 dom 事件结合.可以在性能优化的过程中,节流防抖函数的使用,导航栏获取下标的使用

## JS 中的原型链的理解
原型
万物皆对象，每个对象都有自己的属性，原型解决js中让一个或多个对象共享一个方法的问题
在js中每个对象都有一个与他关联的对象，叫原型对象
每次获取对象属性都是一次查询过程，在对象的自有属性中找不到就会查找他的原型对象
原型链
当我们访问一个对象的属性或方法的时候，首先他会从自身去找，找不到的话会从他的原型上去找，如果原型上还是找不到的话，他就会从他的原型的原型上去找，直到查找到顶端Object。这样一来，就形成了一个链式的结构

## svg优点
矢量图形，放大缩小不影响图像质量；
可编辑可搜索；
平均来讲，SVG文件比JPEG和PNG格式的文件要小很多，因而下载也很快；
动画文件体积更小，播放资源占用更优，动画还原效果更好；
字号小于12px的文字可以用svg嵌套text显示；（1. 使用 transform: scale() 设置后占位区域并没有改变，难以调节对齐方式。2. 使用 canvas 无法选中文字（也可以解决，但不如 svg 简洁））

## 二分查找 [-1,0,1,3,5,6,10,20,21,25,26]  查找20的位置
function binarySearch(arr, target) {
    let start = 0;
    let end = arr.length - 1;
    let middle;
    while(start <= end) {
        if (target === arr[middle]) {
            return middle;
        } else if (target < arr[middle]) {
            end = middle - 1;
        }
    }
}

## css3animation
name duration ease
@keyframes from to 0% 100%

## promise源码理解
Promise是什么？有什么作用？
异步编程的一种解决方案
可以将异步操作队列化，按照期望的顺序执行，返回符合预期的结果
可以在对象之间传递和操作promise，帮助我们处理队列

三种状态 pending、resolved、rejected

pending -> resolved
pending -> rejected

状态一旦改变，就不会再变。
创造Promise实例后，它会立即执行。

如何改变状态？首先我们可以创建一个promise，可以new一个promise，接收一个函数作为参数，这个函数接收resolve、reject两个参数
const p1 = new Promise((resolve, reject) => {

})
改变状态一般在异步任务中改变
resolved状态会触发.then(()=>{})
rejected状态会触发.catch函数
.all() 接收一个数组作为参数，数组里可以是Promise对象，也可以是别的值，返回值是全部值的数组，有任何一个失败，该Promise失败，返回值是第一个失败的子Promise结果
.race() 有任意一个完成就算完成

## 对事件循环的理解
宏任务和微任务
宏任务执行时间比微任务早
宏任务：setTimeout、setInterval、DOM事件、AJAX请求
微任务：Promise、async/await

## JS 数据类型
基本数据类型：number,string,Boolean,null,undefined,symbol（ES6 新增）
复合类型：Object,function

## 深拷贝
1、json
2、lodash函数deepClone
3、递归
function deepClone(obj = {}) {
    if (typeof obj !== 'object' || obj === null) {
        return obj;
    }
    let result = Array.isArray ? [] : {};
    for(let key in obj) {
        if (obj.hasOwnProperty(key)) {
            result[key] = deepClone(obj[key]);
        }
    }
    return result;
}

## 网络相关知识，http、https

## v-show v-if
v-if 和 v-show 都可以显示和隐藏一个元素，但有本质区别
v-if 是惰性的，只是值为 false 就不会加载对应元素，为 true 才动态加载对应元素
v-show:是无论为 true 和为 false 都会加载对应 html 代码，但为 false时用 display:none 隐藏不在页面显示，但为 true 时页面上用 display:block显示其效果
适用场景：切换频繁的场合用 v-show,切换不频繁的场合用 v-if

## vue双向绑定原理
核心主要利用 ES5 中的 Object.defineProperty 实现的，然后利用里面的getter 和 setter 来实现双向数据绑定的

## 计算二叉树深度
function treeDeep (tree) {
    if (!tree) {
        return -1;
    } else {
        return Math.max(treeDeep(tree.left), treeDeep(tree.right)) + 1;
    }
}

## JS 继承（含 ES6 的）
什么是继承
通过【某种方式】让一个对象可以访问到另一个对象中的属性和方法
Js 中继承 es6 中的继承
如何实现继承
构造函数继承 原型、原型链继承 拷贝继承(混入继承：mixin)
用.call()和.apply()将父类构造函数引入子类函数
es6继承，用 class 定义类，用 extends 继承类，用 super()表示父类

## es6新增特性
let/const，箭头函数，模版字符串，解构赋值，模块的导入（import）和导出（export default/export），promise，还有一些数组的新方法等，我比较常用

## js数组常用方法
push
pop
unshift
shift
splice
join
concat
forEach
filter
map
sort
some，只要数组中至少存在一个满足条件的结果，返回值就为 true,否则返回 fasel, 写法和 forEach 类似
every，数组中每一项都得满足条件时，才返回 true，否则返回 false, 写法和 forEach 类似

## 从输入 URL 到页面加载完中间发生了什么
1. DNS 解析
2. TCP 连接
3. 发送 HTTP 请求
4. 服务器处理请求并返回需要的数据
5. 浏览器解析渲染页面
6. 连接结束

## call,apply,bind 区别
答：call,apply,bind 主要作用都是改变 this 指向的，但使用上略有区别，说
一下区别:
call 和 apply 的主要区别是在传递参数上不同，call 后面传递的参数是以
逗号的形式分开的，apply 传递的参数是数组形式 [Apply 是以 A 开头的,所
以应该是跟 Array(数组)形式的参数]
bind 返回的是一个函数形式，如果要执行，则后面要再加一个小括号 例如：
bind(obj,参数 1,参数 2,)(),bind 只能以逗号分隔形式，不能是数组形式

## 什么情况下会产生跨域及产生跨域的解决方案和实现原理
产生跨域的情况有：不同协议，不同域名，不同端口以及域名和 ip 地址的访问都会产生跨域。
跨域的解决方案目前有三种主流解决方案：
跨域是浏览器做出的限制,和后端没关系
一、 jsonp
jsonp 实现原理：主要是利用动态创建 script 标签请求后端接口地址，然后传递 callback 参数，后端接收 callback，后端经过数据处理，返回 callback 函数调用的形式，callback 中的参数就是 json
二、 代理（前端代理和后端代理）
18 / 64
前端代理我在 vue 中主要是通过 vue 脚手架中的 config 中的
index 文件来配置的，其中有个 proxyTable 来配置跨域的
三、 CORS
CORS 全称叫跨域资源共享，主要是后台工程师设置后端代码来达
到前端跨域请求的

## webpack loader和plugin区别

## vue 组件通讯（即传值）
父传子：主要通过 props 来实现的
父组件通过 import 引入子组件，并注册，在子组件标签上添加要传递的属性，子组件通过 props 接收，接收有两种形式一是通过数组形式[‘要接收的属性’ ]，二是通过对象形式{ }来接收，对象形式可以设置要传递的数据类型和默认值，而数组只是简单的接收

子传父：主要通过$emit 来实现
子组件通过通过绑定事件触发函数，在其中设置this.$emit(‘要派发的自定义事件’，要传递的值)，$emit 中有两个参数一
是要派发的自定义事件，第二个参数是要传递的值然后父组件中,在这个子组件身上@派发的自定义事件,绑定事件触发的methods 中的方法接受的默认值,就是传递过来的参数

兄弟之间传值有两种方法
通过 event bus 实现
通过 vuex 实现
vuex 是一个状态管理工具，主要解决大中型复杂项目的数据共享问题，主要包括 state,actions,mutations,getters 和 modules 5 个要素，主要流程：组件通过 dispatch 到 actions，actions 是异步操作，在 actions中通过 commit 到 mutations，mutations 再通过逻辑操作改变 state，从而同步到组件，更新其数据状态

## 事件循环
js是单线程语言，他的异步和多线程是通过EventLoop事件循环来实现的，包括三个部分：调用栈、消息队列（宏任务队列）、微任务队列，eventloop一开始会在全局中执行，遇到函数调用就放到栈中，函数返回后从栈中弹出
宏任务对了：setTimeout、setInterval、AJAX请求、DOM事件等；
微任务队列：Promise、async/await等；

async function async1() {
    console.log('async1 start’);3直接执行
    await async2();4执行
    console.log('async1 end’);6微任务队列 10执行
}
async function async2() {
    console.log('async2’);5执行
}
console.log('script start’);1直接执行
setTimeout(function() {
    console.log('setTimeout’);2宏任务队列 12执行
}, 0)
async1();
new Promise(function(resolve) {
    console.log('promise1’);7执行
    resolve();
}).then(function() {
    console.log('promise2’);8微任务队列 11执行
});
console.log('script end’);9执行

script start
async1 start
async2
promise1
script end
async1 end
promise2
setTimeout

## 二叉树
let tree = {
	val: 0,
	left: {
		val: 0,
		left: null,
		right: {
			val: 0,
			left: null,
			right: {
				val: 0,
				left: null,
				right: null,
			},
		},
	},
	right: {
		val: 0,
		left: {
			val: 0,
			left: null,
			right: null,
		},
		right: {
			val: 0,
			left: null,
			right: null,
		},
	},
}
function treeDeep(tree) {
    if(!tree) {
        return 0;
    } else {
        return Math.max(treeDeep(tree.left), treeDeep(tree.right)) + 1;
    }
}
console.log('----tree', );

## flex布局
flex-direction 主轴方向 水平、垂直；
justify-content 主轴上对齐方式 开始对齐、结束对齐、居中对齐、两端对齐；
align-items 交叉轴对齐方式 开始对齐、结束对齐、居中对齐；
flex-wrap 是否换行，wrap、nowrap

## 三块，左右200px，中间自适应
flex-grow: 1; 

## flex: 1 0 100px;
flex-grow 拉伸因子；
flex-shrink 收缩规则；
flex-basis 主轴方向初始大小；
flex:1 === flex：1 1 0%

## 覆盖宽度

## var、let、const区别
作用域不同，var是全局作用域，let和const是块级作用域；
let定义的值可以改变，const不能，定义栈的可以；
暂时性死区、变量提升
let、const在代码下方会造成暂时性死区，var不会；

## vue2双向绑定原理

## vue3双向绑定原理

## 区别

## vue data变量新增

## bfe，margin重叠
margin重叠指两个或多个盒子（可能相邻也可能嵌套）的相邻边界重合在一起而形成的单一边界。
解决：bfe
底部元素设置为浮动float:left
底部元素的position的值为absolute/fixed
在设置margin-top/bottom值时统一设置上或下

## 跨域及解决办法
跨域是浏览器同源策略引起的，协议、域名、端口号不同会引起跨域；
解决：jsonp、iframe、websocket、proxy、CORS跨域资源共享、nginx代理跨域

## jsonp实现原理
使用script标签，请求后端地址，传递callback数据，后端对数据进行处理，再返回json格式数据；

## v-if和v-show，哪个触发生命周期
v-if和v-show都是控制DOM元素显示与隐藏的，使用true、false判断

## js instanceof实现原理
原型和原型链，实例的__proto__ === 对象的prototype，递归
function myInstanceof(target, origin) {
      const proto = target.__proto__;
      if (proto) {
        if (origin.prototype === proto) {
          return true;
        } else {
          return myInstanceof(proto, origin)
        }
      } else {
        return false;
      }
    }

## 浏览器重绘、重排
重绘指元素外观改变引起的浏览器的动作，例如颜色、背景色、visitable等属性；
重排指元素布局发生变化，如页面初始化渲染、浏览器窗口尺寸改变、元素位置内容改变、添加删除dom元素等
重排：当DOM的变化影响了元素的几何信息(DOM对象的位置和尺寸大小)，浏览器需要重新计算元素的几何属性，将其安放在界面中的正确位置，这个过程叫做重排
重绘不会引起重排，重排一定会引起重绘；
解决：减少dom操作，最小化dom访问次数，尽量缓存dom的样式信息；
使用vue、react等框架，数据改变视图；使用class不使用style，style改变节点样式
不要使用table布局，table中某个元素一旦触发reflow，整个table都会触发reflow
减少使用display:none（重排），visibility:hidden代替（重绘）
使用transform，跳过重排重绘直接合成处理；

## 浏览器持久化，localStorage设置过期时间
cookie，服务器生成，可设置过期时间，与服务端通信，携带在header中；
本地存储
sessionStorage，页面关闭，清空数据；
localStorage，除非被清除，永久有效；
localstorage原生是不支持设置过期时间的，想要设置的话，就只能自己来封装一层逻辑来实现localStorage.setItem(key,JSON.stringify({val:value,time:curtime}));//转换成json字符串序列
indexDB，除非被清除，否则一直存在，非关系型数据库，可以存储大量数据；

## async/await
async返回promise函数值
await接promise

## vue生命周期
创建
beforeCreate created
加载
beforeMounte 
更新
销毁