# ES6笔记
## 一，ES6-let变量声明以及生命特性
```javascript
 <script>
    let a;
    let b,c,d;
    let e = 100;
    let f = '熊祥林', g = [], h = {};
    
    //1.变量不能重复声明
    // let me = '张永';
    // let me = '熊相林';

   //2,块级作用域（只在块级作用域里生效） 全局，函数，eval
    // if else for while 
    // {
    //     let boy = '熊相林'
    // }
    // console.log(boy);  无法打印出变量值

    //3,不存在变量提升
    // console.log(song);
    // let song = '盖世英雄';   这样写会报错


    //4,不影响作用域链效果，函数内部找不到变量定义的时候会向上一级寻找
        {
            let school = 'zzu';
            function xuexiao () {
                console.log(school);
            }
            xuexiao();
        }

    </script>
```


## 二，const声明常量以及特点

```javascript
  <script>
        //常量声明

        const SCHOOL = '尚硅谷';

        //1.常量一定要赋初始值
        //const A; 错误写法
        //2.一般常量写成大写（潜规则，不是语法强制要求）
        // const a = 100;错误写法
        //3.常量的值是不能被修改的

        //4.块级作用域
        // {
        //     const PLAYER = 'uzi';
        // }
        // console.log(PLAYER);  //无法打印块级作用域里的常量

        //5.对于数组和对象的元素修改，不算做对常量的修改，不会报错
        // const TEAM = ['UZI','MXLG','MING','LETME'];
        // TEAM.push('Meiko');//这种修改只是修改常量数组指向的那块空间里保存的值。非修改常量数组指向的那块地址。
        // TEAM = 1000;   //如果这样修改直接把常量里保存的空间地址给修改了，会报错。


    </script>

```
## 三，变量的结构赋值

```javascript
<!-- <script>
    //ES6允许按照一定模式c从数组和对象种提取值，并对变量进行赋值，这被称为结构赋值
    //1.数组结构赋值

    // const  F4 = ['刘能','小沈阳','赵四','宋小宝'];
    // let [liu,xiao,zhao,song] = F4;
    // console.log(liu);
    // console.log(xiao);
    // console.log(zhao);
    // console.log(song);

   // 2.对象结构赋值
    const shifu = {
            name: '赵本山',
            age: 70,
            nengli : function () {
                console.log("我会演小品");
            },
    }

    let {name,age,nengli} = shifu;   //注意被赋值的属性方法名必须与提取对象中的一样

        console.log(name);
        console.log(age);
        console.log(nengli);
        nengli();

</script> -->
```

## 四，模板字符串（反引字符串` `）

```javascript
<script>

    //ES6 引入新的声明字符串的方式反引号``
    //1.声明
    let str = `我也是一个字符串`;
    console.log(str,typeof(str));

    //2.内容中可以直接出现换行符(以前的引号内是不可以出现换行符的，需要进行拼接)
    let str1 = `<ul>
                <li>沈腾</li>
                <li>玛丽</li>
                <li>邓伦</li>
                <li>魏翔</li>
                </ul>`;
    //3.变量拼接
    let v1 = '魏翔';
    let v2 = `${v1}也是一个喜剧演员`;
    console.log(v2);

</script>
```
## 五，对象的简化写法

```javascript
<script>
        //es6允许在大括号里，直接写入变量和函数，作为对象的属性和方法
        let name = '熊相林';
        let change = function (){
          console.log('我们可以改变世界');
        }
        function change1 (){
          console.log('我们可以创造世界');
        }

        const school = {
                name,
                change,
                change1,
                improve () {
                    console.log('我们可以提升技能水平');
                }  //ES6中方法的简化写法

                // improve:function (){
                //   console.log('我们可以提升技能水平');
                // }   以前写法
        }

      console.log(school);
      
</script>
```


## 六，箭头函数以及声明特点

```javascript
<script>
    //ES6允许使用箭头=>定义函数
  
    let fn =(a,b)=>{
        return a+b;
    }
    //调用函数
    let result = fn(1,2);
    console.log(result);

    //1.this是静态的.this始终指向函数声明时所在父级作用域里的this值
    function getName(){
        console.log(this.name);
    }
    let getName1 = ()=>{
        console.log(this.name);
    }
    //设置window对象的name 属性
    window.name ="熊相林";
    const SCHOOL = {
        name:'ATA',
    }
    //直接调用都为熊相林
    // getName();
    // getName1();

    //call方法调用，静态的this无法被修改，使用call或者apply也不能被修改
   getName.call(SCHOOL);
   getName1.call(SCHOOL);

  // 2.不能作为构造函数实例化对象(以下例子为错误示范)
//   let Person = (name,age)=>{
//         this.name = name;
//         this.age = age;
//   }

//   let me = new Person('xiao',18);
//   console.log(me);  

    //3.不能使用arguments变量(以下为错误示范)
    // let fn1 = () => {
    //   console.log(arguments);
    // }
    // fn1(1,2,3);
    
    //4.箭头函数得简写
    // 1)省略小括号,当形参有且只有一个时候
    //     let add = (n)=>{
    //         return n+n;
    //     }
    //     可简写为
    //     let add = n =>{
    //         return n+n;
    //     }
    //   console.log(add(9));
    // 2)当大括号里的代码体只有一条执行语句的时候可以省略大括号,
        //  let add = n =>{
        //     return n+n;
        //  }
        //  简写为 （必须把return去掉，并且该函数的返回值就是这条语句的执行结果）
          let add = n => n+n;
        console.log(add(8));
    
</script>
```
## 七，给函数形参赋初始值

