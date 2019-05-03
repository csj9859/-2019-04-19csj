[toc]
## 计算样式 和 BOM
### 计算样式
- getComputedStyle(element).属性
- 返回值：获取到的结果为**带单位**的字符串，比如：100px

### 获取宽度和高度
#### 第一组：

```
 ele.clientWidth  元素可视区宽度
 ele.clientHeight   元素可视区高度
```

- 返回值：不带单位的数字
- 支持padding，不包含边框

#### 第二组：

```
ele.offsetWidth  元素可视区宽度
ele.offsetHeight  元素可视区高度
```
- 返回值：不带单位的数字
- 支持padding，也包含边框

#### 第三组：

```
ele.scrollWidth  被内容撑开的宽度
ele.scrollHeight  被内容撑开的高度
```
- 返回值：不带单位的数字
- 不包含边框

> 第一组和第二组如果设置一个固定值，就以固定值为依据显示，不会以被内容撑开显示
> 第三组不管设不设置固定样式，都以被内容撑开为显示结果。

### 计算当前元素距离父级的距离
- **offsetParent**  
	- 定位父级
    - 没有定位父级就走body
- **offsetLeft**  
	- 当前元素（左外边框）到定位父级（左内边框）的距离
	- 获取的是不带单位的数字
- **offsetTop** 
	- 当前元素（上外边框）到定位父级的（上内边框）距离
	- 获取的是不带单位的数字

> 如果想要使用这些属性，一定要做到以下几点：
- 1.子级有绝对定位
-  2.定位父级也一定要有定位
-  3.子级和父级都要有宽高（触发haslayout，zoom:1）

### 绝对位置
- 定义：当前元素到页面顶端的距离

```
ele.clientLeft 边框尺寸
ele.clientTop 边框尺寸
```
- **getBoundingClientRect()** 
	- 当前元素到页面可视区的尺寸、距离
	- 注意：是跟滚动条走的

### BOM
> BOM(browser object model)  浏览器对象模型

- 获取浏览器的尺寸：
	- 返回值：不带单位的数字
```
window.innerWidth 浏览器的宽度
window.innerHeight  浏览器的高度
```
>  注意： window.innerWidth||window.innerHeight如果有滚动条，是忽略了滚动条的尺寸的

- **document.body.clientWidth**  浏览器的尺寸,排除滚动条的
	- 注：使用的时候把默认样式清除，如：*{margin:0;padding:0;}
- **window.open(url,用什么方式打开_blank,_self)**  打开新的窗口
	- 注意：需要用户主动触发才不会被拦截
	- 比如： window.open('http://www.baidu.com')
-  **window.close();** 关闭浏览器窗口
	-  注：最好也是用户主动触发体验才好
### 滚动条距离
- 滚动条距离，只能读不能写
	- 返回值：没有单位的数字

```
window.pageYOffset
window.pageXOffset
```
-  **window.scrollTo(x,y)**专门用来写滚动条距离的
-  滚动条的距离，既能读又能写**(document.documentElement=HTML)**
	-  **document.documentElement.scrollTop**
	
### 	缩放浏览器事件
-  **onresize**  缩放浏览器的时候触发的事件
### 滚轮事件
- **onscroll** 有滚动条的时候滚轮时触发。

### 浏览器的内核信息
- **window.navigator.userAgent**，查看用户的浏览器内核信息
	- 注意： 使用的时候判断的字符串有可能会被模拟。
-  **window.location.href**   在当前页面中跳转页面
	

```
if(/iphone/i.test(str)){
  window.location.href = 'http://www.baidu.com';
}else if(/android/i.test(str)){
    window.location.href = 'http://www.sogou.com';
}else{
    window.location.href = 'http://www.zhufengpeixun.cn';
}
```
### 浏览器地址栏信息

```
hash: ""  浏览器hash信息 #之后的信息，更换这个信息是不会刷新页面的

window.location.hash 即能读也能写

host: ""   ip地址 + 端口号
hostname: ""  ip地址
href: ""   url
origin: "file://"
port: ""  端口
protocol: "file:"   协议
reload: ƒ reload()   刷新页面
replace: ƒ ()  替换页面
search: ""   查询信息
```

### 查询信息
-  **window.location.search** ?到#号之间的信息
	-  既可读也可写，只不过写的时候会刷新页面
	-  比如：http://www.zhufengpeixun.cn?num=1#page=0
	
###   刷新页面
-  **window.location.reload()**

### 抖动小例子

```
<style>
#box{
    width:100px;
    height:100px;
    background: skyblue;
    position:absolute;
    top:0;
    left:300px;  
}
#box2{
    width:100px;
    height:100px;
    background:pink;
}
</style>
```

```
<div id="box">
    <div id="box2"></div>
</div>
```

```
<script>
    let ary = [10,-10,8,-8,6,-6,4,-4,2,-2,0];
    let num = 0;
    let timer = null;
    box.onclick = function(){
        let l = this.offsetLeft;
        timer = setInterval(() => {
            num++;
            this.style.left = l + ary[num] + 'px';
            if(num == ary.length){
                clearInterval(timer);
                // console.log(1);
                box2.style.transition = '0.5s';
                box2.style.transform = 'scale(.5)';
                num=0;
            };
            
        }, 16.7);
    }
</script>
```
      
    
    


