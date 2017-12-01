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

#### 3.使用

```html


transform options:

Ast:返回ast，默认true
AuxiliaryCommentAfter: 在非用户注入的代码之后添加comment, null
auxiliaryCommentBefore:在非用户注入的代码之前添加comment, null
Babelrc:是否引用.babelrc和.babelignore文件配置, true
Code:enable code generation
Comments: 输出comment， true
compact：关于空白和line terminators的压缩规则， auto
Env: 设置环境变量，{}
extends： A path to an .babelrc file to extend
filename： Filename for use in errors etc. unknown
filenameRelative：Filename relative to sourceRoot.
generatorOpts: 传给babel-generator的参数，babel-generator is used to turn the art into code，{}
getModuleId: Specify a custom callback to generate a module id with, null
highlightCode:语法错误高亮， true
ignore：对应only选项，only的优先级高于ignore， null
inputSourceMap， sourcemap的base on， null
minified：if code minified, false
moduleId: Specify a custom name for module ids, null
moduleIds: if truthy, insert an explicit id for modules. By default, all modules are anonymous, false
moduleRoot:Optional prefix for the AMD module formatter that will be prepend to the filename on module definitions, sourceRoot
only: matching path to compile
parserOpts: 传给babylon的参数
plugins： plugins to load, []
presets: presets to load ,[]
retainLines, 是否保留行数, false
resolveModuleSource:Resolve a module source ie. import "SOURCE"; to a custom value. 
shouldPrintComment: 是否打印comment的判断函数
sourceFileName： Set sources[0] on returned source map.
sourceMaps：是否返回sourcemap， false
sourceMapTarget： sourcemap目标文件
sourceRoot： 根路径
sourceType：complied file type, module or script , default module
wrapPluginVisitorMethod: An optional callback that can be used to wrap visitor methods
```
