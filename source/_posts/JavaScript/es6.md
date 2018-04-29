---
title: es6
categories: JavaScript
tags:
  - es6
  - JavaScript
---



## es6

### let const

#### let

```javascript
let num = 123;

{
  let num = 456;
  console.log(num); //456
}
console.log(num); //123
```

- `let`声明变量 有板块作用域

#### const

- `const` 声明常量 不能重新赋值

### class extends super

```javascript
class People {
  //声明一个类
  constructor(x,y) {
    //实例私有的属性和方法
    this.age = 'yy';
    this.height = y;
  }
  //类共享的方法
  hello(string){
    console.log(this.age+string+this.height);
  }
}
// new 出实例
let boy = new People(50,60);
boy.hello('hello'); //yyhello60

class Son extends People {
  //son 继承 people extends
  constructor() {
    //super() 关键词 子类继承父类的实例的this 属性和方法
    super();
    //子类私有的属性 会覆盖父类的属性或方法
    this.age = '80';
  }
  //类类的方法
}
let son = new Son();
son.hello('123'); //80123undefined
```

### 箭头函数

```
class People {
  constructor() {
    this.age = 60;
    this.height = 70;
  }
  hello(){
    //箭头函数 会绑定我外面的this
    setTimeout(() => {
      console.log(this.age+this.height);
    },100);
  }
}

let one = new People();
one.hello(); //130
```

### template 字符拼接

```javascript
let book = [
  {book:'海贼王'},
  {book:'火影忍者'},
  {book:'死神'},
  {book:'全职猎人'}
];
let html = '';
html = `\
this is ${book[0].book}
this is ${book[1].book}
this is ${book[2].book}
this is ${book[3].book}
`;
// ${ } 声明变量
console.log(html);
```

### 变量匹配

```javascript
let cat = '123';
let dog = '456';
let zoo = {cat,dog};
console.log(zoo); //{cat:'123',dog:'456'}
```

### default rest

#### default 默认值

```javascript
function animal(cat = 'cat') {
  //cat 有默认值
  console.log(cat);
}
animal();
```

#### rest 剩余参数

```javascript
function animal(dog,go,...cat) {
  console.log(dog);
  //...cat ...表示剩余参数 返回一个数组 cat剩余参数的标识符
  console.log(cat);
  console.log(go);
}
animal('123',50,123,456,789);
```