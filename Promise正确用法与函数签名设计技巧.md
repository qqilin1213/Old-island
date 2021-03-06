### 1、异步处理方案
```js
异步处理方案一: 纯粹callback
异步处理方案二: promise(是一个对象,可以保存状态)
  promise的优势:
    代码风格方面: 1.解决回调地狱 2.解决callback无法return问题
    功能方面: 1.解决多个异步等待合并
异步处理方案三: async await(promise的语法糖) ES2017 小程序不支持
```
### 2、Promise基本用法
```js
//Promise 可以理解成一个对象,可以保存状态. 精髓:用对象的方式保存了异步调用的结果
// Promise 第一步
const promise = new Promise((resolve, reject)=>{
  // 异步代码写在Promise的函数中 第二步
  // Promise整个过程状态: 进行中 已成功 已失败 凝固
  // resolve是把进行中变成已成功, 而reject是把进行中变成已失败
  wx.getSystemInfo({//微信内部异步获取用户信息的函数
    success:(res)=>{
      resolve(res)
    },
    fail:(error)=>{
      reject(error)
    }
  }) 
})
代码简写:
const promise = new Promise((resolve, reject)=>{
  wx.getSystemInfo({
    success: res => resolve(res),
    fail: error => reject(error)
  })
})

//接收有两个函数参数: 已成功时的回调函数 失败函数回调
promise.then((res)=>{
  console.log(res)
},(error)=>{
  console.log(error)
})
代码简写:
promise.then(
    res => console.log(res)
  error => console.log(error)
)
```

### 3、Promise解决回调地狱例子



```js
// 1. 多个promise函数操作解决嵌套地狱情况
bookModel.getHotList()
    .then(res =>{
        console.log(res)
        return bookModel.getMyBookCount()//返回promise的异步函数
    })
    .then(res=>{
        console.log(res)
        return bookModel.getMyBookCount()
    })
    .then(res=>{
        console.log(res)
        return bookModel.getMyBookCount()
    })
// 2. promise与非promise解决嵌套函数的情况
const promisic = function(func){//把小程序异步回调函数变promise,再执行1操作
  return function(params={}){
    new Promise((resolve, reject)=>{
      const args = Object.assign(params,{
        success:(res)=>{
          resolve(res)
        },
        fail:(error)=>{
          reject(error)
        }
      })
      func(args)
    })
  }
}
```
