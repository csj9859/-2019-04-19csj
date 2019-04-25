[toc]


##   constructor (构造函数)
  实例下的constructor == 实例的构造函数

 但是这个constructor是随时随地随便可以修改的
            constructor只能当做实例中指向构造函数的一种参考物
            并不是能够左右实例的构造函数真相。

 constructor什么时候会被修改呢？
            给构造函数的原型赋址对象的时候会变

 解决:
            手动修正constructor指向
            {
                constructor:构造函数
            }



## class (类) 保留字
class是ES6才出来的新语法，优势就是写起来方便
        它其实还是之前构造函数的语法糖 

     用class代替function 后面跟类名 不用加小括号 直接花括号

 class 类名 {}
 
 使用constructor去接收参数
            constructor(a,b){ }

 写方法:
            直接在类中
                方法名 () { }

例子：

```
  class Animals{
        constructor(name,age,){
            this.name  = name;
            this.age = age;
        }
         run(){
            console.log('善奔跑');
        }
        fly(){
            console.log('飞');
        }
    }
```


## class继承
另写一个class想用上一个class的东西  用继承    **extends** 

>  class Cat extends Animal {
        constructor(...arg) {}
                super下面才能写this，不然就报错
        //    console.log(arguments);
            super(...arguments); //super括号中传入父类使用的参数
     this.jiao = '喵喵';

- 想用上边的方法直接点执行
	-     let tom = new Cat('汤姆');
    tom.run();

可以多层使用  如果是一直继承下来的 
下一个继承上一个类就可以 不用返回始祖


例子：

```
    class Animals{
        constructor(name,age,){
            this.name  = name;
            this.age = age;
        }
         run(){
            console.log('善奔跑');
        }
        fly(){
            console.log('飞');
        }
    }
    class Cat extends Animals{
        constructor(...arg){
            super(...arg);
            this.Weapons = '尖牙、利爪';
           
        }
        eat(){
            console.log('鱼');
        }
        eat1(){
            console.log('羚羊')
        }
    }

    class Eagle extends Cat{
        constructor(...arg){
            super(...arg);
            this.Wings = '翅膀';
        }
    }

    let m = new Cat('老猫','6');
    let h = new Cat('狸猫','7');
    let y = new Eagle('秃鹫','4')
    m.run()
    m.eat()
    console.log(m)
    h.run()
    h.eat1()
    console.log(h)
    y.fly()
    y.eat1()
    console.log(y)
```

-  //设置静态方法
        static shui(){
            console.log('睡觉');
        }

shui(){
            
  }

- 两种可以同时存在
 

- 不允许把一个新地址给类的原型

```
new WhiteCat('小白').chi();

    let a = new Animal('高级');
    a.runing(); //动态方法  arr.push
```
- 把父类的方法添加到自身属性中（x）以上6行是错误的 原因理论可以 实际木成立



### 扩展运算符
    // function fn(){
    //     // console.log(arguments); //...[]
    //     function f(a,b){
    //         console.log(a,b);
    //     }
    //     f(...arguments);
    // }

    // fn(1,2);

### 剩余运算符
	   //...c 是个数组
    // function fn(a,...c){
    //     console.log(a,c);
    // }
     // fn(1,2,3,4,5);



- class中继承两个就不一样

```
 class Women extends Person {
        //剩余运算符
        constructor(fs,...arg) {
            //扩展运算符
            super(...arg);
            // console.log(arg)
            this.sex = '女';
            this.fushi = fs;
        }
    }

```



对象的属性只能有一个，如果写多个，下面的会把上面的覆盖


        Object.assign(对象1,对象2,对象3....)


        从后往前合并，改变第一个对象，第一个对象可以为{}

        Child.prototype = Object.assign({},parent.prototype)

assign（分配）

