# estree

1.program node:

{
	type: ‘program’,
	start,
	end,
	body,
	sourceType: 按ES6写的模块：module，其他的为script
}

2.node object:
{
	type,
	loc: represents the source location information of the node（startPosition, source, endPosition）
}

3.identitier: {
	type: "Identifier";
    	name: string;
}
Note that an identifier may be an expression or a destructuring pattern.

4. Literal: {
	type: "Literal";
    	value: string | boolean | null | number | RegExp;
}
Note that a literal can be an expression, RegExpLiteral会多2个属性
raw: ‘/a/g‘
regex: {
    pattern: string;
    flags: string;
  };

5.Function 可以是decleration i.e function f() {},或者是expression i.e var f = function () {}

{
      "type": "FunctionDeclaration",
      "start": 0,
      "end": 18,
      "id": {
        "type": "Identifier",
        "start": 9,
        "end": 10,
        "name": "a"
      },
      "generator": false,
      "expression": false,
      "params": [],
      "body": {
        "type": "BlockStatement",
        "start": 14,
        "end": 18,
        "body": []
      }
    },
    {
      "type": "VariableDeclaration",
      "start": 20,
      "end": 42,
      "declarations": [
        {
          "type": "VariableDeclarator",
          "start": 24,
          "end": 42,
          "id": {
            "type": "Identifier",
            "start": 24,
            "end": 25,
            "name": "a"
          },
          "init": {
            "type": "FunctionExpression",
            "start": 28,
            "end": 42,
            "id": null,
            "generator": false,
            "expression": false,
            "params": [],
            "body": {
              "type": "BlockStatement",
              "start": 40,
              "end": 42,
              "body": []
            }
          }
        }
      ],
      "kind": "var"
    }


6.ExpressionStatement
 a
{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 1,
      "expression": {
        "type": "Identifier",
        "start": 0,
        "end": 1,
        "name": "a"
      }
    }

7.the directive of liberate: “use strict”

{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 12,
      "expression": {
        "type": "Literal",
        "start": 0,
        "end": 12,
        "value": "use strict",
        "raw": "\"use strict\""
      },
      "directive": "use strict"
    }

8. BlockStatement: {}

{
      "type": "BlockStatement",
      "start": 0,
      "end": 2,
      "body": []
    }

9. FunctionBody:

10. EmptyStatement: solitary semicolon
{
      "type": "EmptyStatement",
      "start": 0,
      "end": 1
 }


11. DebuggerStatement: debugger

{
      "type": "DebuggerStatement",
      "start": 0,
      "end": 8
  }

12. WithStatement

{
    type: "WithStatement";
    object: Expression;
    body: Statement;
}

13.ReturnStatement, 必须要在function body里

{
            "type": "ReturnStatement",
            "start": 17,
            "end": 26,
            "argument": {
              "type": "Literal",
              "start": 24,
              "end": 26,
              "value": 23,
              "raw": "23"
            }
          }

14. LabeledStatement： label: {}

{
      "type": "LabeledStatement",
      "start": 0,
      "end": 9,
      "body": {
        "type": "BlockStatement",
        "start": 7,
        "end": 9,
        "body": []
      },
      "label": {
        "type": "Identifier",
        "start": 0,
        "end": 5,
        "name": "label"
      }
    }


15. BreakStatement: break;在blockStatement

{
            "type": "BreakStatement",
            "start": 11,
            "end": 17,
            "label": null
 }

16. ContinueStatement: continue;在循环的blockStatement中

{
            "type": "ContinueStatement",
            "start": 10,
            "end": 19,
            "label": null
          }

17.IfStatement: if else if else

