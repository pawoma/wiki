#js代码规范

  前端开发团队遵循和约定的代码书写规范，意在提高代码的规范性和可维护性, 同时良好的代码习惯也能充分体现个人的职业素养。

##基本格式

  1. 代码统一采用Tab缩进（4个空格，可以在编辑器设置），如：vscode 可在 文件-首选项-设置-"editor.tabSize": 4

  2. 语句的结尾处可看个人习惯是否加分号，建议加上分号，这是一个好习惯，特别是在代码会被压缩的情况下。

  3. 模块代码AMD方式组织。define(), 模块依赖用 commonjs require()

    ```javascript
    define(function(require, exports, module) {
        'use strict';
    
        var _ = require('underscore');
    
        var queue = [];
    
        var initModule = function() {
            _.each(queue, function(v, i) {
                // do something
            });
        };
    
        module.exports = {
            init: initModule
        };
    });
    ```

  4. 字符串变量值统一用单引号(')

    ```javascript
    var s = 'hello world';
    var html = '<div class="header"></div>';
    console.log(s + ', my name is cat');
    ```

  5. 注意使用空格/空行

    完整示例
    
    ```javascript
    function walk(holder, key) {
    
        // The walk method is used to recursively walk the resulting structure so
        // that modifications can be made.
    
        var k, v, value = holder[key];
        if (value && typeof value === 'object') {
            for (k in value) {
                if (Object.prototype.hasOwnProperty.call(value, k)) {
                    v = walk(value, k);
                    if (v !== undefined) {
                        value[k] = v;
                    } else {
                        delete value[k];
                    }
                }
            }
        }
    
        return reviver.call(holder, key, value);
    }
    ```

    需要前后加空格的运算符包括:

    ```
    =, ==, ===, !=, !==, >, <, <=, >= , ? :, -, +, +=, -=, /, *, %, &&, &, ||, |, {}
    ```

    不需要出现空格的包括: ` ;, ., (), []`
                        
    后边带空格的包括:

    ```
    ,, if, for, while, do, catch, with, new,
    ```

    非三元表达式中的:

    ```javascript
    a += 2;
    b = true ? a : 1;
    ```

    括号中的参数之间加空格:

    ```javascript
    get(x, b, c);
    function get(a, b, c) {
        // work with a,b,c
    }
    ```

    注释符前后要有空格

    代码段前后保留空行, 类，方法，函数前后保留空行

  **6. 避免使用全局变量, 如果不能避免则尽量减少数量;**

  **7. 三元操作符不要涉及大段的复杂的代码, 如果可以请改为 if else;**

  **8. 奇淫技巧必须注释, 注释应该更多地体现为什么要这样，而不是会怎么样;**

  **9. 将每条语句放置在一个单独的代码行中保持可读性, 不要出现 aNum++; anOtherNum++;在同一行, var 也一样;**

    **(√)**
    
    ```javascript
    aNum++;
    anOtherNum++;
    ```

    **(╳)**

    ```javascript
    aNum++; anOtherNum++;
    ```

### 命名规范

  通常,使用 `functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`, 和 `SYMBOLICCONSTANTSLIKE_THIS`.

  1. 常规的命名方式

    ```javascript
    var variableNamesLikeThis = '...',  // 变量
        CONSTANTS_LIKE_THIS = '...';    // 常量
    
    // 函数
    function functionNamesLikeThis() {
        ...
    };
    
    // 构造类
    function ClassNamesLikeThis() {
        ...
    };
    
    // 方法&属性等
    ClassNamesLikeThis.methodNamesLikeThis = function(){
        ...
    };
    ```

  2. 属性和方法

    文件或类中的`私有`属性, 变量和方法名应该以下划线 "_" 开头.

    保护属性, 变量和方法名不需要下划线开头, 和公共变量名一样.

    方法名按描述过程或描述项的方式, 动名词结合. 来命名, 以小写字母开头, 连接词使用混合大小写的驼峰形式, 例如: `getAncestorByTagName`.

  3. 方法和函数参数

    函数的参数个数不固定时, 应该添加最后一个参数 args 为参数的个数. 你也可以不设置 args 而取代使用 arguments.

    可选和可变参数应该在 @param (Optional) 标记中说明清楚.

  4. Getters 和 Setters

    不强制要求使用Getters和Setters，但当你使用时，Getters应该命名成`getFoo()`形式，同理Setters应该名称成`setFoo(v)`形式

    对于返回值是布尔类型（Boolean）的Getters方法也可以写成`isFoo()`的形式

    ```javascript
    // 定义一个叫学生的构造类
    function Student() {
        ...
    };
    
    Student.prototype.getName = function() {
        ...
    };
    
    Student.prototype.setName = function(name) {
        ...
    };
    
    // 返回值为布尔类型的Getters方法
    Student.prototype.isGirl= function() {
        if (...) {
            return true;
        } else {
            return false;
        }
    };
    ```

  5. 私有

    如果你要把构造类的方法，变量或属性设置为私有的话，请用下划线开头来命名，如：“_privite”

  6. 文件名应该使用小写字符, 以避免在有些系统平台上不识别大小写的命名方式. 文件名以.js结尾, 不要包含除 "-"外的标点符号，jquery插件看情况定.

  7. 构造函数.

    使用首字母大写的形式, 通常为名词, 例如: `Class`;

    但是, 对于内部基类, 也就是不直接调用生成实例的基类, 使用 _ 和首字母大写的形式命名, 例如: `_Base`;

  8. 布尔值以 is 开头的驼峰形式, 例如 `var isGirl = true`;

  9. this命名, 尽量以能表达当前实例意义的名称, 通用命名为self;

    ```javascript
    Pager.protoype.goto = function() {
        var pager = this, index = page.currentIndex + 1;
        setTimeout(function() {
            page.doRequest(index);
        });
    };
    function foo1(){
        var self = this;
        setTimeout(function() {
            console.log(self.name);
        }, 1);
    }
    function foo2(name){
        var self = this;
        self.name = name;
        foo1.call(self);
    }
    ```

  10. 在循环中, 尽量使用单字符变量名称, 例如: i, j, k, m, n;

  11. 避免使用保留字或语言构造命名;

    ```
    abstract boolean break byte case catch char class const
    continue default do double else extends false final finally
    float for function goto if implements import in instanceof
    int interface long native new null package private protected
    public return short assets super switch synchronized this
    throw throws transient true try var void while with
    ```

  12. 尽量保持所有名称最短, 但是一定要保证名称具有描述性;

  13. js钩子命名必须以j开头的驼峰命名，并且不能此钩子不能有应用样式

    **(√)**
    
    ```html
    <button class="jSubmit">提交</button>
    <button id="jSubmit">提交</button>
    ```

    **(╳)**

    ```html
    <button class="submit">提交</button>
    <button id="submit">提交</button>
    ```

### 基本格式

  1. 变量声明

    变量使用var语句声明

    变量使用前必须先声明

    尽量减少使用全局变量，全局变量使用“g”开头

    同一作用域块内的变量尽量使用一个“var”语句来声明

    **(√)**

    ```javascript
    var gName = '';
    function foo() {
        var name = '...',
            sex = '...',
            age = '';
        ....
    };
    ```

    **(╳)**

    ```javascript
    var name = '';
    function foo() {
        var name = '...';
        var sex = '...';
        var age = '';
        ....
    };
    ```

  2. 字符串

    用单引号包裹：创建字符串对象时，优先使用单引号，当你的字符串中包含html代码片段时将格外方便

    ```javascript
    var myString = '待我长发及腰时那还是人吗？  不是，绝对是神！';
    ```

    长字符串:

    字符串太长需要换行时，不要使用转义符“\”来处理行尾的换行，请用字符串相加来替换

    在编译时, 不能忽略行起始位置的空白字符; "\" 后的空白字符会产生奇怪的错误; 虽然大多数脚本引擎支持这种写法, 但它不是 ECMAScript
    的标准规范.

    **(√)**

    ```javascript
    var myString = '带我长发及腰时'+
        '那还是人吗？ '+
        '不是，绝对是神！';
    ```

    **(╳)**

    ```javascript
    var myString = '带我长发及腰时 \
        那还是人吗？ \
        不是，绝对是神！ \';
    ```

    **建议使用es6的反撇号 ``, 注意此用法需babel转译才能兼容浏览器**
    
    ```javascript
    var name = '上帝';
    var myString = `带我长发及腰时那还是人吗,${name}?`
    ```

  3. 常量

    常量的形式如: NAMES_LIKE_THIS, 即使用大写字符, 并用下划线分隔.

    ```javascript
    var SECONDS_IN_A_MINUTE = 60;
    ```

  4. 总是使用分号.

    如果仅依靠语句间的隐式分隔, 有时会很麻烦. 你自己更能清楚哪里是语句的起止.而且有些情况下, 漏掉分号会很危险:

  5. 函数声明

    尽量不要使用全局函数

    内部函数应该跟在 var 语句后面

    不要在语句块内声明函数，如果确实需要，请使用函数表达式：

    同一作用域块内的变量尽量使用一个“var”语句来声明

    **(√)**
    
    ```javascript
    // 但仍旧不建议在语句块内声明函数，即使是表达式的方式
    if (...) {
        var fooName = function() {
            ...;
        };
    }
    ```

    **(╳)**

    ```javascript
    if (...) {
        function fooName() {
            ...;
        }
    }
    ```

  6. 块内函数声明: 不要在块内声明一个函数. 

    不要写成.

    **(╳)**

    ```javascript
    if (x) {
        function foo() {}
    }
    ```

    虽然很多 JS 引擎都支持块内声明函数, 但它不属于 ECMAScript 规范 (见 ECMA-262, 第13和14条).
    各个浏览器糟糕的实现相互不兼容, 有些也与未来 ECMAScript 草案相违背. ECMAScript 只允许在脚本的根语句或函数中声明函数.
    如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

    ```javascript
    if (x) {
        var foo = function() {}
    }
    ```

  7. 闭包，用起来要小心，因为如果处理不当很容易导致内存泄漏. 及时释放闭包变量引用, destory() 方法的设计. 

  8. eval(): 只用于解析序列化串

    eval() 会让程序执行的比较混乱, 当`eval()`里面包含用户输入的话就更加危险. 可以用其他更佳的, 更清晰, 更安全的方式写你的代码,
    所以一般情况下请不要使用`eval()`. 当碰到一些需要解析序列化串的情况下, 使用`eval`很容易实现.

    这是一个常用的`input`标签里面的属性

    ```html
    <input id="jUser" type="hidden" data-user="{'name':'djune','age':30}" />
    ```

    我们通常如此调用(基于jquery实现)

    ```javascript
    var user = $("#jUser").attr("data-user");
    var user = eval('('+user+')');
    console.log(user.name);
    ```

  9. with() {}: 不要使用 

  10. this: 仅在对象构造器, 方法, 闭包中使用. 

    `this`的语义很特别. 有时它引用一个全局对象(大多数情况下), 调用者的作用域(使用 eval时), DOM 树中的节点(添加事件处理函数时),
    新创建的对象(使用一个构造器), 或者其他对象(如果函数被`call()` 或`apply()`).

    使用时很容易出错, 所以只有在下面两个情况时才能使用:

    在构造器中 对象的方法(包括创建的闭包)中

  11. for-in 循环: 只用于 object/map/hash 的遍历,对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值. 下面就是一些失败的使用案例: 

    ```javascript
    // 本来只要输出0，1；结果输出了0,1,djune;
    var a = [0, 1];
    a.buhu = 'djune';
    for (var i in a) {
        console.log(a[i]);
    }
    ```

  12. 尽量不修改内置对象的原型 

    千万不要修改内置对象, 如`Object.prototype`和`Array.prototype` 的原型. 而修改内置对象, 如
    `Function.prototype`的原型, 虽然少危险些, 但仍会导致调试时的诡异现象. 所以也要避免修改其原型.

  13. Object{}和 Array[]

    使用“{}”替代“new Object()”来创建对象

    使用“[]”替代“new Array()”来创建数组,使用 Array 构造器很容易因为传参不恰当导致错误

    ```javascript
    var obj = {
        a: 1,
        b: 2,
        'say hello': 'hello'
    };
    
    var arr = [1, 2, 'hello'];
    ```

  14. 进行对比操作时，尽量使用“===”和“!==”

 






