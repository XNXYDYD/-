#ES6学习笔记

1.变量/赋值
  var     可以重复定义、不能限制修改、没有块级作用域

  let     不能重复定义、用于定义变量、块级作用域 
            let存在暂时性死区；
例:
```javascript
  let  a = 10;
  let b = function () {
        alert(a);//块级作用域外有一个全局a，又再块级作用域内重新定义了一个a，导致a失去了指针，最后这里弹出a会报错，这种情况称之为暂时性死区
        let a=99;
        alert(a);
    }
    
```
  const   不能重复定义、用于定义常量、块级作用域

2、解构赋值：
  1.左右两边必须一样；右边得是个东西
  2.必须定义和赋值同步完成
  
  例：
  ```javascript
  let [a,b] = [1,2];//结构赋值左右结构要一致，类型也要一致
  console.log('a:',a,'b:',b);
  ```
  ###3.函数
箭头函数
1.如果有且仅有1个参数，()可以省
2.如果函数体只有一句话，而且是return，{}可以省
*关于this： 
箭头函数中没有this，在箭头函数中使用this，this指向上一级的对象；
例:
```javascript
//普通函数
let a = function (b) {
  return b+10;
};
//箭头函数
let b = (a) =>{
    return a+10;
};
//因为参数只有一个，()可以省略
let c = a=>{
    return a+10;
};
//因为函数体内只有一条语句，{}可以省略，return也可以省略
let d = a => a+10;
```
      
**默认参数**
  (a=xx, b=xx, c=xx)
  ```javascript
let fn = (a=5,b=10)=>{
    console.log(a+b);
};
fn();//15
```
      
参数展开(剩余参数、数组展开)
1.“三个点”的第1个用途：接收剩余参数
    function show(a, b, ...名字)
    剩余参数必须在参数列表的最后
```javascript
    function show(a,b,...args) {
      console.log(...args);
    }
    show(1,2,3,4,5,6,7);//3 4 5 6 7
```

2.“三个点”的第2个用途：展开一个数组
```javascript
    function show(a,b,...args) {
      console.log([...args]);
    }
show(1,2,3,4,5,6,7);
```
3.数组/json
数组——5种
map     映射：一个对一个
[18, 67, 98, 25, 17, 96] => [false, true, true, false, false, true]
```javascript
let arr = [18, 67, 98, 25, 17, 96];
let res = arr.map((item,index)=>{
    console.log(index,item);
    if(item>=60){
        return true;
    }else {
        return false;
    }
});
console.log(res);//[false, true, true, false, false, true]
```

reduce  汇总：一堆->一个 (可用于汇总，求平均值等)
```javascript
//Array.reduce(function(returnVal,currentVal,index,arr){},initNumber)
let arr=[12,5,88,37,21,91,17,24];
//汇总
let b = arr.reduce(function(a,b,c) {
    return a+b;
});
console.log(b);
let arrAvg=[12,5,88,37,21,91,17,24];
let avg = arrAvg.reduce(function(tem,item,index) {
    if(index<arrAvg.length-1){
        return tem+item;
    }else {
        return (tem+item)/arrAvg.length;
    }
});
console.log(avg);

```

filter  过滤（返回符合条件的数组）：
[12,5,88,37,21,91,17,24]
```javascript
//filter（）方法可以筛选符合条件的值
let filterArr = [12,5,88,37,21,91,17,24];
let filterVal = filterArr.filter(item =>{
     if(item>20){
         return item;
     }
});
console.log(filterVal);

```
forEach 遍历：
```javascript
let each = [12,5,88,37,21,91,17,24];
each.forEach((item,index)=>{
    console.log(index,item);
});
```
Array.from([array-like])=>[x,x,x];
Array.from() 可以将类数组转化为数组

json——2变化
1.简写：名字和值一样的，可以省
```javascript
let a=12;
let b=5;
let json = {
    a,
    b
};
console.log(josn);
```
2.function可以不写,(json的缩写)
```javascript
let obj = {
    a:12,
    v:11,
    show(){
        console.log(this.a+this.v);
    }
};
obj.show();//23
```
   2）、startsWith(); ===> 检测字符串的开始；
   3）、endsWith(); ===> 检测字符串的结尾；
```javascript
//检测手机号码是否以
  if(sNum.startsWith('135')){
    alert('移动');
  }else{
    alert('联通');
  }
//检测文件类型
  if(filename.endsWith('.txt')){
    alert('文本文件');
  }else{
    alert('图片文件');
  }
```
5.面向对象
  class/constructor ===》class定义类，constructor定义类的属性
  extends/super ===》extends 继承关键字,会继承父类的方法 ；super ==》继承超类（父类）的属性
  ```javascript
  //定义一个类
class Person{
    //定义类的属性
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    showName(){
        alert(this.name);
    }
    showAge(){
        alert(this.age)
    }
}
//继承,
class Worker extends Person{
    constructor(name,age,job){
        super(name,age);
        this.job = job;
        
    }   
}
let w =new Worker('张三',16,'学生');
    w.show();
    w.showJob();

```

普通函数：根据调用我的人  this老变
箭头函数：根据所在的环境  this恒定

bind——给函数定死一个this
```javascript
function show() {
  console.log(this);
}
document.onclick = show.bind('alert');//alert
```

6、promise,generator，async/await

promise：解决异步操作
Promise.all();      与：所有的都成功
Promise.race();     或：只要有一个完成
优点——解除异步操作
局限——带逻辑的异步操作麻烦


```javascript
let p = new Promise((resolve,reject)=>{
            $.ajax({
                url:'./api/a.txt',
                success(data){
                    resolve(data)
                },
                fail(res){
                    reject(res);
                }
            })
        });
let p2 = new Promise((resolve,reject)=>{
    $.ajax({
        url:'./api/j.json',
        success(data){
            resolve(data)
        },
        fail(res){
            reject(res);
        }
    })
});
//一起执行请求，但没有办法保证执行的顺序，当逻辑复杂时没办法处理
Promise.all([p,p2]).then(data=>{
    
    let [n,j] = data;
    console.log(n,j);
},err=>{
    console.log(err)
});
```
generator-生成器
能暂停
yield 有两个作用：
1.参数      function (a, b, c)
2.返回      return
```javascript
    function *show(){
      alert('aaa');
      yield 55;
      alert('bbb');
      return 89;
    }
    let gen=show();

    let res1=gen.next();console.log(res1);    //{value: 55, done: false}

    let res2=gen.next();console.log(res2);    //{value: 89, done: true}
```
generator+promise配合使用，但又以下两个缺点：
1.外来的runner辅助执行——不统一、不标准、性能低
2.generator函数不能写成箭头函数(=>)

async/await:可以将异步操作变成同步操作的形式，也可以进行复杂的逻辑，是最优的解决方案

```javascript
//async 定义关键词
async function show(){
  try{
        let data1=await $.ajax({url: '1.txt', dataType: 'json'});
    
        if(data1.a+data1.b<10){
        let data2=await $.ajax({url: '2.txt', dataType: 'json'});
    
        alert(data2[0]);
    }else{
        let data3=await $.ajax({url: '3.txt', dataType: 'json'});
    
        alert(data3.name);
    }
  }catch(e){
    alert('有问题');
    throw new Error('我错了....');
  }
}
```