```javascript
     <script>
        //ES6 允许给函数的参数赋值初始值
        //1.形参初始值  具有默认值的参数，一般位置要靠后（潜规则）
        function add (a,b,c=10) {    //没有值的话就用默认值
            return a+b+c;
        }
        let result = add(1,2);
        console.log(result);

        //2.与结构赋值结合 

        function connect ({host = "127.0.0.3",username,password,port}) {   //也可直接添加默认值，没传参数的话就是用默认值
                console.log(host);
                console.log(username);
                console.log(password);
                console.log(port);
        }
        //结构赋值的时候属性名要注意一致
        connect({
            host : "localname",
            username : "root",
            password : "root",
            port:3306});

    </script>
```

## 八，es6函数的rest参数

```javascript
<script>
    //es6引入rest参数，用于获取函数的实参，用来代替arguments
    //es6 获取实参的方式
    // function date() {
    //     console.log(arguments);
    // }
    // date('张三','李四','王五');

    //rest参数
    function date(...args) {
        console.log(args);       //返回的是一个数组对象，可以使用数组的一些方法
    }
    date('张三','李四','王五');    //返回结果['张三','李四','王五']

    //rest 参数必须要放到参数最后（语法限制）
    function fn (a,b,...args) {    //...args放到参数中间会报错
        console.log(a);
        console.log(b);
        console.log(args);
    }
    fn(1,2,3,4,5,6,7)    //返回结果1,2,[3,4,5,6,7]

</script>
```

## 九， ...扩展运算符

```javascript
<script>
    //[...] 扩展运算符能将数组转换为逗号分隔的参数序列
    //声明一个数组
    const tfboys = ['易烊千玺','王俊凯','王源'];

    function chunwan() {
        console.log(arguments);
    }

   // chunwan(tfboys);   //第一种形式打印出来的结果只有一个参数
    chunwan(...tfboys);   //第二种是...扩展运算符用法，打印出来会有三个参数，相当于chunwan('易烊千玺','王俊凯','王源');

    //...扩展运算符与rest参数不同点在于rest参数要放在在形参中的最后一位
</script>


...扩展运算符的运用

<div></div>
<div></div>
<div></div>

<script>
    
    //1.数组的合并
    const kuaizi = ['王太利','肖央'];
    const fenghuang = ['曾毅','玲花'];
    //const hebing = kuaizi.concat(fenghuang); 合并数组

    const hebing = [...kuaizi,...fenghuang];  // 相当于=>['王太利','肖央','曾毅','玲花']
    console.log(hebing);

    //2.数组的克隆
    const sanzhihua = ['E','G','M'];
    const sanyecao = [...sanzhihua];   //如果数组中又引用值的话，拷贝属于浅拷贝
    console.log(sanyecao);

    //3.将伪数组转化为真数组

    const divs = document.querySelectorAll('div');
    const divArr = [...divs];
    console.log(divArr);   //转化为一个真正的数组

</script>   

```

## 十，symbol类型数据

ES6 引入了一种新的原始数据类型 Symbol ，表示独一无二的值，最大的用法是用来定义对象的唯一属性名。

ES6 数据类型除了 Number 、 String 、 Boolean 、 Object、 null 和 undefined ，还新增了 Symbol 。

Symbol 函数不能用 new 命令，因为 Symbol 是原始数据类型，不是对象。可以接受一个字符串作为参数，为新创建的 Symbol 提供描述，用来显示在控制台或者作为字符串的时候使用，便于区分。

Symbol特点：             
1） Symbol的值是唯一的用来解决命名冲突的问题
2） Symbol值不能其他数据进行运算
3） Symbol定义的对象属性不能使用for...in循环遍历，但可以使用Reflect.ownKeys来获取对象的所有键名

```javascript
<script>
        //创建symbol
        //1.
        let s = Symbol();
       // console.log(s, typeof s);
       //2.
        let s2 = Symbol('熊相林');  //相当于对symbol对象做了一个注释
        let s3 = Symbol('熊相林');
        console.log(s2===s3);   //false   两个并不是同一个对象
        //3. Symbol.for 创建
        let s4 = Symbol.for('张永');   //函数对象
        let s5 = Symbol.for('张永');    //创建出一个唯一的对象
        console.log(s4===s5);     //true

        //不能与其他数据进行运算比较，与自己也不能运算

        //4. Symbol创建对象属性

        //向对象中添加方法 up down
        // let game = {

        //     up: function () {
        //         console.log('我是先来的up');
        //     },
        //     down: function () {
        //         console.log('我是先来的down');
        //     }

        // }

        // let method = {
        //     up : Symbol,
        //     down : Symbol
        // }

        // game[method.up] = function () {
        //         console.log('我是后加的up');
        //     }; 
        // game[method.down] = function () {
        //         console.log('我是后加的down');
        //     };

        // console.log(game);

        
        let youxi = {
            name : '狼人杀', 
            [Symbol('say')] : function () {
                console.log('我可以发言');
            },
            [Symbol('zibao')] : function () {
                console.log('我可以自爆');
            }
        }
        //作为属性名使用时不能用点形式，必须放在括号内，如果用点，声明的是普通属性名，而不是Symbol
        console.log(youxi);

</script>
```

