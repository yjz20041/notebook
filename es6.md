# es6

#### 1.generator

#### introduction： generator实现分为runtime执行环境和执行函数。执行函数由babeljs编译generator函数得到，原理是将其中的yield语句转为switch语句，test条件为runtime中的执行位置loc。loc通过yield作为分水岭，由runtime中的context.prev和context.next标识。

#### poly process:

1. 生成执行函数 f

2.runtime.mark(f),使f拥有指定spec的constructor、prototype、__proto__。

3.runtime.wrap(f,markedF,this,tryLocsList),tryLocsList为f函数体内try...catch的所处的位置。

4.next(arg):

  4.1 context._sent = context.sent = context.arg = arg,参数会被作为yield的返回值 e.g
  ```js
    let a = yield 1 =>
    
    case 0:
      return 1;
    case 2:
      var a = context.send;
    'end':
      return context.stop();
  ```

  4.2 record = tryCatch(fn, context, arg)
  
  4.3 
  ```js
  if record.type === 'normal', return {value, done} 
  if record.type === 'throw',  dispatchExcuetion, 如果 exception被内部catch了，则context.type='next',继续调到catch语句执行。否则context.type = 'throw'，将exception抛到函数外，如果函数外没有捕获exception，则程序抛出异常并结束运行。
  ```
5.throw(arg):

```js
  5.1 如果gen函数还处于‘suspendedStart’,则gen直接向函数外抛出异常
  
  5.2 如果gen函数处于'suspendedYield',则dispatchExcuetion, 如果 exception被内部catch了，则context.type='next',继续调到catch语句执行。否则context.type = 'throw'，将exception抛到函数外，如果函数外没有捕获exception，则程序抛出异常并结束运行。
  ```

6.return(arg):

```js
  6.1 context.abrupt("return", context.arg);
  
  6.2 abrupt会执行try在prev之前，finally在prev之后的finally语句,如果finally里还有finally语句，这继续执行
  
  6.3
```

7.*yield gen():
```js

  7.1 通过 _context2.delegateYield(a(), "t0", 1)方法，gen会被代理给执行*yield gen()的generator。当gen.done时，host.delegate
  置位null

```

8. async await

aync 函数会被转化为gennerator，await后的语句会被放进promise里
```js
  value = gen.next();//excution automatically
  new Promise.resolve(value).then(function () {
    gen.next();
  }, function () {
    gen.throw();
  })
```

```js
  

```

#### 2.Object扩展

```
  1.简写属性值{a} => {a:a}
  2.简写方法 {a(){}}
  3.setter and getter,ie9+支持：e.g
  
  {
    set a (val) {this._a = val}
    get a() {return this._a}
  }
  
  4.Object.defineProperty: 可以控制对象属性的默认操作，如是否可遍历、删除、get、set etc. e.g， ie9+,ie8只支持给dom对象添加属性，给plain object添加属性会报错，并且有几个注意点：
  Property attributes must be set to some values. The configurable, enumerable and writable attributes should all be set to true for data descriptor and true for configurable, false for enumerable for accessor descriptor.(?) Any attempt to provide other value(?) will result in an error being thrown.
Reconfiguring a property requires first deleting the property. If the property isn't deleted, it stays as it was before the reconfiguration attempt

  Object.defineProperty(o, 'a', {
    configurable: false//是否允许重新配置 data descriptor或者accessor descriptor，是否允许删除
    enumerable: false// 是否允许枚举
    
    //下面两组2者选1,不可并存
    
    //data descriptor
    writable: false//是否可写，
    value: 123//默认值
    
    //accessor descriptor
    set (value) { this._a = value}
    get () {return this._a}
    
  })
  
  5.变量key:{[key]: 123}
  
  6.Object.is:
  es5 只有 ==和===， 不足：==会转化两边的变量类型，而且NaN!=NaN, 且+0 === -0。
  Object.is跟===基本一致，但是Object.is(NaN,NaN)为true，Object.is(0, -0)为false
  
  7.Object.assign:合并
    1.第1个参数会转化为对象，如果是null和undefined则会报错
    2.如果只有一个参数，则直接返回该参数,如果该参数非对象，则转成对象返回
    3.数组：{0: "a", 1: "b", 2: "c", length: 3, [[PrimitiveValue]]: "abc"}
    4.布尔值、数值、字符串分别转成对应的包装对象，可以看到它们的原始值都在包装对象的内部属性[[PrimitiveValue]]上面，这个属性是不会被      Object.assign拷贝的。只有字符串的包装对象，会产生可枚举的实义属性，那些属性则会被拷贝。
    5.只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（enumerable: false）
  
  8.Object.getOwnPropertyDescriptor:获取属性的描述对象
  
  9.enumerable:false对 Object.keys, for in, Object.assign,JSON.stringify，其中for in 会遍历继承属性，而其他的不会
  
  10.
  （1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。

首先遍历所有数值键，按照数值升序排列。
其次遍历所有字符串键，按照加入时间升序排列。
最后遍历所有 Symbol 键，按照加入时间升序排列

11.Object.getOwnPropertyDescriptors(): 返回指定对象所有自身属性（非继承属性）的描述对象

12. Object.getPropertyOf 和Object.setPropertyOf分别用于读取和设置对象的__proto__

13.super,指向对象的原型对象

14.Object.keys,values,entries都不包括继承和symbol属性

15. ...destruction：{a, ..b} = {a:1,c:2,d:3} =>  a = 1; b = {c:2, d:3}

16. ...扩展运算符：var o = {a:1,b:2} var o2 = {...o} => o2 = {a:1,b:2}等同于let o2 = Object.assign({}, o);扩展运算符也可以用于合并
var o = {...a,...b}.扩展运算符的参数对象之中，如果有取值函数get，这个函数是会执行的。

17.（提案）null运算符a?.b?.c如果有属性为undefined或者null，则返回undefined
```

#### 3.class


