---
title: typeScript的接口 ----笔记
date: 2019-09-04 17:54:39
tags:
    - typeScript
---
在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范。在程序设计里面，接口起到了一定限制和规范的作用。接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部状态数据，也不关心这些类里方法的实现细节，它只规定这批类里必须提供某些方法，提供这些方法就可以满足实际需要。

> * 属性接口
> * 函数类型接口
> * 可索引接口
> * 类类型接口
> * 接口扩展
> * 复杂例子


### 1. 属性接口 对json的约束

```yaml
function printLabel(labelInfo: {label: string}) :void {
    console.log('label')
}
# printLabel('lalall') 错误写法
# printLabel({name: '张三'}) 错误写法
printLabel({label: '张三'})


# 传入对象(必传)约束
interface FullName {
    firstName: string;
    lastName: string
}

function printName(name: FullName) {
    console.log(name.firstName +' '+ name.lastName)
}
var obj = { # 传入的参数必须包含 firstName 和 lastName
    firstName: 'cen',
    lastName: "mandy",
    age: '18'
}
printName(obj)

# 可选属性 

interface FullName {
    firstName: string;
    lastName?: string; # 可选属性（加上问号），可填可不填
}

function getName (name: FullName) {
    console.log(name)
}

getName({
    firstName: 'cen'
})


```
例子: 
```yaml

interface Config {
    type: string;
    url: string;
    data?: string;
    dataType: string;
}

function ajax(config: Config) {
    var xhr = new XMLHttpRequest();
    xhr.open(config.type, config.url, true)
    xhr.send(config.data)
    xhr.onreadystatechange = res=> {
        if(xhr.readyState == 4 && xhr.status == 200){
            console.log('------------成功------------')
            if(config.dataType === 'json'){
                console.log(JSON.parse(xhr.responseText))
            } else {
                console.log(xhr.responseText)
            }
        }
    }
}

ajax({
    type: 'get',
    url: 'xxxx.com',
    dataType: 'json'
})
```
### 2.函数类型接口
对方法传入的参数  以及返回值进行约束
```yaml
#加密的函数类型接口
interface encrypt {
    (key: string, value: string): string
}

var md5: encrypt = function(key: string, value: string): string {
    return key + value
}

alert(md5('name', "zhangsan"))
```
### 3. 可索引接口： 数组、对象的约束 

```yaml
# 数组约束
interface UserArr {
    [index: number]: string
}

var arr:UserArr = ['1234', '345']
console.log(arr[0])
```

```yaml
# 对象约束
interface UserObj {
    [index: string]: string
}

var obj:UserObj = {name: 'ton'}
```

### 4.类类型接口： 对类的约束
```yaml
interface Animal {
    name: string;
    eat(str: string): void;
}

class Dog implements Animal {
    name: string;
    constructor (name: string) {
        this.name = name
    }

    eat () {
        console.log( this.name + '吃粮食')
    }
}

var dog = new Dog('布拉多')
dog.eat()
```
### 5. 接口扩展：接口可以继承接口
```yaml
interface Animal {
    eat(): void;
}

interface Person extends Animal { # 继承Animal接口
    work(): void;
}

class Web implements Person {
    name: string
    constructor(name: string){
        this.name = name
    }
    eat (){
        console.log(this.name + "喜欢吃馒头")
    }
    work () {
        console.log(this.name + "在写代码")
    }
}

var web = new Web('mandy')
web.eat()
```

### 6. 复杂例子
```yaml

#不仅可以继承类同时可以实现接口，而且接口也能继承接口
interface Animal {
    eat(): void;
}

interface Person extends Animal { # 继承Animal接口
    work(): void;
}

class Programmer {
    public name: string;
    constructor(name: string) {
        this.name = name
    }
    coding (code: string){
        console.log(this.name + code)
    }
}

class Web extends Programmer implements Person { 
    constructor(name: string){
        super(name)
    }
    eat (){
        console.log(this.name + "喜欢吃馒头")
    }
    work () {
        console.log(this.name + "在写代码")
    }
}

var web = new Web('mandy')
web.coding("敲代码")

```