## 十一，迭代器
    迭代器（iterator）是一种接口，为各种不同的数据结构提供统一的访问机制。任何
数据结构只要不是iterator接口，就可以完成遍历操作。
1） ES6创造了一种新的遍历命令for...of循环，iterator接口主要供for..of消费
2） 原生具备iterator接口的数据（可用for of遍历）
    a) Array
    b) Argument
    c) Set
    d) Map
    e) String
    f) TypedArray
    g) NodeList
3) 工作原理
    a) 创建一个指针对象，指向当前数据结构的起始位置
    b) 第一次调用对象的next方法，指针自动指向数据结构的第一个成员
    c) 接下来不断调用next方法，指针一直往后以东，直到执行最后一个成员
    d) 每调用next方法返回一个包含value和done属性的对象
注意：需要自定义遍历数据的时候，要想到迭代器

```javascript
<script>
    //迭代器 iterator
    //声明一个数组
    // const xiyou = ['唐僧','孙悟空','猪八戒','沙僧'];

    //使用for ..of遍历数组
    // for (let v of xiyou){     
    //      //迭代器里的v表示键值，for..in中的v表示的是键名,注意区分
        
    //     console.log(v);

    // }

       // console.log(xiyou);

        // let iterator = xiyou[Symbol.iterator]();   //需要在xiyou调用的方法加上()表示执行
        // console.log(iterator.next());
        // console.log(iterator.next());
        // console.log(iterator.next());
        // console.log(iterator.next());
        // console.log(iterator.next());

        //done为true的时候表示遍历完成

    //自定义迭代器
    //声明一个对象
    const banji = {

        name : '终极一班',
        stus : [
            '张三',
            '赵四',
            '王五',
            '李六'
        ],

        [Symbol.iterator] : function () {   //迭代器是一个方法
            //索引变量 
            let index=0;
            //保存一下this
            let _this = this;
            return {
                next : function () { 
                    if (index<_this.stus.length){
                        const result = {value: _this.stus[index],done:false};
                        index++;
                        return result;
                    }else{
                            return {value: undefined,done:true};
                        }
                    }
                };
            }
    }

    //遍历这个对象
    for (let v of banji){
        console.log(v);
    }

</script>
```

## 十二，生成器

    生成器是es6提供的一种异步编程解决方案，语法行为与传统函数完全不同
```javascript 
<script>
    //1.生成器其实就是一个特殊函数
    //异步编程 纯回调函数   例如node->fs   ajax   mongodb

    // function * gen(){   //声明方式与原来不同，中间需要加*

    //     //console.log('hello generator');
    //    // console.log(1);
    //     yield '一直没有耳朵';   // yield 是函数代码的分割符，把函数代码分割成几块
    //    // console.log(2);
    //     yield '一直没有尾巴';
    //   //  console.log(3);
    //     yield '真奇怪';
    //    // console.log(4);
    // }

    // let iterator = gen();
    //console.log(iterator);

    // iterator.next();    //借助迭代器中的next方法执行下一步操作
    // iterator.next();
    // iterator.next();
    // iterator.next();

    // console.log(iterator.next()); 
    // console.log(iterator.next()); 
    // console.log(iterator.next()); 
    // console.log(iterator.next()); 

    // for (let v of iterator) {
    //     console.log(v);
    // }
    

    //2.生成器函数参数

    // function *gen (arg) {
    //   console.log(arg);
    //   let one = yield 111;
    //   console.log(one);
    //   let two = yield 222;
    //   console.log(two);
    //   let three = yield 333; 
    //   console.log(three);
    // }
    // //执行获取迭代器对象
    // let iterator = gen('AAA');   //生成去函数可以往里面传递参数
    // console.log(iterator.next());

    // //next方法也可以传入实参 ，传入的参数当作上一句yield语句执行的返回值
    //  console.log(iterator.next('BBB'));
    //  console.log(iterator.next('CCC'));   //next方法会返回yield语句后面的值或者字面量的值
    //  console.log(iterator.next('DDD')); 

    //3.生成器函数实例
    //异步编程  文件操作 网络操作（ajax ,request） 数据库操作
    //1s后控制台输出111，2s后输出222，3S后输出333

    //回调地狱 ,回调次数多了，造成代码读写困难，执行效率也低
    // setTimeout(()=>{
    //     console.log(111);
    //         setTimeout(()=>{
    //                 console.log(222);
    //                     setTimeout(()=>{
    //                         console.log(333);
    //                     },3000)
    //         },2000)
    // },1000)

    //利用生成器产生异步调用,结局回调地狱问题
    // function one () {
    //     setTimeout(()=>{
    //         console.log(111);
    //     },1000);
    //     iterator.next();  
    // }

    // function two () {
    //     setTimeout(()=>{
    //         console.log(222);
    //     },2000);
    //     iterator.next(); 
    // }

    // function three () {
    //     setTimeout(()=>{
    //         console.log(333);
    //     },3000);
    //     iterator.next();  
    // }

    // function * gen (){

    //     yield one();
    //     yield two();
    //     yield three();

    // } 
    // let iterator = gen();
    // iterator.next();
   
    //4.模拟获取  用户数据 订单数据 商品数据

    function  geUsers (){
        setTimeout(()=>{
            let data = '用户数据';
            //调用next方法，并且将数据传入
            iterator.next(data);
            //这是第二次调用next方法,传入的数据将作为上一个yield的返回值
        },1000);
        
    }

    function getOrders(){
        setTimeout(()=>{
            let data = '订单数据';
            iterator.next(data);
        },1000);
        
    }

    function getGoods(){
        setTimeout(()=>{
            let data = '商品数据';
            iterator.next(data);
        },1000);
        
    }

    function * gen(){
       let users = yield geUsers();
       console.log(users);
       let orders = yield getOrders();
       console.log(orders);
       let goods = yield getGoods();
       console.log(goods);
    }

    //调用生成器函数
    let iterator = gen();
        iterator.next();

</script>
```

