# let 命令
##  基本用法
- 用来声明变量的，es里变量更加灵活，不需要指定类型，只需要let或者var声明即可
```
{
    let a = 10;
    var b = 11;//在代码块也能拿到b，但是无法拿到a
}
```

- let vs var
1、let是局部有效，var是全局有效
```
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6]();//10
//此时的i是全局的，每次循环变量i的值就会发生改变
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6]();//6
//此时的i只在本轮循环有效，每次循环i都是一个新的变量
```

* 注意：for循环设置循环变量的部分是一个父作用域，循环体内部是一个单独的子作用域
```
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
```

## 不存在变量提升
var在声明之前使用，值为undefined
let必须在声明之后使用，否则报错：ReferenceError
```
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;
// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

## 暂时性死区 - temporal dead zone，简称 TDZ
只要会计作用域内存在let或者const命令，它所声明的变量就“绑定”这个区域，不再受外部的影响
```
var tmp = 123;
if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

因为有了暂时性死区，所以typeof不再是一个百分百安全的操作
```
typeof x;//ReferenceError 会报错
let x;

typeof undeclared_variable;// undefined 不会报错
```

有些“死区”比较隐蔽，不太容易发现
```
function bar(x = y, y = 2) {
    return [x, y];
}
bar();// 报错
```
函数bar的参数里，x的默认值等于y，但是y还没有声明，属于“死区”，所以报错

```
function bar(x = 2,y = x){
    return [x, y];
}
bar();// [2, 2]
```
此时不会报错，因为y等于的x，前面已经声明了


```
var x = x;//不报错

let x = x;//报错
// ReferenceError: Cannot access 'x' before initialization
```
上面代码报错，也是因为暂时性死区的问题


## 不允许重复声明
let 不允许在相同作用域内，重复声明同一个变量
```
//报错
function func(){
    let a = 10;
    var a = 1;
}
//报错
function func(){
    let a = 10;
    let a = 1;
}
```

不能在函数内部重新声明参数
```
function func(arg) {
  let arg;
}
func() // 报错
function func(arg) {
  {
    let arg;
  }
}
func() // 不报错
```