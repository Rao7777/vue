### 抽象组件 abstract
```
AbsComponents = {
  abstract: true, // 没有暴露的属性，默认false
  created () {
    console.log('我是一个抽象的组件')
  }
}
```
1. `keep-alive` 和 `transition` 是抽象组件
2. 抽象组件不会渲染dom到页面
3. 抽象组件不会出现再父子关系路径


### 响应式
- 简单步骤
  1. 需要响应式的属性，会注册到`vm`实例的`_data`对象上
  2. `proxy` 函数：通过`Object.defineProperty` 函数在实例对象`vm`上定义与`data`字段同名的访问器属性，属性的代理的值是`vm._data`上对应的属性值
  3. `Object.defineProperty()` 重写属性的 `get/set`方法
  4. 在`get/set`函数中，闭包引入收集依赖的`Dep`实例对象
  5. `Dep` 实例会处理该数据，并给数据添加 `__ob__` 属性
  6. `get` 函数: `dep.depend()` 观察者被收集了
  7. `set` 函数: `dep.notify()` 触发了响应


- 为什么没有初始化的属性不能被监听到？ 
  - 因为没有经过`get` 拦截呀！
  - `Vue.set()` 会触发 `data.a._ob_.dep` 依赖

- 特殊的数组
```javascript
{
  arr: [
    { a: 1, __ob__ /* 将该 __ob__ 称为 ob2 */ },
    __ob__ /* 将该 __ob__ 称为 ob1 */
  ]
}

Vue.set(ins.$data.arr, 0, {a: 2}) // 修改 ob1
Vue.set(ins.$data.arr[0], 'b', 2) // 修改 ob2

```


- [`proxy` 函数：通过`Object.defineProperty` 函数在实例对象`vm`上定义与`data`字段同名的访问器属性，属性的代理的值是`vm._data`上对应的属性值](http://caibaojian.com/vue-design/art/7vue-reactive.html#%E5%AE%9E%E4%BE%8B%E5%AF%B9%E8%B1%A1%E4%BB%A3%E7%90%86%E8%AE%BF%E9%97%AE%E6%95%B0%E6%8D%AE-data)
```javascript
export function proxy (target: Object, sourceKey: string, key: string) {
  sharedPropertyDefinition.get = function proxyGetter () {
    return this[sourceKey][key]
  }
  sharedPropertyDefinition.set = function proxySetter (val) {
    this[sourceKey][key] = val
  }
  Object.defineProperty(target, key, sharedPropertyDefinition)
}

```