{
      "type": "IfStatement",
      "start": 0,
      "end": 41,
      "test": {
        "type": "Identifier",
        "start": 4,
        "end": 5,
        "name": "a"
      },
      "consequent": {
        "type": "BlockStatement",
        "start": 7,
        "end": 11,
        "body": []
      },
      "alternate": {
        "type": "IfStatement",
        "start": 17,
        "end": 41,
        "test": {
          "type": "Identifier",
          "start": 21,
          "end": 22,
          "name": "b"
        },
        "consequent": {
          "type": "BlockStatement",
          "start": 24,
          "end": 31,
          "body": []
        },
        "alternate": {
          "type": "BlockStatement",
          "start": 37,
          "end": 41,
          "body": []
        }
      }
    }

18. SwitchStatement: switch () {case 1: break; default: break}
switch (a) {
  case 1:
    break;
    case 2:
    break;
  default:
    break;
}

 {
      "type": "SwitchStatement",
      "start": 0,
      "end": 80,
      "discriminant": {
        "type": "Identifier",
        "start": 8,
        "end": 9,
        "name": "a"
      },
      "cases": [
        {
          "type": "SwitchCase",
          "start": 15,
          "end": 33,
          "consequent": [
            {
              "type": "BreakStatement",
              "start": 27,
              "end": 33,
              "label": null
            }
          ],
          "test": {
            "type": "Literal",
            "start": 20,
            "end": 21,
            "value": 1,
            "raw": "1"
          }
        },
        {
          "type": "SwitchCase",
          "start": 38,
          "end": 78,
          "consequent": [
            {
              "type": "BreakStatement",
              "start": 50,
              "end": 56,
              "label": null
            },
            {
              "type": "LabeledStatement",
              "start": 59,
              "end": 78,
              "body": {
                "type": "BreakStatement",
                "start": 72,
                "end": 78,
                "label": null
              },
              "label": {
                "type": "Identifier",
                "start": 59,
                "end": 66,
                "name": "defalut"
              }
            }
          ],
          "test": {
            "type": "Literal",
            "start": 43,
            "end": 44,
            "value": 2,
            "raw": "2"
          }
        }
      ]
    }


19. ThrowStatement: throw ‘123’;

{
      "type": "ThrowStatement",
      "start": 0,
      "end": 12,
      "argument": {
        "type": "Literal",
        "start": 6,
        "end": 11,
        "value": "123",
        "raw": "'123'"
      }
    }


20. TryStatement: try {} catch(e){}finally{}
{
      "type": "TryStatement",
      "start": 0,
      "end": 29,
      "block": {
        "type": "BlockStatement",
        "start": 3,
        "end": 7,
        "body": []
      },
      "handler": {
        "type": "CatchClause",
        "start": 7,
        "end": 18,
        "param": {
          "type": "Identifier",
          "start": 13,
          "end": 14,
          "name": "e"
        },
        "body": {
          "type": "BlockStatement",
          "start": 15,
          "end": 18,
          "body": []
        }
      },
      "finalizer": {
        "type": "BlockStatement",
        "start": 25,
        "end": 29,
        "body": []
      }
    }

21.WhileStatement:while(1){}
{
      "type": "WhileStatement",
      "start": 0,
      "end": 11,
      "test": {
        "type": "Literal",
        "start": 6,
        "end": 7,
        "value": 1,
        "raw": "1"
      },
      "body": {
        "type": "BlockStatement",
        "start": 8,
        "end": 11,
        "body": []
      }
    }

22. DoWhileStatement do{}while(1)

 {
      "type": "DoWhileStatement",
      "start": 0,
      "end": 15,
      "body": {
        "type": "BlockStatement",
        "start": 3,
        "end": 7,
        "body": []
      },
      "test": {
        "type": "Literal",
        "start": 13,
        "end": 14,
        "value": 1,
        "raw": "1"
      }
    }

23. ForStatement: for(;;){}

{
      "type": "ForStatement",
      "start": 0,
      "end": 10,
      "init": null,
      "test": null,
      "update": null,
      "body": {
        "type": "BlockStatement",
        "start": 7,
        "end": 10,
        "body": []
      }
    }



