### namespace
- toggle
- intercept

### 数据判断

```javascript
Array.isArrary()

typeof foo === 'function'

// 数组、null、对象 返回 'obect'
typeof sth === 'object' 

```

### Object.prototype.toString 
- // [ref](https://www.cnblogs.com/bq-med/p/8796836.html)
- 进行复杂数据类型判断
- 存在子元素重写`toString`方法的清空
```javascript

const _toString = Object.prototype.toString

// eg. 数组会重写 `toString` 方法
var arr=[1,2];
arr.toString();// "1,2"


_toString.call([]); //"[object Array]"
_toString.call({}); //"[object Object]"
_toString.call(123); //"[object Number]"
_toString.call('123'); //"[object String]"
_toString.call(function()); //"[object Function]"
_toString.call(undefined); //"[object Undefined]"
_toString.call(true); //"[object Boolean]"
_toString.call(null); //"[object Null]"


function isPlainObject(obj){
  return _toString.call(obj) === '[object object]'
}


function toRawType (value: any): string {
  return _toString.call(value).slice(8, -1)
}


```


### 定义、赋值
```javascript
// 定义对象
const obj1 = {}
const obj2 = new Object()
const obj3 = Object.create(obj1) // obj3.__proto__ === obj1

// 连续赋值、 引用赋值
var a , b , c ;
a = b = c = {a:1}
// 对象是引用赋值

```

### 原型链、继承、调用
```javascript

Object.create()

.call()

.apply()

```


### typeScript
```
flow 
```

### object.defineProperty()
```javascript

let Person = {}
let temp = null

Object.defineProperty(Person, 'name', {
  value: '',
  writable: false,
  enumerable: false,
  configurable: false,
  get: function(){
    return temp
  },
  set: function(val){
    temp = val
  }
})

```

### class
```javascript

```

### makeMap 闭包
```
/**
 * Make a map and return a function for checking if a key
 * is in that map.
 */
export function makeMap (
  str: string,
  expectsLowerCase?: boolean
): (key: string) => true | void {
  const map = Object.create(null)
  const list: Array<string> = str.split(',')
  for (let i = 0; i < list.length; i++) {
    map[list[i]] = true
  }
  return expectsLowerCase
    ? val => map[val.toLowerCase()]
    : val => map[val]
}
// 根据字符串生成一个`map`
// 返回一个函数，并且接受一个字符串 `key` 作为入参
// 函数判断 `map` 中是否有`key`

```




 

