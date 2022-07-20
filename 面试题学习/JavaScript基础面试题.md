### 1.延迟加载JS有哪些方式？

```js
1.js脚本放在文档的底部，来使js脚本尽可能的在最后来加载执行
2.在script标签中 添加async 或 defer （仅适用于script）
	async：不让页面等待下载，从而异步加载页面其他内容
	defer：在html已加载后才运行js


async 与 befer 的区别
1.async 与html解析同步的，所有js文件谁先加载完谁先执行。
2.defer 等html解析完成后，才会顺次执行js脚本
```

### 2.JS数据类型有哪些

```js
基本类型：string、number、boolean、undefined、null、symbol、bigint

引用类型：object
```



### 3.null与undefined的区别







### 4.微任务和宏任务

```
1.js是单线程语言


2.同步代码 ===> 异步代码（微任务 ===> 宏任务）




```

1. promise的几个API

promise.resolve(1)

promise.reject(1)

promise.all([promise1,promise2,promise3])

promise.race([promise1,promise2,promise3])

1. promise的三个状态
pending，表示进行中

fulfilled也是resolved，表示成功

rejected，表示失败

2.promise的状态变化
只能从pending->resolved或者pending->rejected

promise的状态改变后就不会再次改变会一直保持这个状态，而且promise不会受到外界的影响，只会受到异步操作的结果的影响

3.promise的基本用法
new Promise((resolve,reject)=>{
				if(true){
					resolve(value);
				}else{
					reject(err);
				}
			}).then(
				value=>{};
				reason=>{};
			).catch(
			)
新建一个promise构造函数，函数接受一个函数作为参数，同时该函数有两个参数，reject和resolve

执行异步操作

成功执行resolve()，状态变成resolved状态

失败执行reject()，状态变成rejected状态

无论成功还是失败都可以通过.then()指定成功和失败的回调函数，catch只能调用失败的回调函数

promise是同步执行，then是异步执行


5.JS中的同步与异步
同步就是指放在主线程中执行的任务，只有主线程中上一个任务执行完毕才执行下一个同步任务

异步不是在主线程中执行，而是将其放在任务队列中执行，只有等到主线程执行完毕，任务队列中的任务才放入主线程执行

而比较重要的一点是任务队列又分为宏队列和微队列

executor是promise的执行器函数，是同步执行的函数，也就是说promise是同步，而promise的回调函数是异步

6.宏队列和微队列
宏队列：用来保存待执行的宏任务，，比如定时器、DOM回调、ajax回调

微队列：用来保存待执行的微任务，比如：promise的回调/mutationObserver的回调

 

执行顺序：每次取出宏任务之前要先把微任务全部取出来放到栈里面处理掉，然后再执行宏任务

