24. ForInStatement: for(var key in o){}
{
      "type": "ForInStatement",
      "start": 0,
      "end": 19,
      "left": {
        "type": "VariableDeclaration",
        "start": 4,
        "end": 11,
        "declarations": [
          {
            "type": "VariableDeclarator",
            "start": 8,
            "end": 11,
            "id": {
              "type": "Identifier",
              "start": 8,
              "end": 11,
              "name": "key"
            },
            "init": null
          }
        ],
        "kind": "var"
      },
      "right": {
        "type": "Identifier",
        "start": 15,
        "end": 16,
        "name": "o"
      },
      "body": {
        "type": "BlockStatement",
        "start": 17,
        "end": 19,
        "body": []
      }
    }

25. FunctionDeclaration function a() {}

{
      "type": "FunctionDeclaration",
      "start": 0,
      "end": 17,
      "id": {
        "type": "Identifier",
        "start": 9,
        "end": 10,
        "name": "a"
      },
      "generator": false,
      "expression": false,
      "params": [],
      "body": {
        "type": "BlockStatement",
        "start": 14,
        "end": 17,
        "body": []
      }
    }

26.VariableDeclaration var a = 1;

{
      "type": "VariableDeclaration",
      "start": 0,
      "end": 10,
      "declarations": [
        {
          "type": "VariableDeclarator",
          "start": 4,
          "end": 9,
          "id": {
            "type": "Identifier",
            "start": 4,
            "end": 5,
            "name": "a"
          },
          "init": {
            "type": "Literal",
            "start": 8,
            "end": 9,
            "value": 1,
            "raw": "1"
          }
        }


27. ThisExpression: this
{
      "type": "VariableDeclaration",
      "start": 0,
      "end": 15,
      "declarations": [
        {
          "type": "VariableDeclarator",
          "start": 4,
          "end": 15,
          "id": {
            "type": "Identifier",
            "start": 4,
            "end": 8,
            "name": "self"
          },
          "init": {
            "type": "ThisExpression",
            "start": 11,
            "end": 15
          }
        }


28. ArrayExpression:[]

{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 2,
      "expression": {
        "type": "ArrayExpression",
        "start": 0,
        "end": 2,
        "elements": []
      }
    }

29.ObjectExpression:var a = {a:1,b:2};
{
      "type": "VariableDeclaration",
      "start": 0,
      "end": 16,
      "declarations": [
        {
          "type": "VariableDeclarator",
          "start": 4,
          "end": 16,
          "id": {
            "type": "Identifier",
            "start": 4,
            "end": 5,
            "name": "a"
          },
          "init": {
            "type": "ObjectExpression",
            "start": 7,
            "end": 16,
            "properties": [
              {
                "type": "Property",
                "start": 8,
                "end": 11,
                "method": false,
                "shorthand": false,
                "computed": false,
                "key": {
                  "type": "Identifier",
                  "start": 8,
                  "end": 9,
                  "name": "a"
                },
                "value": {
                  "type": "Literal",
                  "start": 10,
                  "end": 11,
                  "value": 1,
                  "raw": "1"
                },
                "kind": "init"
              },
              {
                "type": "Property",
                "start": 12,
                "end": 15,
                "method": false,
                "shorthand": false,
                "computed": false,
                "key": {
                  "type": "Identifier",
                  "start": 12,
                  "end": 13,
                  "name": "b"
                },
                "value": {
                  "type": "Literal",
                  "start": 14,
                  "end": 15,
                  "value": 2,
                  "raw": "2"
                },
                "kind": "init"
              }
            ]
          }
        }
      ],
      "kind": "var"
    }

30. UnaryExpression:"-" | "+" | "!" | "~" | "typeof" | "void" | "delete"
{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 6,
      "expression": {
        "type": "UnaryExpression",
        "start": 0,
        "end": 6,
        "operator": "void",
        "prefix": true,
        "argument": {
          "type": "Literal",
          "start": 5,
          "end": 6,
          "value": 0,
          "raw": "0"
        }
      }
    }


31. UpdateExpression: ++ | —

{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 4,
      "expression": {
        "type": "UpdateExpression",
        "start": 0,
        "end": 4,
        "operator": "++",
        "prefix": false,
        "argument": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        }
      }
    }

32. BinaryExpression  "==" | "!=" | "===" | "!=="
         | "<" | "<=" | ">" | ">="
         | "<<" | ">>" | ">>>"
         | "+" | "-" | "*" | "/" | "%"
         | "|" | "^" | "&" | "in"
         | “instanceof"

{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 5,
      "expression": {
        "type": "BinaryExpression",
        "start": 0,
        "end": 5,
        "left": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        },
        "operator": "+",
        "right": {
          "type": "Identifier",
          "start": 4,
          "end": 5,
          "name": "b"
        }
      }
    }

33. AssignmentExpression "=" | "+=" | "-=" | "*=" | "/=" | "%="
        | "<<=" | ">>=" | ">>>="
        | "|=" | "^=" | “&="
{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 6,
      "expression": {
        "type": "BinaryExpression",
        "start": 0,
        "end": 6,
        "left": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        },
        "operator": "!=",
        "right": {
          "type": "Identifier",
          "start": 5,
          "end": 6,
          "name": "b"
        }
      }
    }

34. LogicalExpression:"||" | “&&”:a && b

{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 6,
      "expression": {
        "type": "LogicalExpression",
        "start": 0,
        "end": 6,
        "left": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        },
        "operator": "&&",
        "right": {
          "type": "Identifier",
          "start": 5,
          "end": 6,
          "name": "b"
        }
      }
    }

