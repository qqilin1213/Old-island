### 1、访问API获取数据

```js
想访问外部的URL的话,必须在后台账号中把这个域名添加到合法域名列表中才可以去访问
如果开发阶段不想去设置这个域名的话,我们可以打开小程序开发工具>>设置>>项目设置>>✅不校验合法域名...
```

### 2、**同步，异步与回调函数**



```js
/*生命周期函数--监听页面加载*/
  onLoad: function (options) { // 小程序里的request只有异步没有同步
    console.log(this.data.test)
    let that = this//sp1
    wx.request({
      url:'http://bl.7yue.pro/v1/classic/latest'
      header:{
        appkey:"DFLSAJFLAJASJDFLJAAJD"
        },
      success:function(res){//接收异步成功的回调函数
        console.log(res)
        //在回调函数中,由于作用域发生了改变,此时的this不是指page,如果想让this指代不变,需要下面操作:
            //console.log(this.data.test)   
        console.log(that.data.test)//sp2
        }
      //ES6解决this指代的问题:改用箭头函数问题解决
      success:(res)=>{
         console.log(this.data.test)
      }
    })
  },
```

### 3、**正确理解Promise**



```css
promise解决两个问题:1.解决异步嵌套的问题(回调地狱) 2.解决使用异步回调时,无法使用return(return一个结果)的能力
```

### 4、const常量、 **Module export与import**



```js
//在config.js配置文件中,设置常量
export const config = {//const 声明一个固定不变的常量,不能被更改
  api_base_url:'http://bs.7yue.pro/v1/',
  appkey:"KDASFLAKSDJFLSDJLFJAS"
}
export let fun1 = function(){
  
}
//或者换一个导出方式:
export {config,fun1}

// 在其他.js中导入引用config.js
import {config as config1, fun1} from '../config.js'
// 注意:在import的时候不能使用绝对路径,必须使用相对路径
// 组件的时候,可以使用绝对路径
```

### 5、调试代码



```css
打开小程序工具控制台>>Sources>>
xxx.js文件是源文件处理过后的文件,Console打印错误的行号,指的是这个文件里的行号;
xxx.js?[sm]文件,跟我们编写代码文件一样,可以在这打断点,进行调试
```
