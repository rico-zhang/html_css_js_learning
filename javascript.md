# JS语言概述
## JS语言简史
1. JS语言的起源
网景(Netscape Communication Corperation)1994年推出了第一款商用浏览器===》网景浏览器(Netscape Navigator)
1995年，网景公司决定在浏览器中加入一门语言，可以作交互效果，提高用户体验。
最终决定独立开发一门新的语言聘请Brendan Eich，10天后，新的语言诞生
LiveScript->JavaScript
**JS语言之父：Brendan Eich**
2. 第一次浏览器大战
网景公司打算在浏览器中加入网络操作系统，影响到微软的利益，引起了微软的注意
1995年，微软发布IE浏览器。
JS语言推出后，网景获得了极大的竞争优势。
微软对JS进行反编译，借鉴JS语言，推出了JScript、VBScript
第一次浏览器大战是**标准之争**
1997年，网景公司将javascript1.1版本提交给ECMA(欧洲计算机制造协会)
IE3发布，并绑定windows操作系统
1998年网景公司被收购。
**ECMA收录了javascript,并提交给ISO，经过修改，成为了第一个标准版本，成为ECMAScript,简称ES**
3. 第二次浏览器大战
IE4 IE5 IE6(windows xp)
微软决定解散浏览器团队
Brendan Eich，带领团队成立Mozilla基金会，并决定经网景浏览器开源
长时间内，世界的技术爱好者对网景浏览器进行维护和打补丁
2002年，Mozilla推出了fiefox浏览器。
2008年，谷歌推出了Chrome浏览器，苹果推出了Safari，ASA公司推出了opera
chrome浏览器打在JS执行引擎V8*(V8引擎可以将Js代码直接转换为字节码，理论上，JS代码的执行速度已经接近汇编语言)于是，JS具备了编写大型应用程序能力，甚至服务器
> Ryan Dahl 准备写一个服务器的框架，直接利用V8引擎完成了该框架，就是nodejs
**v8引擎将JS的执行推向了一个新的台阶**
4. ES标准的发展
ES1 ，1997年
ES2 ，1998年
ES3 ，1999年
ES4 ，太激进，没有发布 所以没有这个版本
ES5 ，2009年，习惯上不再区分JavaScript(js)和ECMAScript(es)
ES6 ，2015年
ES7 ，2016年
**ES制定语言标准，不涉及语言的运行环境，正式因为ES避免了运行环境，才让ES有机会在各种环境中执行**

## JS语言特性
* 解释性语言
* 弱类型语言
* 单线程

# 运算符
## 概述
* 表达式就是操作符和操作数组成
* 表达式的返回结果为表达式的运算结果
 * = :返回右边的计算结果
 * console.log 的返回值为undefined
 
## 算数运算符
* typeof 1/0 : 相当于(typeof 1) / 0
* +"Infinity" 结果为 Number类型的Infinity
* +"-Infinity" 结果为 Number类型的-Infinity
* % 运算符的结果只与被除数的正负号有关系，与除数无关
* 正数/0:Infinity
* 负数/0:-Infinity
* 0/0 :NaN
* isNaN与Number.isNaN:前者会将参数转化为Number,后者不会
 * isNaN("nihk") : true
 * Number.isNaN("nihk") :false
 * 算数运算符计算的结果是不精确的
 
## 自增 自减
* ++ -- 的运算符优先级很高，比 + - * / % 高，比()低
* ++a :返回值为自增之后的新值
* a++ :返回值为自增之前的旧值
* 运算顺序
 1. 从左到右依次查看
 2. 如果遇到操作数，将数据的值直接取出(除++ -- 外，因为++ -- 的操作数不能是字面量)
 3. 如果遇到相邻的两个运算符，并且左边的运算符优先级大于等于右边，则直接运行左边的运算符，然后再从第一步开始
 4. var x= 1 ;var y = x + x++ \* (x = x + x++ * ++x) + x ;//x：10 y:21

## 比较运算符
* 算数运算符优先级高于比较运算符

### 大小比较
* 两个字符串比较大小，比较的是字符串的字符编码(ASCII)
* 只要有一个不是字符串，并且两个都是原始类型，则转化为数字比较
* NaN与任何比较，得到的都是都是false
* Infinity比任何数字都大（与NaN比较大小都为false）
* 如果其中有一个是对象，那么先将对象转化为原始类型

### 相等比较
* == != 不严格比较
* ===  !== 严格比较
* 两端类型相同，比较数据本身(对象比较地址)
* 两端类型不同
 * null、undefined与其他数字比较都为false 但是null ==undefined为true
 * Infinity ,-Infinity只能和自身相等
 * NaN与其他都不等，自身也不等
 * 对象转化为原始类型 再比较

## 逻辑运算符
* && 短路与用于判断数据是否有效 callback && typeof(callback) ==="function" && callback()
* || 默认值 var a = b || 1；
* ! 转化为boolean类型 !!a
* && 的优先级高于 || 如果出现混合使用 可以看成||两端分别计算，最后计算 ||

## void 
* void() 执行表达式并且返回undefined
* void(1+2) undefined
* void 1+2 相当于void(1) +2 :NaN
* 同typeof一样，最好个括号一起使用

## 逗号运算符
* 逗号运算符的优先级比=还低
* 返回最后一个表达式的结果

