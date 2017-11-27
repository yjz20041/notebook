# es6

#### generator

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

```

8. sync await
