# notebook

#### 1.slice

String.prototype.slice(start, end)，如果end的负数，则end = length + end

#### 2.with

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

with 语句内部的节点父节点修改后, 不会同步到节点本身. 也就是说, 不能保证内外数值的一致性. 这是可能成为项目里面隐藏性很高的 bug. 

#### 3.{} instanceof Object,没有prototype属性，但是有__proto__属性，或者通过Object.getPrototypeOf获取
