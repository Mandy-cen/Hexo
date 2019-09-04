---
title: typeScript的继承
date: 2019-09-04 11:41:32
tags:
    - typeScript
---

### 1. 定义类
```yaml
class Person {
    name: string  # 属性 前面省略了public关键词
    constructor (name: string) { # 构造函数 实例化的时候触发的方法
        this.name = name
    }
    
    getName(): string {
        return this.name
    }
    
    setName(name:string): void {
        this.name = name
    }
}

var p = new Person('张三') # 实例化
alert(p.getName())

p.setName('mandy')
alert(p.getName())
```

### 2.继承 extends、super

```yaml
class Person {
    name: string
    constructor (name: string) {
        this.name = name
    }

    run(): string {
        return `${this.name} 在运动---------父类`
    }
}

class Web extends Person {
    constructor (name: string) {
        super(name) # 初始化父类构造函数
    }

    work () {
        alert(`${ this.name } 在工作`)
    }

    run (): string {
        return `${this.name} 在运动--------- 子类`
    }
}

var w = new Web('zhangsan') # 实例化子类

w.work()

alert(w.run()) # 在调用子类的方法的时候，首先是从子类里面先找，如果子类没有再到父类里面找

```
### 3.类里面的修饰符
typeScript里面定义属性的时候给我们提供了三种修饰符：
- public 公有          在类里面，子类，类外面都可以访问
- protected 保护类型   在类里面可以访问，在类外部设法访问
- private 私有         在类里面可以访问，子类，类外部都没法访问

属性如果不加修饰符则默认是公有类型

> * public公有

```yaml
class Person{
    public name: string # 公有属性
    constructor (name: string) {
        this.name = name
    }

    run (): string {
        return `${ this.name } 在运动---------父类`
    }
}

class Web extends Person {
    constructor (name: string) {
        super(name)
    }

    work () {
        alert(`${ this.name } 在工作`)
    }

    run (): string {
        return `${ this.name } --------- 子类`
    }
}
# 子类访问
var w = new Web('王五')
w.work()

# 公有属性类外部访问
var p = new Person("张三")
alert(p.name)

```

> * protected 保护类

```yaml
class Person{
    protected name: string #公有属性
    constructor (name: string) {
        this.name = name
    }

    run (): string {
        return `${ this.name } 在运动---------父类`
    }
}

class Web extends Person {
    constructor (name: string) {
        super(name)
    }

    work () {
        alert(`${ this.name } 在工作`)
    }

    run (): string {
        return `${ this.name } --------- 子类`
    }
}
# 当前类 、子类
var w = new Web('李四')
alert(w.run())

# 类外部
var p = new Person('王五')
alert(p.name) # 报错

```

> * private

```yaml
class Person{
    private name: string #公有属性
    constructor (name: string){
        this.name = name
    }

    run(): string {
        return `${ this.name } 在运动---------父类`
    }
}

class Web extends Person {
    constructor (name: string) {
        super(name)
    }

    work() {
        alert(`${ this.name } 在工作`) # 当name为私有属性的时候这里报错
    }
}

# 类外部
var p = new Person('张三')
alert(p.name) # 报错了

#子类
var w = new Web ('李四')
w.work() #访问不到

```

### 4.静态属性  静态方法

```yaml
class Person {
    public name: string
    public age: number = 20
    static sex: string = "man"
    constructor (name: string) {
        this.name = name;
    }

    run () {
        alert (`${ this.name }在运动`)
    }

    static print () { #静态方法没法直接调用类里面的属性，当想要调用类里面的属性的时候需要声明静态的属性
        alert('静态方法'+ this.age + Person.sex)
    }
}

var p = new Person('张三')
p.run()
Person.print() #静态方法调用

```

### 5.多态
父类定义一个方法不去实现，让继承他的之类去实现 每一个子类有不同的表现

```yaml
class Animal {
    public name: string
    constructor (name: string) {
        this.name = name
    }

    eat () { # 具体方法怎么做，让继承他的子类去实现，每一个子类的表现不一样
        alert("吃的方法")
    }
}


class Dog extends Animal {
    constructor (name: string){
        super(name)
    }
    eat () {
        return this.name + '吃肉'
    }
}
class Cat extends Animal {
    constructor (name: string){
        super(name)
    }
    eat () {
        return this.name + "吃老鼠"
    }
}

```

### 6. 抽象类
typeScript中的抽象类：他是提供其他继承的基类，不能直接被实例化
用abstract关键字定义抽象类和抽象方法，抽象中的的抽象方法不包含具体实现并且必须在派生中实现
abstract抽象方法只能放在抽象类里面
抽象类和抽象方法用来定义标准，标准：Animal 这个类要求他的子类必须包含eat方法

```yaml
abstract class Animal {
    public name: string
    constructor (name: string) {
        this.name = name
    }
    abstract eat(): any #抽象方法不包含具体实现并且必须在派生中实现
}

class Dog extends Animal {
    constructor (name: string) {
        super(name)
    }
    # 抽象类的子类必须实现抽象类里面的抽象方法
    eat () {
        console.log(this.name + "吃粮食")
    }
}

var dog = new Dog('潘多拉')
dog.eat()

```