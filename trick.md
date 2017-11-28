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

5.总的来说，Object/Function及对应Object.prototype和Function.prototype这4个instances js executer事先会创建好。Object.prototype是原型链上的根节点，Function.prototype是一个特殊的函数，不是Function的实例，其__proto__指向了Object.prototyepe,i.e.原型链的节点可以是一个函数，其定义了一些内部实现，具体未知（[native code]）,其父链指向Object.prototype

#### 5.switch... case

当case缺少break，则会一直向下执行，不论接下来的case是否匹配，知道swtich结束

#### 6. BOM：字节顺序标记 byte order mark, \ufeff

6.1utf-8 有  有bom头 格式 和 无bom头格式

有bom头的就是读取文件的时候  文件内容会以 \ufeff 开头

正因为这样  使用文件内容的时候  使有些无法过滤掉 bom头的 函数或是语言 不能正常处理文件内容 比如  javascript 不能使用原生的 jsonparse 处理json   

或是   php  报错

6.2

字符U+FEFF如果出现在字节流的开头，则用来标识该字节流的字节序，是高位在前还是低位在前。如果它出现在字节流的中间，则表达零宽度非换行空格的意义，用户看起来就是一个空格。从Unicode3.2开始，U+FEFF只能出现在字节流的开头，只能用于标识字节序，就如它的名称——字节序标记——所表示的一样；除此以外的用法已被舍弃。取而代之的是，使用U+2060来表达零宽度无断空白。

#### 7.unicode编码的各种表示方式
```js
格式一：&#XXXX;&#XXXX;
示例：&#24744;&#22909;
结果：您好


格式二：\uXXXX\uXXXX
示例：\u60a8\u597d
结果：您好


格式三：&#DDDDD;&#DDDDD;
示例：&#x60a8;&#x597d;
结果：您好
```

#### 8.空格相关

```js

8.1 \n新一行，\r返回。打字机时代的产物
\f: 换页符，\t:tab,\v：垂直制表符，就是换行后紧跟前一列。

8.2 \xa0或者\u00a0, &nbsp;

8.3 0x20 \x20 \u2000：空格,中文空格为\u3000

8.4： nbsp 是 Non-Breaking SPace的缩写，即“不被折断的空格”，当两个单词使用 &nbsp; 连接时，这两个单词就不会被分隔为2行

8.5 trim支持IE9+，polyfill String.replace(/^[\s\ufeff\xa0\u3000]+|[\s\ufeff\xa0\u3000]+$/g, '')
```

#### 9.word-break word-wrap white-space区别

```css
  9.1 word-break:单词内换行，默认normal，非CJK只在单词链接处(空格)换行
  
  9.2 word-wrap(overflow-wrap):
```

