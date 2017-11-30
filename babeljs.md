# babeljs

#### 1.babel-polyfill 6.26在ie8下无法运行，因为delegate.iterator.return中return是关键字在IE8下，需要修改为delegate.iterator['return']

#### 2.兼容性

```js
  1. 如果运行环境低于es5，则需要引入babel-polyfill
  
  2. babel-polyfill：无法polyfill Object.setPrototypeOf方法，Object.defineProperty无法实现setter 和getter。
  
  3. class:
    3.1 由于polyfill无法完成Object.setPrototypeOf方法，而静态方法和属性是通过subClass.__proto__ = supClass得到继承的，因此ie 11-下是无法继承
    静态方法和属性的。可以通过protoToAssign插件让supClass的方法全部assign到subClass。
    3.2 由于polyfill的defineProperty无法完成setter和getter，所以ie9-不要用set和get为class添加属性和方法

```