## 十三，promise(重要)

Promise是ES6引入的异步编程新解决方案。语法上Promise是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。
1) Promise构造函数：promise(excutor){}
2) Promise.prototype.then方法
3）Promise.prototype.catch方法

```javascript 
<script>
    //1.Promise基本语法
    //实例化 Promise对象  对象有三个状态：初始化，成功，失败
    const  p = new Promise(function (resolve, reject) {
        // resolve和reject这两个参数可以自己定义名称
        setTimeout(function () {
            // let data = '数据库中的用户数据';
            
            // resolve(data);    //P状态设置为成功  

            let err = '数据读取失败';
            reject(err);     //p状态设置为失败
        },1000);
    });
    //调用promise对象的then方法，数据调用成功的时候resolve会调用then方法的第一个回调函数，
    //数据调用失败的时候，reject会调用then方法的第二个回调函数
    p.then(function(value){
        console.log(value);
    },function(reason){
        console.error(reason);
    });
//2.用promise封装读取文件操作
//3.封装AJAX操作

//4.promise.prototype.then
//创建promise对象
const p = new Promise((resolve, reject) =>{
        setTimeout(()=>{
            //resolve('用户数据')；
            reject('出错啦');
        },1000)
})


//调用then方法 then 方法的返回结果是promise对象，对象状态由回调函数执行结果决定
//1）如果回调函数中返回结果是非promise类型的属性，状态为成功，返回值为对象的成功的值
const reasult = p.then(value=>{

    console.log(value);
    //1.非promise类型的属性,默认返回为
    //return 'iloveyou';
    //2.是promise对象
    // return new Promise((resolve, reject) =>{
    //         // resolve('ok');   由返回的结果决定Promise对象状态
    //         reject('error');
    //     });
    //3.抛出错误
    //throw new Error('出错了！');
    //throw '出错了！'

},reason=>{
    console.log(reason);
});

console.log(reasult);

//链式调用   可以是任务一步步推进执行，避免回调地狱
    // p.then(value=>{
    //     //嵌套异步任务
    // }).then(reason=>{
    //     //嵌套异步任务
    // })

//5.promise封装多文件读取任务方法

//6.promise的catch方法

const p = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        //设置p对象的状态为失败，并设置失败的值
        reject('出错啦');
    },1000)
});


//调用catch方法返回失败状态
p.catch(function(reason){
    console.warn(reason);
});

</script>
```

## 十四，Set

 ES6提供了新的数据结构Set（集合）.它类似与数组，但成员的值都是唯一的（遇到重复值，会自动去重），集合实现了iterator接口，所以可以使用扩展运算符和for..of进行遍历，集合的属性和方法：
 1）size   返回集合的元素个数
 2）add    增加一个新元素，返回当前集合
 3）delete    删除元素，返回boolean值
 4）has    检测集合中是否包含某个元素，返回boolean值

```javascript 
 <script>
    //1.声明一个set
    // let s = new Set();
    // let s2 = new Set(['大事儿','小事儿','好事儿','坏事儿','小事儿']);

    //元素个数
    // console.log(s2.size);
    //添加新的元素
    //s2.add('喜事儿');
    //删除元素
    //s2.delete('坏事儿');
    //检测
    //console.log(s2.has('糟心事'));
    //清空
    //s2.clear();
    //console.log(s2);

    // for (let v of s2){
    //     console.log(v);
    // }

    //2.Set 实践
    
    //1)数组去重
        // let arr = [1,2,3,4,5,4,3,2,1];
        // let s = [...new Set(arr)];
        // console.log(s);
    //2)交集
    // let arr1 = [1,2,3,4,5,6,7,8],
    //     arr2 = [4,5,6,7,8,9,10];
   
    // let s1 = [...new Set(arr1)].filter(item => {
    //     let s2 = new Set(arr2);
    //     if (s2.has(item)){
    //         return true;
    //     }else{
    //         return false;
    //     }
    // });
    // console.log(s1);
    //简写为
    // let s1 = [...new Set(arr1)].filter(item => new Set(arr2).has(item));
    // console.log(s1);


    //3)并集
    // let arr1 = [1,2,3,4,5];
    // let arr2 = [11,12,13,14,15,14]; 
    // let s = new Set([...arr1,...arr2]);
    // console.log(s);

    //4)差集
    // let arr1 = [1,2,3,4,5,6,7,8],
    //     arr2 = [4,5,6,7,8,9,10];
   
    // let diff = [...new Set(arr1)].filter(item => !(new Set(arr2).has(item)));
    // console.log(diff);

</script>
```


