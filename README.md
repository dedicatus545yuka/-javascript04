# -javascript04
函数，作用域
### 函数  
>一段 JavaScript 代码，它只定义一次，但可能被执行或调用多次，那就是函数。   
>简单来说，函数就是一组可重用的代码，你可以在你程序的任何地方调用它。
#### 函数的定义和调用
>函数 - 先定义，再调用  
>* 注意 - 定义一个函数并不会自动的执行它。定义了函数仅仅是赋予函数以名称并明确函数被调用时该做些什么。调用函数才会真正执行这些动作。
1. 函数声明方式   
- function 函数名(){      
             函数体 - 实际上，就是语句块  
}
```js
function fn1() {
    console.log('this is function');
}
```
- 函数的调用
```js
fn1();
```
2. 字面量方式   
       var 函数名 = function(){函数体}
```js
var fn2 = function(){
    console.log('this is function too');
}
```
- 函数的调用
```js
fn2();
```
![函数调用的方式](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/H8HcKKhNgCC9LMIZTTzcGFIGvgV27jbSXnF1dzl0oVM!/m/dPMAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)

#### 函数与变量
- 变量与函数同名时 - 出现覆盖和被覆盖的现象     
![变量与函数的分析图](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/ZvbIOyiR2JjKptpr0L6NXcaYfAqGvyHPmMUQlzWxHGQ!/m/dD8BAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist) 
```js
var fn = 'this is text';
console.log(fn);
// 字面量方式定义函数
var fn = function(){
    console.log('this is function');
}
// 调用变量
console.log(fn);// 函数将变量覆盖
// 调用函数
fn();
```
![测试图](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/5ax6N09Z6Gmpe0ph.uVJEsRt6Pevy34r0K2r0Bp*.58!/m/dPMAAAAAAAAA&bo=6AdkAQAAAAADB6g!&rf=photolist)
```js
var fn = 'this is text';
console.log(fn);
// 声明方式定义函数
function fn(){
    console.log('this is function');
}
// 调用变量
console.log(fn);// 变量并没有被函数覆盖
fn();//调用函数 - 结果为报错* TypeError: fn is not a function - fn不是一个函数
```
- 这是存储方式的问题  
![测试图](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/5EFG8DHguWj.ZPBmAHvKJFBc6hpRCRueaJyKbhBegPk!/m/dPMAAAAAAAAA&bo=XgMwAQAAAAADB04!&rf=photolist)
#### 函数的参数  
>函数的参数就相当于在函数中使用的变量（虽然这个比方不是很准确）。   
>JavaScript 中的函数定义并未制定函数参数的类型，函数调用时也未对传入的参数做任何的类型检查。  
>函数的参数可以分为以下两种:  
>- 形参: 出现在函数定义文法中的参数列表是函数的形式参数，简称形参 。简单来说，就是定义函数时使用的参数就是形参。  
>- 实参: 函数调用时实际传入的参数是函数的实际参数，简称实参。 简单来说，就是调用函数时使用的参数就是实参。
```js
//函数的定义 - 形参：在函数体中，形参可以类似于变量的定义
function fn(a){
    // 变量的调用 - 目前是只定义，而未初始化的
    console.log(a);// 100
}
fn(100);// 函数的调用 - 实参：在函数体中，初始化对应形参的值
console.log(a);// 函数的形参：在函数体外，是无法被访问(调用)的 - ReferenceError: a is not defined
```
![函数的参数示意图](http://a4.qpic.cn/psb?/V118JuTr0BKcy7/psWTma9OPdV.mHPYfSX***ZJm7kQMlrqD.d*CguYVpU!/m/dPMAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)

1. 在函数的函数体外，也可以被正常访问(调用)
```js
var a = 100;
function fn(){
    console.log(a);// 100
}
fn();
// 也可以调用变量a
console.log(a);// 100
```
2. 在函数体中定义的变量，不能用于函数体外  
```js
function fn(){
    var a = 100;// 变量的定义
    console.log(a);// 100
}
fn();
console.log(a);// 报错 - ReferenceError: a is not defined
```
3. 低耦合  
```js
var c = 100;
function fn(a) {
    console.log(a);
}
fn(c);
```
#### 形参与实参
- 一般情况下，形参与实参的个数是相同的。但在 JavaScript 中并不强求这一点，在特殊情况下，函数的形参和实参的个数可以不相同。  
1. 形参和实参的个数相同 
```js
// 形参 - 允许定义多个，形参之间使用逗号分隔
function fn(a,b,c){
    console.log(a + b + c);// 60
}
// 实参 - 允许定义多个，实参之间使用逗号分隔
fn(10,20,30);
```
2. 形参的个数多于实参的个数
```js
function fn(a,b,c){
    console.log(a+b+c);// 多余的形参的值为 undefined - 10+20+undefined=NaN
}
fn(10,20);
```
3. 实参的个数多于形参的个数
```js
function fn(a,b){
    console.log(a+b);// 30 - 多余的实参的值，形参无法接收
}
fn(10,20,30);
```
4. 函数的函数体中，具有 arguments 对象 - **了解**
    * 作用 - 用于接收实际的实参内容（省略形参）
```js
function fn(){
    console.log(arguments);
}
fn();
fn(1);
fn(1,2);
fn(1,2,3);
/* 输出结果为
{}
{ '0': 1 }
{ '0': 1, '1': 2 }
{ '0': 1, '1': 2, '2': 3 }
 */
```
#### return语句  
- 函数还可以包含一个返回语句（return）。当然，这并不是必需的。  
- return 语句使函数可以作为一个值来使用。  
- return 默认情况下返回的是 undefined。 
```js
//字面量定义方式 
var fn = function(){
    var a = 100;
    // 函数的返回值 return，尽量定义在函数体的最后面
    return a;
    // 如果定义的代码在 return 语句之后，不会被执行
    console.log('xxx');
}
// 变量的调用方式
console.log(fn);// 输出function类型
// 函数的调用方式
fn();
// 将函数的调用结果，输出打印
console.log(fn());// 100
```
![函数的返回值](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/wWzXE3rAsFWZE.i.fKZt0NauUONu2p6N7A5NbTvMx2s!/m/dPIAAAAAAAAA&bo=GwWAAgAAAAADB74!&rf=photolist)
#### 预定义函数 
>JavaScript 预定义了一组函数，又称为全局函数，允许直接使用。    
![示意图](http://a3.qpic.cn/psb?/V118JuTr0BKcy7/EqptfG.JCMeW2iMZcJ.3aeWFxIgvbIUsC*rzvko2SmU!/m/dPIAAAAAAAAA&bo=CQSAAgAAAAADB60!&rf=photolist) 
1. eval()函数   
- eval() 函数用于执行以字符串（String）形式出现的 JavaScript 代码。此函数可以实现动态的执行 JavaScript 代码。
```js
// 定义一个字符串类型的JavaScript代码
var str = 'console.log("this is test.")';
console.log(str);// 将JavaScript代码当作普通的文本内容输出
eval(str);// eval()函数 - 将一段字符串类型的JavaScript代码运行
```
>eval()函数使用
>* 好处 - 可以利用这种方式有效地保护核心代码(存储在服务器端)
>* 坏处 - Web安全性低(目前不推荐使用)

2. 编码与解码(了解)    
```js
var uri = "http://www.atguigu.com/Web前端开发工程师";
console.log(uri);// 涉及到中文，有时不能被正确的显示或使用 - // 输出 http://www.atguigu.com/Web%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%B7%A5%E7%A8%8B%E5%B8%88
// 对字符串进行编码
var encode = encodeURI( uri );
console.log(encode);
// 对字符串进行解码
var decode = decodeURI( encode );
console.log(decode);
/*
    * URI - 统一资源标识符
    * URL - 统一资源定位符
 */
```
### 作用域
- 变量和函数都具有作用域。   
- 作用域就是变量和函数的可被访问的范围，控制着变量和函数的可见性和生命周期。   
- 变量的作用域可被分为全局作用域和函数作用域（局部作用域）。
    - 如果变量是被定义在全局作用域的话，在 JavaScript 代码中的任何位置都可以访问该变量；  
    - 如果变量是被定义在指定函数内部的话，在 JavaScript 代码中只能在该函数内访问该变量。   
- 函数的作用域也可被分为全局作用域和函数作用域（局部作用域）。   
    - 被定义在指定函数内部的函数被称之为局部函数或内部函数。    
>ECMAScript 6 之前的 JavaScript 没有语句块作用域。

#### 变量的作用域
1. 全局变量 - 被定义在全局作用域的变量，在所有函数之外声明的变量，叫做全局变量，因为它可被当前文档中的其他代码所访问。
```js
var str = 'this is text';
// 在全局作用域中允许访问
console.log(str);// 'this is text'
function fn(){
    // 在函数作用域中允许访问
    console.log(str);// 'this is text'
}
fn();
```
2. 局部变量 - 在函数内部声明的变量，叫做局部变量，因为它只能在该函数内部访问。
```js
// 定义函数
function fn(){
    // 函数体 - 就是函数作用域
    // 局部变量 - 被定义在函数作用域中的变量
    var str = 'this is text';
    // 只能在当前函数作用域中被访问
    console.log(str);
}
fn();
// 在全局作用域(非函数作用域)中不能访问局部变量
console.log(str);
```
>在函数作用域中，定义局部变量，不使用 var 关键字时 - 自动提升为全局变量
```js
function fun(){
    // 定义变量时没有使用关键字 var - 这种不使用 var 关键字，在严格模式下是不允许的
    atguigu = "this is atguigu";
    // 在函数作用域访问变量 atguigu
    console.log( atguigu );// 输出 this is atguigu
}
fun();
// 在全局作用域访问变量 atguigu
console.log( atguigu );// 输出 this is atguigu
```
3. 全局变量与局部变量  
```js 
// 全局变量与局部变量同名时
var str = 'this is text';
function fn(){
    console.log(str);// undefined
    var str = 'this is function';
    // 在函数作用域中只访问到的是局部变量
    console.log(str);// this is function
}
fn();
console.log(str);// this is text  
```
4. 声明提前    
 - JavaScript 变量的另一特别之处是，你可以引用稍后声明的变量，而不会引发异常。这一概念称为变量声明提升。    
 - JavaScript 变量感觉上是被“举起”或提升到了所有函数和语句之前。然而提升后的变量将返回 undefined 值，所以即使在使用或引用某个变量之后存在声明和初始化操作，仍将得到 undefined 值。   
 ```js 
var str;//定义一个变量
console.log(str);// undefined
str = 'this is text';
console.log(str);// this is text
```
以下写法与上述写法其实是等价的 - 变量的声明提前   
* 以下代码   
```js
      console.log(str);// undefined       
      var str = 'this is text';
```
* 等价于 
```js  
      var str;
      console.log(str);// undefined
      str = 'this is text';
```
- 在函数内,同样亦是如此
```js
function fn(){
    console.log(str);// undefined
    var str = 'this is a text';
    console.log(str);//'this is a text'
}
fn();
```
5. 按值传递     
- 按值传递就是指将实参变量的值复制一份副本给函数的形参变量。   
- JavaScript 中为函数传递参数时，都是按值传递的。    
- 如果向函数传递的参数是原始类型数据，则在函数中修改参数变量的值，不会影响外部实参的变量
```js
// 定义全局变量
var str = 100;
// 函数的形参 - 函数体中改变的都是形参的值，与全局变量无关
function fn(str){
    console.log(str);// 100
    str = str - 10;
    console.log(str);// 90
}
fn(str);// 函数的实参 -> 对应全局变量 - 100
console.log(str);// 100
```
6. 参数与局部变量      
```js
// 函数的形参与局部变量的关系
function fn(num){
    // 形参 - 利用形参初始化局部变量
    console.log(num);// 100
    // 定义局部变量，值为形参的值
    var num = num;
    // 局部变量
    console.log(num);// 100
    // 局部变量
    num = num - 10;
    // 局部变量
    console.log(num);// 90
}
fn(100);
```
7. 就近原则     
```js
// 定义全局变量
var str = 'this is text';
// 就近原则
function fn(){
    console.log(str);//这里找到的是fn()所以结果是undefined

    var str = 'this is function';//定义局部变量并且初始化值

    console.log(str);// 由于离局部变量最近，所以打印局部变量的值
}
fn();
```
#### 函数的作用域
>函数与变量类似，具有全局作用域和函数作用域（局部作用域）。 
1. 全局函数 - 为了与预定义函数区别，一般就称为函数    
- 与全局变量类似，全局函数是被定义在全局作用域的，在任何位置都可以访问或调用该函数。
```js
function fn(){
    console.log('this is function');
}
// 在全局作用域中允许访问
fn();
function fun(){
    // 在函数作用域中允许访问
    fn();// 'this is function'
}
fun();
```
2. 内部（私有）函数 - 在函数作用域中定义的函数
```js
function fn(){
    // 在函数作用域中定义的函数 - 内部(私有)函数
    function n(){
        console.log('this is n function');//'this is n function'
    }
    // 在当前函数作用域中允许访问
    n();
}
fn();
// 在指定函数作用域外，不允许访问-报错 ReferenceError: n is not defined
n();
```
