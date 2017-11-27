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
  if record.type === 'normal', return {value, done} 
  if record.type === 'throw',  dispatchExcuetion, 如果 exception被fcatch了，则context.type='next',否则context.type = 'throw'.

5.throw:

6.return:

7.*yield:

8.
