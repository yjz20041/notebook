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
```

#### 3.class


