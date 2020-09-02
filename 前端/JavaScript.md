# JavaScript简介

ECMAScript是一种语言标准，而JavaScript是网景公司对ECMAScript标准的一种实现。

# JavaScript基本语法

### 赋值

```
var a=1;
```

### 注释

```
//这是一行注释
alert（"hello"）;

/*
这是注释
这也是注释
这还是注释
*/
```

### 大小写

JavaScript严格区分大小写，如果弄错了大小写，程序将报错或者运行不正常。

### 数据类型

#### Number

JavaScript不区分整数和浮点数，统一用Number表示，以下是合法的Number类型；

```
123; // 整数123
0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
-99; // 负数
NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
```

Number可以直接做四则运算，规则和数学一样；

```
1 + 2; // 3
(1 + 2) * 5 / 2; // 7.5
2 / 0; // Infinity
0 / 0; // NaN
10 % 3; // 1
10.5 % 3; // 1.5
```

#### 字符串

字符串是以单引号或者双引号括起来的任意文本，

```
'abc'
"acb"
```

多行字符串用\n写起来比较费事，最新的ES6标准新增了一种多行字符串的表示方法，用反引号表示

```
`这是一个
多行
字符串`;
```

拼接字符串，可以用+号连接，ES6新增了一种模板字符串。如下例

```
var name = '小明';
var age = 20;
var message = '你好, ' + name + ', 你今年' + age + '岁了!';
alert(message);

//ES6新特性
var name = '小明';
var age = 20;
var message = `你好, ${name}, 你今年${age}岁了!`;
alert(message);
```

##### 操作字符串的一些方法

toUpperCase()：把一个字符串全部变成大写

toLowerCase()：把一个字符串全部变成小写

indexOf()：会搜索指定字符串出现的位置

substring()：返回指定索引区间的子串

```
var s = 'Hello';
s.toUpperCase(); // 返回'HELLO'


var s = 'Hello';
var lower = s.toLowerCase(); // 返回'hello'并赋值给变量lower
lower; // 'hello'

var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1

var s = 'hello, world'
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'
```



#### 布尔值

一个布尔值只有true、false两种值

```
true; // 这是一个true值
false; // 这是一个false值
2 > 1; // 这是一个true值
2 >= 3; // 这是一个false值
```

&&运算是与运算，LL只有所有都为true，&&运算结果才是true

```
true && true; // 这个&&语句计算结果为true
true && false; // 这个&&语句计算结果为false
false && true && false; // 这个&&语句计算结果为false
```

||运算是或运算，只要其中有一个为true，||运算结果就是true；

```
false || false; // 这个||语句计算结果为false
true || false; // 这个||语句计算结果为true
false || true || false; // 这个||语句计算结果为true
```

！运算是非运算，是一个单目运算符，把true变成false。false变成true；

```
! true; // 结果为false
! false; // 结果为true
! (2 > 5); // 结果为true
```

#### 比较运算符

有两种比较运算符

第一种是==比较，它会自动转换数据类型再比较，很多时候，会得到比较诡异的结果。

第二种是===比较，他不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较。

由于这个缺陷，不要使用==比较，始终坚持使用===比较。



有一种例外是Nan这个特殊的Number与所有其他值都不相等，包括它自己。

```
NaN===NaN; //false
```

唯一能判断NaN的方法是通过isNaN()函数；

```
isNaN(NaN)；//true
```

对于浮点数的相等比较要注意，对于那种有无限循环小数的结果之间的比较，要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值

```
Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true
```

#### null和undefined

Null表示一个空的值，和0以及字符串''不同，0是一个数值，''表示长度为0的字符串，而null为空。

Undefined表示值未定义，大多数情况下没什么用，仅仅在判断函数参数是否传递的情况下有用。

#### 数组

数组是一组按顺序排列的集合，JavaScript的数组可以包括任意数据类型。数据的元素可以通过索引来访问。

```
var arr = [1, 2, 3.14, 'Hello', null, true];
arr[0]; // 返回索引为0的元素，即1
arr[5]; // 返回索引为5的元素，即true
arr[6]; // 索引超出了范围，返回undefined
```

##### 方法

indexOf()：搜索一个指定的元素的位置

slice()：截取Array的部分元素，然后返回一个新的Array，slice()的起止参数包括开始索引，不包括结束索引，如果不给slice()传递任何参数，它会从头到尾截取所有元素，利用这一点，我们可以很容易复制一个Array

push()：向Array的末尾添加若干元素

pop()；把Array的最后一个元素删除掉

unshift()：往Array的头部添加若干元素。

shift()：把Array的第一个元素删掉

sort()：对当前元素进行排序。按照默认顺序排序

reverse()；把整个Array的元素反转

splice()；可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素

concat()；把当前Array和另一个Array连接起来，并返回一个新的Array

join()；把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串，如果Array的元素不是字符串，将自动转换为字符串再连接

#### 对象

JavaScript的对象是一组由键-值组成的无序集合。JavaScript对象的键都是字符串类型，值可以是任意数据类型。

```
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```

如果属性包含特殊字符，必须用单引号`'..'`括起来