## 十五，Map
  ES6提供了MAP数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包阔对象）都可以当作键。MAP也实现了iterator接口，所以可以使用扩展运算符和for..of进行遍历。MAP的属性和方法：
1) size 返回MAP的元素个数
2）set 增加ige新的元素，返回当前MAP
3）get 返回键名对象的键值
4) has 检测map中是否包含某个元素，返回boolean值
5）clear 清空集合，返回undefined

```javascript 
<script>
    //声明Map
    let m = new Map();
    //添加元素
    m.set('name','尚硅谷');
    m.set('change',function(){
        console.log('我们可以改变你！');
    });
    let key = {
        school : 'ATGUIGU'
    }
    m.set(key,['北京','上海','深圳']);
    
    //大小
    console.log(m.size);

    //删除
    //m.delete('name');

    //获取
    // console.log(m.get('change'));
    // console.log(m.get(key));

    //清空
   // m.clear();

    //遍历
    for (let v of m){

        console.log(v);
    }

    console.log(m);
</script>
```

## 十六，class类

ES6提供了更接近传统语言的邪恶发，引入了class这个概念，作为对象的模板。通过class关键字，可以定义类。基本上，ES6的class可以看作这是一个语法糖，他的绝大部分功能，ES5都可以做到，新的class写法这是让对象原型的写法更加清晰，更像面向对象编程的语法而已。
知识点：
1）class声明类
2）constructor定义构造函数初始化
3）extends继承父类
4）super调用父级构造方法
5）static定义静态方法和属性
6） 父类方法可以重写

```javascript 
<script>
    //1.类声明
    //手机
    // function Phone(brand,price){
    //     this.brand = brand;
    //     this.price = price;
    //     this.call = function (){
    //         console.log('我可以打电话');
    //     }
    // }
    // //添加方法
    // Phone.prototype.weixin = function () {
    //     console.log('我可以使用微信');
    // }

    // //实例化对象
    // let Huawei = new Phone('华为','5999');
    // Huawei.call();
    // Huawei.weixin();
    // console.log(Huawei);


    //class
    // class Shouji {
    //     //构造方法，固定写法不可改名  new的时候实例化对象调用constructor方法
    //     constructor(brand,price){
    //         this.brand = brand;
    //         this.price = price;
    //     }
    //     //方法必须使用该写法，不能使用ES5的对象完整形式
    //     call(){
    //         console.log('我可以打电话！');
    //     }
    // }

    // let Oneplus = new Shouji('1+','1999');
    // Oneplus.call();
    // console.log(Oneplus); 


    //2.静态成员
        // function Phone(){

        // }

        // Phone.name ='手机';
        // Phone.zhifubao = function () {
        //     console.log('我可以使用支付宝');
        // }

        // Phone.prototype.size = '5.5inch';

        // let nokia = new Phone();
        // console.log(nokia.name);  //  undefined   因为name和change是属于构造函数Phone对象的属性和方法， 是Phone对象私有的，不属于实例化对象，
        // nokia.change();   // undefined     与实例化对象无关。只有phone原型对象里的属性和方法才与实例化对象有关
       // console.log(nokia.size);
       

       //静态属性
        // class Shouji{
        //     static name = '手机';   //静态成员  属于类不属于实例对象
        //     static change = function () {
        //         console.log('我可以改变世界');
        //     }
        // }

        // let nokia = new Shouji();
        //  console.log(nokia.name);  // undefined
        // // nokia.change();   // not a function
        // console.log(Shouji.name);   //手机
    //3. 对象继承   ES5继承
    // //手机
    // function Phone(brand,price){
    //     this.brand = brand;
    //     this.price = price;
    // }   

    // Phone.prototype.callphone = function (){
    //     console.log('我可以打电话');
    // }
    // function Smartphone(brand,price,color,size){
    //     Phone.call(this,brand,price);
    //     this.color = color;
    //     this.price = price;
    // }

    // //设置子级构造函数的原型
    // Smartphone.prototype = new Phone();
    // Smartphone.prototype.constructor = Smartphone;
    
    // //声明子类的方法
    // Smartphone.prototype.photo = function () {
    //     console.log('我可以拍照');
    // }

    // Smartphone.prototype.playgame = function () {
    //     console.log('我可以玩游戏');
    // }

    
    // const chuizi = new Smartphone('锤子','1999','white','6.5inch');
    // console.log(chuizi);

    //4.类继承 ES6继承
    // class Phone {
    //     constructor(brand,price){
    //         this.brand = brand;
    //         this.price = price;
    //     }
    //     //父类的成员属性
    //     callphone (){
    //         console.log('我可以打电话');
    //     }
    // }

    // class Smartphone extends Phone{
    //     //构造方法
    //     constructor(brand,price,color,size){
    //        super(brand,price);   //使用super关键字调用父类的constructor函数，相当于Phone.call(this,brand,price)方法
    //         this.color = color;
    //         this.size = size;
    //     }
    //     playgame (){
    //         console.log('我可以玩游戏');
    //     };
    //     photo (){
    //         console.log('我可以拍照');
    //     };
    //     //子类对父类方法的重写   不允许子类直接调用父类的方法
    //     callphone(){
    //         console.log('我可以视频通话');
    //     }

    // }

    // let moto = new Smartphone('摩托罗拉',1999,'red','6.5inch');
    // console.log(moto);

    // moto.callphone();
    // moto.playgame();
    // moto.photo();

    //4.class的get 和set方法  对对象的属性进行方法的绑定
    class Phone {
        //类中不能定义字面量
        static value = '0';
        set price(value1){ 
            this.value = value1;
           console.log('这个价格被修改了');
        }

        get price(){     //给price这个属性绑定一个方法读取price的属性值
            console.log('价格属性被读取了');
            return this.value;    //函数的返回值就是price这个属性的值
        }
 
    }
    //实例化对象
    let s = new Phone();
    
     s.price = 500;  //设置属性值
     console.log(s.price);   //获取属性值

</script>
```

