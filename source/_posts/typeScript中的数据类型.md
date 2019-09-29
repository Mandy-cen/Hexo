---
title: typeScript中的数据类型
date: 2019-09-03 10:02:08
tags: 
    - typeScript
---
### typeScript中的数据类型
注意：写ts代码必须制定类型（因为ts会类型校验）
> * 布尔类型（boolean）
> * 数字类型（number）
> * 字符串类型（string）
> * 数组类型（array）
> * 元组类型（tuple）
> * 枚举类型（enum）
> * 任意类型（any）
> * null 和 undefined
> * void类型
> * never类型

### 1.布尔类型

```yaml
var flag: boolean = true
flag = false
console.log('boolean:', flag)
```

### 2.数字类型
```yaml
var num: number = 123
num = 666
console.log('number:', num)

num = 'typeScript' #报错。ts会校验数据类型
```

### 3.字符串类型
```yaml
var str: string = 'this is ts'
str = 'lalala'
console.log('string:', str)
```

### 4.数组类型 两种方式

```yaml
# ES5定义数组  var arr = [1,3,4,5]

# 第一种
var arr1: number[] = [1,2,3]
console.log("arr1:", arr1)

# 第二种
var arr2: Array<number> = [4,5,6]
console.log('arr2:', arr2)
```

### 5.元组类型（属于数组的一种）

```yaml
let tup: [number, string] = [666, 'str']
console.log('tup:', tup)
```

### 6.枚举类型
```yaml
enum Status {success=200, error=404}
let f: Status = Status.success
console.log("Status:", f)

enum color {blue, red, 'orange'} # 如果标识符没有赋值 它的值就是下标值
let idx: color = color.orange
console.log('index:', idx)
```

### 7. 任意类型
```yaml
var any_Data: any = 123
any_Data = 'str'
any_Data = false
console.log('any_Data:', any_Data)

```

### 8. null 和 undefined

```yaml
var a: number;
console.log(a) # 输出:undefined 报错

var b: undefined;
console.log('b:', b) # 输出undefined 正确

# 一个元素可能是 number | unll | undefined
num = 12345
console.log(num)
```


### 9. void 类型
typeScript中的void表示没有任何类型，一般用于定义方法的时候方法没有返回值。
```yaml
# 没有返回值
function fun(): void {
    console.log('fun')
}
fun ()

# 有返回值
function fun1(): number {
    return 123
}
```

### 10. never类型
其他类型（包括null 和 undefined）的子类型，代表从不会出现的值
```yaml
# 这意味着证明never的变量只能被never类型所赋值

# 例如
var c: undefined;
c = 123 # 报错
c = undefined


# 用法
var d: never;
d =(()=>{
    throw new Error('error')
})()
```