```
var xiaoming={
name:'小红',
'middle-school':'No 1 Middle School'
}
```

访问这个属性也无法使用`.`操作符，必须用`['xxx']`来访问

```
xiaohong['middle-school']; // 'No.1 Middle School'
xiaohong['name']; // '小红'
xiaohong.name; // '小红'
```

由于JavaScript的对象是动态类型，你可以自由地给一个对象添加或删除属性：

```
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```

如果我们要检测`xiaoming`是否拥有某一属性，可以用`in`操作符：

```
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
```

不过要小心，如果`in`判断一个属性存在，这个属性不一定是`xiaoming`的，它可能是`xiaoming`继承得到的：

```
'toString' in xiaoming; // true
```

因为`toString`定义在`object`对象中，而所有对象最终都会在原型链上指向`object`，所以`xiaoming`也拥有`toString`属性。

要判断一个属性是否是`xiaoming`自身拥有的，而不是继承得到的，可以用`hasOwnProperty()`方法：

```
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```

#### 变量

JavaScript种的变量名是大小写、数字、$和_的组合，且不能用数字开头，也不能是JavaScript的关键字。

#### 循环

##### for....in

for循环的一个变体是`for....in`循环，它可以把一个对象的所有属性依次循环出来；

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    console.log(key); // 'name', 'age', 'city'
}
```

要过滤掉对象继承的属性，用`hasOwnProperty()`来实现：

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    if (o.hasOwnProperty(key)) {
        console.log(key); // 'name', 'age', 'city'
    }
}
```

由于`Array`也是对象，而它的每个元素的索引被视为对象的属性，因此，`for ... in`循环可以直接循环出`Array`的索引：

```
var a = ['A', 'B', 'C'];
for (var i in a) {
    console.log(i); // '0', '1', '2'
    console.log(a[i]); // 'A', 'B', 'C'
}
```

*请注意*，`for ... in`对`Array`的循环得到的是`String`而不是`Number`。

##### do....while

最后一种循环是`do { ... } while()`循环，它和`while`循环的唯一区别在于，不是在每次循环开始的时候判断条件，而是在每次循环完成的时候判断条件：

```
var n = 0;
do {
    n = n + 1;
} while (n < 100);
n; // 100
```

用`do { ... } while()`循环要小心，循环体会至少执行1次，而`for`和`while`循环则可能一次都不执行。

### Map和Set

#### Map

Map初始化

```
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95
```

Map主要方法

```
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```

#### Set

`Set`和`Map`类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在`Set`中，没有重复的key。

要创建一个`Set`，需要提供一个`Array`作为输入，或者直接创建一个空`Set`：

```
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```

重复元素在`Set`中自动被过滤：

```
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}
```

注意数字`3`和字符串`'3'`是不同的元素。

通过`add(key)`方法可以添加元素到`Set`中，可以重复添加，但不会有效果：

```
s.add(4);
s; // Set {1, 2, 3, 4}
s.add(4);
s; // 仍然是 Set {1, 2, 3, 4}
```

通过`delete(key)`方法可以删除元素：

```
var s = new Set([1, 2, 3]);
s; // Set {1, 2, 3}
s.delete(3);
s; // Set {1, 2}
```

### Iterable

遍历`Array`可以采用下标循环，遍历`Map`和`Set`就无法使用下标。为了统一集合类型，ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

具有`iterable`类型的集合可以通过新的`for ... of`循环来遍历。

```
var a = ['A', 'B', 'C'];
var s = new Set(['A', 'B', 'C']);
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
for (var x of a) { // 遍历Array
    console.log(x);
}
for (var x of s) { // 遍历Set
    console.log(x);
}
for (var x of m) { // 遍历Map
    console.log(x[0] + '=' + x[1]);
}
```

# 函数

### 函数定义

```
//第一种方法
function abs(x){
   if(x>=0){
   return x;
   }else {
   return -x;
   }
}

//第二种方法
var abs=function(x){
   if(x>=0){
   return x;
   }else {
   return -x;
   }
}
```

JavaScript允许传入任意个参数而不影响调用，因此传入的参数比定义的参数多也没有问题，当然传入的少也没有问题。

```
abs(10,'baabab');//返回10;

abs();  //返回NaN   

```

### arguments

是`javascript`中的关键字，只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数，`arguments`类似于`array`但是它不是个`Array`

```
function foo(x) {
    console.log('x = ' + x); // 10
    for (var i=0; i<arguments.length; i++) {
        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
    }
}
foo(10, 20, 30);

```

### rest参数

为了获取除了已定义参数之外的参数，之前是用arguments，并且循环要从索引n（已定义参数个数）开始来排除已定义的参数。

```
function foo(a, b) {
    var i, rest = [];
    if (arguments.length > 2) {
        for (i = 2; i<arguments.length; i++) {
            rest.push(arguments[i]);
        }
    }
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}
```

ES6之后引入了rest函数，上面的改写为：

```
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// 结果:
// a = 1
// b = undefined
// Array []
```

### 变量作用域