35. MemberExpression,If computed is true, the node corresponds to a computed (a[b]) member expression and property is an Expression. If computed is false, the node corresponds to a static (a.b) member expression and property is an Identifier.

{
        "type": "MemberExpression",
        "start": 0,
        "end": 3,
        "object": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        },
        "property": {
          "type": "Identifier",
          "start": 2,
          "end": 3,
          "name": "b"
        },
        "computed": false
      }

{
        "type": "MemberExpression",
        "start": 0,
        "end": 4,
        "object": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        },
        "property": {
          "type": "Identifier",
          "start": 2,
          "end": 3,
          "name": "b"
        },
        "computed": true
      }


36. ConditionalExpression: a?b:c

{
        "type": "ConditionalExpression",
        "start": 0,
        "end": 5,
        "test": {
          "type": "Identifier",
          "start": 0,
          "end": 1,
          "name": "a"
        },
        "consequent": {
          "type": "Identifier",
          "start": 2,
          "end": 3,
          "name": "b"
        },
        "alternate": {
          "type": "Identifier",
          "start": 4,
          "end": 5,
          "name": "c"
        }
      }

37. CallExpression: a.call(this)

{
        "type": "CallExpression",
        "start": 0,
        "end": 12,
        "callee": {
          "type": "MemberExpression",
          "start": 0,
          "end": 6,
          "object": {
            "type": "Identifier",
            "start": 0,
            "end": 1,
            "name": "a"
          },
          "property": {
            "type": "Identifier",
            "start": 2,
            "end": 6,
            "name": "call"
          },
          "computed": false
        },
        "arguments": [
          {
            "type": "ThisExpression",
            "start": 7,
            "end": 11
          }
        ]
      }

38. NewExpression: new F()

{
        "type": "NewExpression",
        "start": 0,
        "end": 5,
        "callee": {
          "type": "Identifier",
          "start": 4,
          "end": 5,
          "name": "F"
        },
        "arguments": []
      }

39. SequenceExpression a,b

{
        "type": "SequenceExpression",
        "start": 0,
        "end": 3,
        "expressions": [
          {
            "type": "Identifier",
            "start": 0,
            "end": 1,
            "name": "a"
          },
          {
            "type": "Identifier",
            "start": 2,
            "end": 3,
            "name": "b"
          }
        ]
      }


