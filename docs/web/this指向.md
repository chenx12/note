## this指向

### 普通函数中的this

1. 总是代表着它的直接调用者，如obj.fn，fn里的最外层this就是指向obj
2. 默认情况下，没有直接调用者，this指向window
3. 严格模式下（设置了'use strict'），this为undefined
4. 当使用call，apply，bind绑定的，this指向绑定对象
	1. call 方法第一个参数是this的指向，后面传入的是一个参数列表。当第一个参数为null、undefined的时候，默认指向window。如：getUserName.call(obj, 'Bob', 'Tom')

	2. apply 方法接受两个参数，第一个参数是this的指向，第二个参数是一个参数数组。当第一个参数为null、undefined的时候，默认指向window。如：getUserName.apply(obj, ['Bob', 'Tom'])

	3. bind 方法和 call 方法很相似，第一个参数是this的指向，从第二个参数开始是接收的参数列表。区别在于bind方法返回值是函数以及bind接收的参数列表的使用。低版本浏览器没有该方法，需要自己手动实现

### 箭头函数中的this

1. 默认指向定义它时，所处上下文的对象的this指向。即ES6箭头函数里this的指向就是上下文里对象this指向，偶尔没有上下文对象，this就指向window
2. call，apply，bind等方法不能改变箭头函数this的指向

#### 举例

1. hello直接调用者是obj，第一个this指向obj，setTimeout里匿名函数没有直接调用者，this指向window
```javascript
const obj = {
    num: 10,
   hello: function () {
    console.log(this);    // obj
    setTimeout(function () {
      console.log(this);    // window
    });
   }    
}
obj.hello();
```
2. hello直接调用者是obj，第一个this指向obj，setTimeout箭头函数，this指向最近的函数的this指向，即也是obj
```javascript
const obj = {
    num: 10,
   hello: function () {
    console.log(this);    // obj
    setTimeout(() => {
      console.log(this);    // obj
    });
   }    
}
obj.hello();
```

### 代码举例

```javascript
let abc = {
	bcd: 1,
	cde: {
		bcd:2,
		def:() => {console.log(this)},
		fgh: {
			hij:() => {console.log(this)}
		}
	},
	efg: () => {console.log(this)},
	jkl:{
		bcd:3,
		lmn:function(){
			console.log(this.bcd)
			console.log(this)
		}
	}
}
window.bcd = 5
abc.jkl.lmn()// 3 jkl
let haa = abc.jkl.lmn
haa()  // 5 window

abc.efg() // window
abc.cde.def() // window
abc.cde.fgh.hij()// window
let hhh = abc.cde.fgh.hij 
hhh()// window
```

