---
title: typeScript的泛型
date: 2019-09-04 18:54:39
tags:
    - typeScript
---
我们不仅要创建一致的定义良好的API，同时也要考虑可重用性。组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。
在像c#和java这样的语言中，可以使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。这样用户就可以以自己的数据类型来使用组件。
通俗理解：泛型就是解决 类 接口 方法的复用性、以及对不特定数据类型的支持

### 1.泛型的定义
```yaml
首先看一下ts函数的定义
function getData(value: string): string { // 传入值和返回值都限制了string类型
    return 'str'
}

需要同时返回string类型和number类型时   any可以解决这个问题

function getData (value: any):any { // 传入参数类型和返回值类型可以不一致
    return value
}

getData(123)
getData('str')

但是用了any就代表着放弃了类型的检查，这时当我们需要传入什么，就返回什么类型的数据就行不通了
这个问题可以通过泛型类实现， 它可以支持不特定的数据类型。


function getData <T>(value: T): T{ //T表示泛型（也可以取其他名字），具体什么类型是调用这个方法的时候决定的
    return value
}

// getData<number>('eeee') //错误写法
getData<number>(123) //错误写法

当然，如果想返回任意类型的值可以用any
function getData<T>(value: T):any {
    return '11222'
}
getData<number>(123);// 传入参数必须是number
```

### 2. 泛型类
比如有最小堆算法，需要同时支持返回数字和字符串两种类型。通过类的泛型来实现

```yaml

class myClass {
    public list: number[] = [];
    add (num: number){
        this.list.push(num)
    }

    min () : number{
        var min=arr[0];
        list.forEach((value)=>{
            if(value<min){
                min=value
            }
        })
        return min
    }
}
var m = new myClass()
m.add(2);
m.add(3);
m.add(5);
m.add(5);
m.add(7);
m.add(8);
alert(m.min()) //输出了最小值


class myClass<T> {
    public list:T[] = [];
    add (value: T): void {
        this.list.push(value)
    }
    min () : number {
        var min=arr[0];
        list.forEach((value)=>{
            if(value<min){
                min=value
            }
        })
        return min
    }
}


var m = new myClass<number>() //实例化，并且指定了泛型T的类型为number
m.add(2);
m.add(3);
m.add(5);
m.add(5);
m.add(7);
m.add(8);
alert(m.min()) //输出了最大值


```

### 3.泛型接口

```yaml

回顾接口定义
interface Config {
    (value1:string, value2: string): string
}

var setData: Config = function (val1: string, val2: string): string {
    return val1 + val2
}

alert(setData("name: ", "mandy"))

泛型接口

interface ConfigFn {
    <T>(val: T): T;
}
var getData: ConfigFn  = function<T>(value: T): T{
    return value
}
getData<string>('str')


interface ConfigFn<T> {
    (value:T):T
}

function getData <T>(value: T): T {
    return value
}
var myData:ConfigFn <string> = getData;
myData('2344')

```