40. Patterns: ArrayPattern, ObjectPattern。ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值

Es2015

41.generator

{
      "type": "FunctionDeclaration",
      "start": 0,
      "end": 15,
      "id": {
        "type": "Identifier",
        "start": 10,
        "end": 11,
        "name": "a"
      },
      "generator": true,
      "expression": false,
      "params": [],
      "body": {
        "type": "BlockStatement",
        "start": 13,
        "end": 15,
        "body": []
      }
    }

42.ForOfStatement: for(var v of []){}

{
      "type": "ForOfStatement",
      "start": 0,
      "end": 20,
      "left": {
        "type": "VariableDeclaration",
        "start": 5,
        "end": 10,
        "declarations": [
          {
            "type": "VariableDeclarator",
            "start": 9,
            "end": 10,
            "id": {
              "type": "Identifier",
              "start": 9,
              "end": 10,
              "name": "v"
            },
            "init": null
          }
        ],
        "kind": "var"
      },
      "right": {
        "type": "ArrayExpression",
        "start": 14,
        "end": 16,
        "elements": []
      },
      "body": {
        "type": "BlockStatement",
        "start": 18,
        "end": 20,
        "body": []
      }
    }

43VariableDeclaration kind is let or const

44  A super pseudo-expression
Class a {constructor () {super()}}
{
                    "type": "ExpressionStatement",
                    "start": 42,
                    "end": 49,
                    "expression": {
                      "type": "CallExpression",
                      "start": 42,
                      "end": 49,
                      "callee": {
                        "type": "Super",
                        "start": 42,
                        "end": 47
                      },
                      "arguments": []
                    }
                  }

45 spread element […b] 展开操作符

"expression": {
        "type": "ArrayExpression",
        "start": 0,
        "end": 6,
        "elements": [
          {
            "type": "SpreadElement",
            "start": 1,
            "end": 5,
            "argument": {
              "type": "Identifier",
              "start": 4,
              "end": 5,
              "name": "b"
            }
          }
        ]
      }

46 ArrowFunctionExpression () => 1;
{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 8,
      "expression": {
        "type": "ArrowFunctionExpression",
        "start": 0,
        "end": 7,
        "id": null,
        "generator": false,
        "expression": true,
        "params": [],
        "body": {
          "type": "Literal",
          "start": 6,
          "end": 7,
          "value": 1,
          "raw": "1"
        }
      }
    }

47.YieldExpression yield 1
{
            "type": "ExpressionStatement",
            "start": 17,
            "end": 24,
            "expression": {
              "type": "YieldExpression",
              "start": 17,
              "end": 24,
              "delegate": false,
              "argument": {
                "type": "Literal",
                "start": 23,
                "end": 24,
                "value": 1,
                "raw": "1"
              }
            }
          }


48.TemplateLiteral `123${a}1`:

