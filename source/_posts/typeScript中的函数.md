---
title: typeScript中的函数
date: 2019-09-03 15:15:11
tags:
    - typeScript
---

ES5中函数的定义方法
函数声明
`function run () { return 'fun'}`
匿名函数
`var fun = function () { return 'fun'}`


### 1.ts中定义函数的声明方法
定义了函数返回的类型，返回值必须是对应该类型的值
```yaml
// 1.函数声明
function fun3 ():string {
    return '123'
}
alert(fun3())

// 2.匿名函数
var fun4 = function():number {
    return 666
}

alert(fun4())
```

### 2.ts中定义方法传参
转入参数类型必须对应, 返回类型也是
```yaml
# 1.函数声明
function getInfo(name:string, age:number):string {
    return `my name is ${name}, ${age} yeas old`
}

alert(getInfo('mandy', 18))
# 2.匿名函数
var getInfo2 = function (name: string, age: number): string{
    return `my name is ${name}, ${age} yeas old`
}

alert(getInfo2('mandy', 18))
```
### 3.没有返回值的方法
```yaml
function fun5 ():void {
    console.log('void')
}
```

### 4.方法可选参数
es5里面方法的实参数形参可以不一样，但是ts中必须一样，如果不一样就需要配置可选参数
在形参后面加上?就可以了。 注意：可选参数必须配置到参数的最后面

```yaml
var getInfo3 = function (name: string, age?: number): string{
    return `可选参数------------my name is ${name}, ${age} yeas old`
}

alert(getInfo3('mandy'))
```
### 5.默认参数
```yaml
var getInfo4 = function (name: string, age: number = 18): string{
    return `可选参数------------my name is ${name}, ${age} yeas old`
}

alert(getInfo4('mandy'))

```

### 6.剩余参数 (利用es6的扩展运算符)
```yaml
function sun(...arr: number[]): number{
    var res = 0
    arr.forEach(e=>{
        res = res + e
    })
    return res
}

alert(sun(1,2,3,4))
```

### 7.函数的重载
java中方法的重载：重载指的是两个或者两个以上同名函数，但他们的参数不一样，这时会出现函数重载的情况
typeScript中的重载：通过为同一个函数提供多个函数类型定义来试下多种功能的目的
ts为了兼容es5 以及es6重载的写法和java中有区别
```yaml
function getInfo5 (name:string):string;
function getInfo5 (age:number):number;
function getInfo5 (str: any):any {
    if(typeof str === 'string'){
        return '我叫：'+ str;
    } else {
        return `我的年龄是：${str}`;
    }
}

alert(getInfo5(20))
```