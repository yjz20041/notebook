# notebook

#### 1.slice

String.prototype.slice(start, end)，如果end的负数，则end = length + end

#### 2.with
```js
var root = { 
branch: { 
node: 1 
} 
}; 

with(root.branch) { 
root.branch = { 
node: 0 
}; 
// 显示 1, 错误! 
alert(node); 
} 
// 显示 0, 正确! 
alert(root.branch.node); 
```

with 语句内部的节点父节点修改后, 不会同步到节点本身. 也就是说, 不能保证内外数值的一致性. 这是可能成为项目里面隐藏性很高的 bug. 

#### 3.{} instanceof Object,没有prototype属性，但是有__proto__属性，或者通过Object.getPrototypeOf获取

#### 4.Function和Object


1.每个函数默认都会有一个属性叫prototype, 每一个通过函数和new操作符生成的对象都具有一个属性__proto__, 这个属性保存了创建它的构造函数的prototype属性的引用

2.所有函数包括Object和Function,Array,String,Boolean,Number，都是以Function.prototype为原型创建的特殊对象（因为拥有函数的性质，并且拥有prototype属性），它们的__proto__都指向Function.prototype。

比如定义函数 function a () {console.log('a')} 等同于 var a = new Function('console.log("a")')。new Function：生成的对象拥有函数的特性，并且会再原型链中创建一个以根链节点Object.prototype为父链的instance作为prototype属性值（Object则指向Object.prototype）。

3. new f()原理

var o = {};
o.__proto__ = f.prototype;
o.call(f);

4.如何解释 Function instanceof Object and Object instanceof Function

var Object = new Function(...)
Object的__proto__指向Function.prototype, 所以Object instanceof Function

由于Function.__proto__.__proto__为Object.prototype，所以Function instanceof Object

5.总的来说，Object/Function及对应Object.prototype和Function.prototype这4个instances js executer事先会创建好。Object.prototype是原型链上的根节点，Function.prototype是一个函数，i.e.原型链的节点可以是一个函数，其定义了一些内部实现，具体未知（[native code]）,其父链指向Object.prototype