{
      "type": "ExpressionStatement",
      "start": 11,
      "end": 21,
      "expression": {
        "type": "TemplateLiteral",
        "start": 11,
        "end": 21,
        "expressions": [
          {
            "type": "Identifier",
            "start": 17,
            "end": 18,
            "name": "a"
          }
        ],
        "quasis": [
          {
            "type": "TemplateElement",
            "start": 12,
            "end": 15,
            "value": {
              "raw": "123",
              "cooked": "123"
            },
            "tail": false
          },
          {
            "type": "TemplateElement",
            "start": 19,
            "end": 20,
            "value": {
              "raw": "1",
              "cooked": "1"
            },
            "tail": true
          }
        ]
      }

49.ObjectPattern ({a} = {b:1}) 对象解构
{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 13,
      "expression": {
        "type": "AssignmentExpression",
        "start": 1,
        "end": 12,
        "operator": "=",
        "left": {
          "type": "ObjectPattern",
          "start": 1,
          "end": 4,
          "properties": [
            {
              "type": "Property",
              "start": 2,
              "end": 3,
              "method": false,
              "shorthand": true,
              "computed": false,
              "key": {
                "type": "Identifier",
                "start": 2,
                "end": 3,
                "name": "a"
              },
              "kind": "init",
              "value": {
                "type": "Identifier",
                "start": 2,
                "end": 3,
                "name": "a"
              }
            }
          ]
        },
        "right": {
          "type": "ObjectExpression",
          "start": 7,
          "end": 12,
          "properties": [
            {
              "type": "Property",
              "start": 8,
              "end": 11,
              "method": false,
              "shorthand": false,
              "computed": false,
              "key": {
                "type": "Identifier",
                "start": 8,
                "end": 9,
                "name": "b"
              },
              "value": {
                "type": "Literal",
                "start": 10,
                "end": 11,
                "value": 1,
                "raw": "1"
              },
              "kind": "init"
            }
          ]
        }
      }
    }

50 arrayPattern [a] = [1] 数组解构
{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 9,
      "expression": {
        "type": "AssignmentExpression",
        "start": 0,
        "end": 9,
        "operator": "=",
        "left": {
          "type": "ArrayPattern",
          "start": 0,
          "end": 3,
          "elements": [
            {
              "type": "Identifier",
              "start": 1,
              "end": 2,
              "name": "a"
            }
          ]
        },
        "right": {
          "type": "ArrayExpression",
          "start": 6,
          "end": 9,
          "elements": [
            {
              "type": "Literal",
              "start": 7,
              "end": 8,
              "value": 1,
              "raw": "1"
            }
          ]
        }
      }
    }

51 resetElement function (a, …b) {} reset参数

{
      "type": "FunctionDeclaration",
      "start": 0,
      "end": 22,
      "id": {
        "type": "Identifier",
        "start": 9,
        "end": 10,
        "name": "a"
      },
      "generator": false,
      "expression": false,
      "params": [
        {
          "type": "Identifier",
          "start": 12,
          "end": 13,
          "name": "a"
        },
        {
          "type": "RestElement",
          "start": 15,
          "end": 19,
          "argument": {
            "type": "Identifier",
            "start": 18,
            "end": 19,
            "name": "b"
          }
        }
      ],
      "body": {
        "type": "BlockStatement",
        "start": 20,
        "end": 22,
        "body": []
      }
    }

52 AssignmentPattern  [a=1] = [1] 解构时的默认值

{
      "type": "ExpressionStatement",
      "start": 0,
      "end": 11,
      "expression": {
        "type": "AssignmentExpression",
        "start": 0,
        "end": 11,
        "operator": "=",
        "left": {
          "type": "ArrayPattern",
          "start": 0,
          "end": 5,
          "elements": [
            {
              "type": "AssignmentPattern",
              "start": 1,
              "end": 4,
              "left": {
                "type": "Identifier",
                "start": 1,
                "end": 2,
                "name": "a"
              },
              "right": {
                "type": "Literal",
                "start": 3,
                "end": 4,
                "value": 1,
                "raw": "1"
              }
            }
          ]
        },
        "right": {
          "type": "ArrayExpression",
          "start": 8,
          "end": 11,
          "elements": [
            {
              "type": "Literal",
              "start": 9,
              "end": 10,
              "value": 1,
              "raw": "1"
            }
          ]
        }
      }
    }

53 Classes class c extends a { f () {}}
{
      "type": "ClassDeclaration",
      "start": 0,
      "end": 29,
      "id": {
        "type": "Identifier",
        "start": 6,
        "end": 7,
        "name": "c"
      },
      "superClass": {
        "type": "Identifier",
        "start": 16,
        "end": 17,
        "name": "a"
      },
      "body": {
        "type": "ClassBody",
        "start": 17,
        "end": 29,
        "body": [
          {
            "type": "MethodDefinition",
            "start": 20,
            "end": 27,
            "computed": false,
            "key": {
              "type": "Identifier",
              "start": 20,
              "end": 21,
              "name": "f"
            },
            "static": false,
            "kind": "method",
            "value": {
              "type": "FunctionExpression",
              "start": 22,
              "end": 27,
              "id": null,
              "generator": false,
              "expression": false,
              "params": [],
              "body": {
                "type": "BlockStatement",
                "start": 25,
                "end": 27,
                "body": []
              }
            }
          }
        ]
      }
    }

54 ImportDeclaration 

54.1 ImportDefaultSpecifier import a from ‘a’：
 {
      "type": "ImportDeclaration",
      "start": 0,
      "end": 17,
      "specifiers": [
        {
          "type": "ImportDefaultSpecifier",
          "start": 7,
          "end": 8,
          "local": {
            "type": "Identifier",
            "start": 7,
            "end": 8,
            "name": "a"
          }
        }
      ],
      "source": {
        "type": "Literal",
        "start": 14,
        "end": 17,
        "value": "a",
        "raw": "'a'"
      }
    }


54.2 ImportSpecifier import {a} from ‘a’：
{
      "type": "ImportDeclaration",
      "start": 0,
      "end": 19,
      "specifiers": [
        {
          "type": "ImportSpecifier",
          "start": 8,
          "end": 9,
          "imported": {
            "type": "Identifier",
            "start": 8,
            "end": 9,
            "name": "a"
          },
          "local": {
            "type": "Identifier",
            "start": 8,
            "end": 9,
            "name": "a"
          }
        }
      ],
      "source": {
        "type": "Literal",
        "start": 16,
        "end": 19,
        "value": "a",
        "raw": "'a'"
      }
    }

54.3 ImportNamespaceSpecifier import * as a from ‘a'
{
      "type": "ImportDeclaration",
      "start": 0,
      "end": 22,
      "specifiers": [
        {
          "type": "ImportNamespaceSpecifier",
          "start": 7,
          "end": 13,
          "local": {
            "type": "Identifier",
            "start": 12,
            "end": 13,
            "name": "a"
          }
        }
      ],
      "source": {
        "type": "Literal",
        "start": 19,
        "end": 22,
        "value": "a",
        "raw": "'a'"
      }
    }

55 ExportDefaultDeclaration export default 1:
{
      "type": "ExportDefaultDeclaration",
      "start": 0,
      "end": 16,
      "declaration": {
        "type": "Literal",
        "start": 15,
        "end": 16,
        "value": 1,
        "raw": "1"
      }
    }

56ExportNamedDeclaration export {a}
{
      "type": "ExportNamedDeclaration",
      "start": 0,
      "end": 10,
      "declaration": null,
      "specifiers": [
        {
          "type": "ExportSpecifier",
          "start": 8,
          "end": 9,
          "local": {
            "type": "Identifier",
            "start": 8,
            "end": 9,
            "name": "a"
          },
          "exported": {
            "type": "Identifier",
            "start": 8,
            "end": 9,
            "name": "a"
          }
        }
      ],
      "source": null
    }
57 ExportAllDeclaration export * from ‘a’
{
      "type": "ExportAllDeclaration",
      "start": 0,
      "end": 17,
      "source": {
        "type": "Literal",
        "start": 14,
        "end": 17,
        "value": "a",
        "raw": "'a'"
      }
    }

58 awaitExpression await 1

"expression": {
                "type": "AwaitExpression",
                "start": 24,
                "end": 31,
                "loc": {
                  "start": {
                    "line": 2,
                    "column": 2
                  },
                  "end": {
                    "line": 2,
                    "column": 9
                  }
                },
                "argument": {
                  "type": "NumericLiteral",
                  "start": 30,
                  "end": 31,
                  "loc": {
                    "start": {
                      "line": 2,
                      "column": 8
                    },
                    "end": {
                      "line": 2,
                      "column": 9
                    }
                  },
                  "extra": {
                    "rawValue": 1,
                    "raw": "1"
                  },
                  "value": 1
                }