## 十七，数值扩展
## 十八，对象方法扩展

```javascript 
<!-- <script>
    //1.Object.is  判断两个值是否完全相等
    // console.log(Object.is(120,120));   //功能类似于===,不同的地方在于对NaN的比较
    // console.log(Object.is(NaN,NaN));    //true
    // console.log(NaN===NaN); //false,NaN与任何一个数都不全等，包括自己

    //2.Object.assign   对象的合并

    const config1 = {
        host: "localhost",
        port: 3306,
        name: "root",
        pass: "root",
        test: 'test'
    };

    const config2 = {
        host: 'http://www.google.com',
        port: 3306,
        name: 'google',
        pass: 'iloveyou',
        test2: 'test2'
    }

    console.log(Object.assign(config1,config2));  //有相同的属性，第二个对象会把第一个对象的覆盖，不相同的则不会

    //3.Object.setPrototypeOf   设置原型对象 Object.getPrototypeOf
    const school = {
        name: '尚硅谷'
    }
    const cities = {
        xiaoqu : ['北京','上海','深圳']
    }

    Object.setPrototypeOf(school,cities);     //设置school对象的原型对象为cities
    console.log(Object.getPrototypeOf(school));
    console.log(school);
</script> -->
```

## 十九，模块化
    模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来

    模块化的好处：
    模块化的优势有以下几点：
    1） 防止命名冲突
    2） 代码复用
    3）高维护性

    模块化规范产品
    ES6之前的模块化规范有：
    1）CcommonJS => NodeJS Browserify
    2) AMD => requireJS
    3) CMD => seaJS

    ES6模块化语法
    模块功能主要由两个命令构成：export和import
    export命令用于规定模块的对外接口
    import命令用于输入其他模块提供的功能

```javascript
//分别暴露
//m1.js
export let school ='尚硅谷';
//export关键字对外暴露数据
export function teach(){
    console.log('我可以教课！');
}
```

```javascript
//统一暴露
//m2.js
let school = '尚硅谷';

function findjob(){
    console.log('我们可以帮你找工作');
}

//使用export关键字对外暴露数据
export {school,findjob};

```
```javascript
//默认暴露写法
//m3.js
export default {
    school: '尚硅谷',
    change: function(){
        console.log('我们可以改变你');
    }
}
```
```javascript
<script type="module">
   //1.通用的导入方式
    //引入m1.js模块内容
    import * as m1 from "./js/m1.js";
    console.log(m1);

    //引入m2.js模块内容
    import * as m2 from "./js/m2.js";
    console.log(m2);

    //引入m3.js模块内容
    import * as m3 from "./js/m3.js";
    console.log(m3);
    m3.default.change();   //引用函数的时候需要添加一层default结构

    //2.解构赋值形式引入
    import {school,teach} from "./js/m1.js";
    import {school as guigu,findjob} from "./js/m2.js";   //使用as给重名的school起的别名
    import {default as m3} from "./js/m3.js";    //导入默认暴露的时候必须使用as起一个别名

    //3.简便形式  针对默认暴露
    import m3 from "./js/m3.js";
    console.log(m3);
</script>
```

模块化在浏览器中的另外一种写法：

```javascript
//app.js   JS的入口文件

//模块引入
import * as m1 from "./m1.js";
import * as m2 from "./m2.js";
import * as m3 from "./m3.js";

console.log(m1);
console.log(m2);
console.log(m3);
```

```javascript
<script src="./js/app.js" type='module'></script>
```

babel对ES6模块化代码转换
```javascript
<script>
    // 1.安装工具babel-cli babel-preset-env browserify(实际开发用webpack，需要额外配置)
    //安装nodejs
    //npm init --yes
    //npm i babel-cli babel-preset-env browserify -D
    //2.npx babel src/js -d dist/js --preset=babel-preset-env(全局安装去掉npx)
    //3.打包 npx browserify dist/js/app.js -o dist/bundle.js  //打包成bundle.js文件
</script>
```

ES6模块化引入NPM包
```javascript
//入口文件

//模块引入
import * as m1 from "./m1.js";
import * as m2 from "./m2.js";
import * as m3 from "./m3.js";

//命令行安装jquery
//npm i jquery

//修改背景颜色为粉色
import $ from 'jquery';     //引入npm包-jquery
$('body').css('background','pink'); 
//重新打包下文件
```