用`var`声明的变量实际上有作用域，如果一个变量在函数体内部声明，则该变量的作用域为整个函数体，函数体外不可引用该变量。

不同函数内部的同名变量互相独立，互不影响。

JavaScript的函数可以嵌套，内部函数可以访问外部函数定义的变量，反过来则不行

##### 变量提升

`JavaScript`的函数定义有个特点，会先扫描整个函数体的语句，把所有申明的变量提升到函数顶部，但是只能提升变量y的 声明，但不会提升变量y的赋值。

```
function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}

//相当于上面函数
function foo() {
    var y; // 提升变量y的申明，此时y为undefined
    var x = 'Hello, ' + y;
    console.log(x);
    y = 'Bob';
}
```

对于`JavaScript`这一怪异的特性，我们在函数内部定义变量时，首先声明所有变量。

##### 全局作用域

不在任何函数内定义的变量就具有全局作用域，实际上，`JavaScript`默认有一个全局对象`window`，全局作用域的变量实际上被绑定到`window`的一个属性

##### 名字空间

全局变量会绑定到`window`，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会照成命名冲突。

减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中。

```
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```

把自己的代码全部放入唯一的名字空间`MYAPP`中，会大大减少全局变量冲突的可能。

##### 局部作用域

由于JavaScript的变量作用域实际上是函数内部，我们在`for`循环等语句块中是无法定义具有局部作用域的变量的：

```
function foo() {
    for (var i=0; i<100; i++) {
        //
    }
    i += 100; // 仍然可以引用变量i
}
```

为了解决块级作用域，ES6引入了新的关键字`let`，用`let`替代`var`可以申明一个块级作用域的变量：

```
function foo() {
    var sum = 0;
    for (let i=0; i<100; i++) {
        sum += i;
    }
    // SyntaxError:
    i += 1;
}
```

##### 常量

ES6标准引入了新的关键字`const`来定义常量，`const`与`let`都具有块级作用域：

```
const PI = 3.14;
PI = 3; // 某些浏览器不报错，但是无效果！
PI; // 3.14
```

### 解构赋值

从ES6开始，JavaScript引入了解构赋值，可以同时对一组变量进行赋值。

什么是解构赋值？我们先看看传统的做法，如何把一个数组的元素分别赋值给几个变量：

```
var array = ['hello', 'JavaScript', 'ES6'];
var x = array[0];
var y = array[1];
var z = array[2];
```

现在，在ES6中，可以使用解构赋值，直接对多个变量同时赋值：

```
var [x, y, z] = ['hello', 'JavaScript', 'ES6'];
console.log('x = ' + x + ', y = ' + y + ', z = ' + z);
```
具体使用如下
```
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};
var {name, age, passport} = person;
console.log('name = ' + name + ', age = ' + age + ', passport = ' + passport);
```

### 方法

绑定到对象上的函数称为方法，就是在内部使用了一个`this`关键字，`this`是一个特殊变量，在一个方法内部，它始终指向当前对象。

```
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;
    }
};

xiaoming.age; // function xiaoming.age()
xiaoming.age(); // 今年调用是25,明年调用就变成26了
```

但是换一种写法

```
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25, 正常结果
getAge(); // NaN
```

单独调用`getAge（）`返回值是NaN，这就是`JavaScript`的一个大坑，

`JavaScript`的函数内部如果调用了`this`，这个`this`指向谁视情况而定。

如果以对象的方法形式调用，该函数的`this`指向被调用的对象，

如果单独调用函数，该函数的`this`指向全局对象，也就是`window`

而且如果这样写也是错误的,要保证`this`的指向正确，必须用obj.xxx()的形式调用。

```
var fn = xiaoming.age; // 先拿到xiaoming的age函数
fn(); // NaN
```

##### apply

虽然在一个独立的函数调用中，根据是否是strict模式，`this`指向`undefined`或`window`，不过，我们还是可以控制`this`的指向的！

要指定函数的`this`指向哪个对象，可以用函数本身的`apply`方法，它接收两个参数，第一个参数就是需要绑定的`this`变量，第二个参数是`Array`，表示函数本身的参数。

用`apply`修复`getAge()`调用：

```
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25
getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空
```

另一个与`apply()`类似的方法是`call()`，唯一区别是：

- `apply()`把参数打包成`Array`再传入；
- `call()`把参数按顺序传入。

比如调用`Math.max(3, 5, 4)`，分别用`apply()`和`call()`实现如下：

```
Math.max.apply(null, [3, 5, 4]); // 5
Math.max.call(null, 3, 5, 4); // 5
```

对普通函数调用，我们通常把`this`绑定为`null`。

### 高阶函数

JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。一个简单的高阶函数如下：

```
function add(x, y, f) {
    return f(x) + f(y);
}
var x = add(-5, 6, Math.abs); // 11
console.log(x);
```

##### map

```
var arr = ['A', 'B', 'C'];
var r = arr.filter(function (element, index, self) {
    console.log(element); // 依次打印'A', 'B', 'C'
    console.log(index); // 依次打印0, 1, 2
    console.log(self); // self就是变量arr
    return true;
});
```