## 数字扩展 
### 为什么JS的小数运算不精确
因为计算机以二进制存储数字，十进制转化为二进制时可能无法精确表示如0.3转化为二进制就把无法完全存储
### 数字存储
JS在计算机中给每个数字开辟一块内存，尺寸固定为64位，分为3段
第一段：1位，符号位，1为负数，0为正数
第二段：11位 指数位，即2的多少次方，设置一个偏移量算出的结果要减去1023
第三段：52位 有效数字 算出的结果为小数位，正数会为1
0    1000 0000 011    111 0000 0000 00000。。。。
\+    1027             0.1110000。。。
\+ 1.111 * 2 ^ (1027-1023)
* 指数为0 尾数为0 表示数字0
* 符号为0 指数为2047 尾数为0 表示正无穷
* 符号为1 指数为2047 尾数为0 表示负无穷
* 指数为2047 尾数不为0 表示NaN

## 位运算
* 如果进行位运算，先将数字转为为整数,再转化为32位的二进制 
 * 2.7 --》2 --》32位的二进制 第一位是符号位
 * NaN，Infinity，-Infinity都转化为0
* & 两位都为1 才为1 有0就为0
* | 两位都为0 才为0 有1就为1
* ~ 按位取反（包括符号位）；应用：快速取整 ~~3.14
* ^ 两位不同为1 相同为0
```javascript
var perm = {
read:0b001,//读
write:0b010,//写
create:0b100//创建
} 
var p = perm.read | perm.write;//p表示可读可写
p & perm.read === read;//为true表示有读的权限
p = (p | perm.read) ^ perm.read //去掉可读权限，必须先|一下，不然直接异或，如果p没有读权限，那么不仅没有去掉 反而添加上去了
```
* << 左位移 a * 2**b === a<<b
* \>> 右位移 parseInt(a / 2**b) === a>>b
* \>>> 全右位移 符号位也会位移

## 求余与求模
* 求余
  * y rem x => y -parseInt(y/x) * x 
  * -7 rem 3 => -7-(-2)*3 => -1
  * 商向0取整

* 求模
 * y mod x =>  y- Math.floor(y/x) *x
 * -7 mod 3 => a = -3; -7-(-3) *3 =>2
 * 商向下取整

* 只有商为负数的时候有差别
* 求余的结果与被除数符号一样
* 求模的结果与除数符号一样

#函数
## new.target

该表达式在函数中使用，返回的是当前的构造函数，但是，如果该函数不是通过new调用的，则返回undefined

通常用于判断某个函数是否是通过new在调用。

## 对象属性 描述符
```js
  function User(name, age) {

            var _age;

            Object.defineProperty(this, "age", {
                get : function () {
                    console.log('get');
                    return _age;
                },
                set: function (val) {
                    if (val > 100) {
                        _age = 100;
                    } else if (val < 0) {
                        _age = 0;
                    }else{
                        _age = val;
                    }
                    console.log('set',val,_age);
                }
            });
            this.age = age;

        }

        var user = new User('zhang',50);
```
##防抖与节流
```js
   function test(e) {
            console.log(this, e);
        }
        var hand = throttle(test, 1000, false);

        function resize(e) {
           hand.apply(this,arguments);
        }
        window.onresize = resize;

        function debounce(cb, time) {
            var timer = null;
            return function () {
                clearTimeout(timer);
                var args = arguments;
                var self = this;
                timer = setTimeout(() => {
                    cb.apply(self, args);
                }, time);
            }
        }

        function throttle(cb, time, invali) {
            if (invali) {
                var last = 0;
                return function () {
                    var now = new Date();
                    var self = this;
                    var args = arguments;
                    if (now - last > time) {
                        cb.apply(self, args);
                        last = now;
                    }
                }
            } else {
                var timer = null;
                return function () {
                    var self = this;
                    var args = arguments;
                    if (timer)
                        return;
                    else {
                        timer = setTimeout(() => {
                            cb.apply(self, args);
                            timer = null;
                        }, time);

                    }
                }
            }
        }
```

##管道
``` js
   function add(val) {
            return val + 1;
        }

        function sub(val) {
            return val - 1;
        }

        function muti(val) {
            return val * 2;
        }
        var val = 1;


        function pipe(arr, val) {

            // for (let i = 0; i < arr.length; i++) {
            //     const fun = arr[i];
            //     val = fun(val);
            // }
            //  return val;

            // arr.forEach(fun => {
            //     val = fun(val);
            // });
            // return val;

            return arr.reduce((pre, now) => {
                return now(pre);
            }, val);
        }
        var res = pipe([add, muti, sub], 1);
        console.log(res);
```
## 柯里化
``` js
   function test(a, b, c, d) {
            console.log(a * b + c - d);
            return a * b + c - d;
        }
        test(1, 5, 5, 2); //8
        test(1, 4, 6, 8); //2
        test(1, 3, 7, 4); //6
        test(1, 3, 7, 6); //4

        function curry(fun) {
            var args = Array.prototype.slice.call(arguments, 1);
            var self = this;
            return function () {
                var totalArgs = args.concat(Array.from(arguments));
                if (totalArgs.length >= fun.length) {
                    fun.apply(self, totalArgs);
                } else {
                    totalArgs.unshift(fun)
                   return self.curry.apply(self, totalArgs);
                }
            }
        }
        var g = curry(test, 1);
        g(5, 5, 2);
        g(4, 6, 8);
        var y = g(3, 7);
        y(4);
        y(6);
```