## 二十， ES7新特性
 1）Array.prototype.includes
 includes方法用来检测数组中是否包含某个元素，返回布尔类型值
 2) 指数操作符
 在es7中引入指数操作符**，用来实现幂运算，功能与math.pow结果相同

```javascript
<script>
    //includes
    const mingzhu = ['西游记','红楼梦','三国演义','水浒传'];

    //判断
    console.log(mingzhu.includes('西游记'));    //有该值返回true
    console.log(mingzhu.includes('金瓶梅'));    //无该值返回false

    //**
    console.log(2**10);
    console.log(Math.pow(2,10));    //效果类似于该方法
</script>
```

## 二十一，ES8新特性
async和await两种语法结合可以让异步代码像同步代码一样
1） async函数
    1.async函数的返回值为promise对象，
    2.promise对象的结果由async函数执行的返回值决定
```javascript
<script>
    //async函数
    async function fn(){
        //返回一个字符串
        //return '尚硅谷'
        //只要返回的不是一个promise类型的对象,则这个函数返回的对象就是一个成功的promise类型对象
        //return;   //哪怕什么都不返回，函数返回的也是一个promise对象
        //抛出错误，返回的结果是一个失败的Promise
        throw new Error('出错啦');
        //返回的结果是一个Promise对象
        return new Promise((resolve, reject)=>{
            resolve('成功的数据');  //返回的是成功的值，fn函数返回的promise对象也是成功的值

            //reject('失败的错误');
        })
    }
    const result = fn();
   // console.log(result);

   result.then((value=> {
       console.log(value);
   },reason=>{
        console.warn(reson);
   }))

</script>
```
2) await表达式
    1.await必须写在async中
    2.await右侧的表达式一般为promise对象
    3.await返回的是promise成功的值
    4.await的promise失败了，就会抛出异常，需要通过try...catch捕获处理

```javascript
<!-- <script>
    //创建promise对象
    const p = new Promise((resolve, reject)=>{
        resolve('用户数据');

    })

    //await 要放在async函数中
    async function main() {
        try{
            let reasult = await p;   //返回的值就是对象的值--用户数据
            console.log(result);
        } catch(e){
            console.log(e);
        } 
    }

    //调用函数
    main();
</script> -->
```

读取文件
```javascript
<!-- <script>
    //需安装nodejs环境
    //1.引入fs模块
    const fs = require('fs');

    //读取例子
    function readLizi1(){
        return new Promise((resolve, reject)=>{
            fs.readFile("./resource/例子1.md",(err,data)=>{
                //如果失败
                if (err) reject(err);
                //如果成功
                resolve(data);
            })
        })
    }

    function readLizi2(){
        return new Promise((resolve, reject)=>{
            fs.readFile("./resource/例子2.md",(err,data)=>{
                //如果失败
                if (err) reject(err);
                //如果成功
                resolve(data);
            })
        })
    }

    function readLizi3(){
        return new Promise((resolve, reject)=>{
            fs.readFile("./resource/例子3.md",(err,data)=>{
                //如果失败
                if (err) reject(err);
                //如果成功
                resolve(data);
            })
        })
    }


    //声明一个async函数
    async function main(){
            //获取例子1内容
                let lizi1 = await readLizi1();
            //获取例子2内容
                let lizi2 = await readLizi2();
            //获取例子3内容
                let lizi3 = await readLizi3();

            console.log(lizi1.toString());
            console.log(lizi2.toString());
            console.log(lizi3.toString());
    }

    main();
</script> -->
```

发送AJAX请求
```javascript
<!-- <script>
    //发送AJAX请求 ,返回的结果是Promise对象
    function sendAJAX(url){
        return new Promise((resolve,reject)=>{
            //1.创建对象
            const x = new XMLHttpRequest();
            //2.初始化
            x.open('get',url);
            //3.发送
            x.send();
            //4.事件绑定
            x.onreadystatechange = function(){
                if (x.readyState ===4){
                    if (x.status >= 200 && x.status < 300){
                        //成功啦
                        resolve(x.response);
                    }else{
                        //如果失败
                        reject(x.status);
                    }
                }
            }
        })
       
    }

    // //promise then 方法测试
    // sendAJAX('www.baidu.com').then(value=>{
    //         console.log(value);
    // },reason=>{})

    //async 与await测试
    async function main(){
        //发送AJAX请求
        let result = await sendAJAX('www.baidu.com');
        //再次测试
        let tianqi = await sendAJAX("https://weathernew.pae.baidu.com/weathernew/pc?query=%E6%B2%B3%E5%8D%97%E9%83%91%E5%B7%9E%E5%A4%A9%E6%B0%94&srcid=4982");
        console.log(tianqi);
    }
</script> -->
```

## 二十二，ES8对象方法扩展
1）Object.values()方法返回一个给定对象的所有可枚举属性值的数组
2) Object.entries()方法返回一个给定对象自身可遍历属性[key,value]的数组
3） Object.getOwnPropertyDescriptors()方法返回指定对象所有自身属性的描述对象
```javascript
<script>
    //声明对象
    const school = {
        name: '尚硅谷',
        cities: ['北京','上海','深圳'],
        xueke: ['前端','java','大数据','运维']
    }

    //获取对象所有的键
    console.log(Object.key(school));
    //获取对象所有的值
    console.log(Object.values(school));
    //获取对象所有的键和值
    console.log(Object.entries(school));
    //创建MAP
    const m = new Map(Object.entries(school));
    console.log(m.get('cities'));

    //对象属性的描述对象
    console.log(Object.getOwnPropertyDescriptor(school));
    const obj = Object.create(null,{       //配置属性的属性描述对象
            name:{
                //设置值
                value:'尚硅谷',
                //属性特性
                writable:true,    //可写
                configurable:true,    //可配置
                enumerable:true      //可枚举
            }
    })
</script>
```

## 二十三，ES9扩展运算符与rest参数
    Rest参数与spread扩展运算符在ES6中已经引入，不过ES6中只针对数组，
    在ES9中为对象提供了像数组一样的rest参数和扩展运算符

```javascript
<script>
    // function connect({host,port,...user}) {
    //     console.log(host);
    //     console.log(port);
    //     console.log(user);
    // }

    // connect({
    //     host : '127.0.0.1',
    //     port : 3306,
    //     username : 'root',
    //     password : 'root',
    //     type : 'master'
    //     });

    const skill1 = {
        q:'天音破'
    }

    const skill2 = {
        w:'金钟罩'
    }

    const skill3 = {
        e:'天雷破'
    }

    const skill4 = {
        r:'猛龙摆尾'
    }

    const mangseng = {...skill1, ...skill2, ...skill3, ...skill4};
    console.log(mangseng);
</script>
```

## 二十四，ES9正则扩展

```javascript
<script>
    //1.命名捕获分组
    //声明一个字符串
    // let str = '<a href="www.baidu.com">百度</a>';

    // //提取URL与标签文本
    // const reg = /<a href="(.*)">(.*)<\/a>/;

    // //执行
    // const result = reg.exec(str);
    // console.log(result);     //执行结果groups为undefined
    
     //命名捕获分组   
    // let str = '<a href="www.baidu.com">百度</a>';
    // const reg = /<a href="(?<url>.*)">(?<text>.*)<\/a>/;
    // const result = reg.exec(str);
    // console.log(result);   //groups里分组  url  text

    //2.反向断言
        // let str = '454545454你知道吗555啦啦啦';
        // //正向断言
        // //const reg =  /\d+(?=啦)/;
        // //const result = reg.exec(str);

        // //反向断言
        // const reg = /(?<=么)\d+/;    //判断数字前面是不是么字
        // const result = reg.exec(str);
        // console.log(result);

    //3.dotALL模式
        //dot  .  元字符，除换行符以外的任意单个字符
        // let str = `<ul>
        //     <li>
        //     <a>肖生克的救赎</a> 
        //     <p>上映日期:1994-09-10</p>
        //     </li>
        //     <li>
        //         <a>阿甘正传</a> 
        //     <p>上映日期:1994-07-16</p>
        //     </li>
        //     </ul>`;
        
        //声明正则     以前的写法
        // const reg = /<li>\s+<a>(.*?)<\/a>\s+<p>(.*?)<\/p>/;    //需要加换行符\s
        // //执行匹配
        // const result = reg.exec(str);
        // console.log(result);

        //现在DOT-ALL模式  
        // const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/s;     //加入模式修正符s
        // const result = reg.exec(str);
        // console.log(result);

        // const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs;     //加入模式修正符s  加入全部模式g
        // let result;
        // let data = [];
        // while(result = reg.exec(str)){
        //     console.log(result);
        //     data.push({title:result[1],time:result[2]});
        // }
        // //输出结果
        // console.log(data);
   
</script>
```

## 二十五，  ES10新特性
```javascript
<!-- <script>
     //1.Object.fromEntries    参数为二维数组或者map对象  将二维数组转为对象
    //二维数组
    // const result = Object.fromEntries([
    //     ['name','尚硅谷'],
    //     ['xueke','JAVA,大数据，前端，云计算']
    // ]);

    // //Map
    // const m = new Map();
    // m.set('name','ATGUIGU');
    // const result = Object.fromEntries(m);
    
    // //ES8中的   Object.entries方法,将对象转为二维数组，相当于Object.fromEntries逆运算
    // const arr = Object.entries({
    //     name : '尚硅谷'
    // })
    // console.log(arr);

    //2.trimStart与trimEnd  用来清除字符串左右两边的空白
    // let str = '      我爱你     ';
    // console.log(str);
    // console.log(str.trimStart());
    // console.log(str.trimEnd());

    //3.flat与flatMap
    //将多维数组转化为低位数组
    //const arr = [1,2,3,[5,6]];
    //const arr = [1,2,3,4,[5,6,[7,8,9]]];
    //参数为深度，是一个数字
    //console.log(arr.flat(2));   //参数2将三维数组转为一维数组。默认参数为1，只能将三维数组转为二维数组

    //flatMap
    // const arr = [1,2,3,4];
    // const reasult = arr.flatMap(item => [item*10]);    //返回的结果如果是一个多维数组，可以用flatMap变成一维数组
    // console.log(result);

    //4.Symbol.prototype.description
    //创建symbol
    let s = Symbol('尚硅谷');

    console.log(s.description);
 </script> -->
```

## 二十六，ES11新特性

```javascript

```

