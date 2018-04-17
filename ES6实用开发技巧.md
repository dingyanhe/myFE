
## 定义变量/常量
  ES6 中新增加了 let 和 const 两个命令，let 用于定义变量，const 用于定义常量。
  两个命令与原有的 var 命令所不同的地方在于，let, const 都是块级作用域，其有效范围仅在代码块中，实例如下：
  
  ```javascript
  // ES5
  if(true) {
    var b = 'foo';
  }
  console.log(b); // foo

  //es6
   if(true) {
    var a = 'foo';
  }
  console.log(a); // undefined
  ```

> 定义常量对象
```javascript
const a = {a:1, b: 2};
a.b=3;
console.log(a); // {a:1, b: 3}
```
上例中，常量 a 中的内容在定义后，再进行修改依然有效，原因是对于对象类型的使用是指针式引用，常量只是指向了对象的指针，对象本身的内容却依然可以被修改，注意，数组(Array) 也是对象； 那么如果在定义常量时使用基础数据类型：string, number, boolean 等。

```javascript
const a = 1;
a = 2; // Uncaught TypeError: Assiginment to constant variable.
```
在使用中建议使用let和const完全替代var命令。

## 数值扩展

> 字符串内容测试

```javascript
'abcdef'.includes('c'); // true
'abcdef'.includes('ye'); // false
'abcdef'.startsWith('a'); // true
'abcdef'.endsWith('a'); // false


// includes、startsWith、endsWith都支持第二个参数
// 第二个参数的类型是数字类型，意为从第N个字符开始，endsEith是别例
'abcdef'.includes('c', 4); // false 从第5个参数开始查找
'abcdef'.startsWith('d', 3); // true 从第4个字符开始查找是否以d这个字符开头
'abcdef'.endsWith('d', 4); // true 前面的4个字符里，是否以d结尾
```

> 字符串内容重复输出

```javascript
'a'.repeat(5); // aaaaa 重复输出5遍（算上自身）
```

> 原生模板支持
```javascript
  //es5 
  $('body').append(
    '1' + count + '2'+
    '3' + index + '4' + 
    'ex';
  );

  //es6 
  $('body').append(`
    1${count}23${index}4ex
  `)
```

> 字符串遍历输出
```javascript
// for...of 格式是ES6中的Iterator迭代器输出方式
for(let c of 'acbadf'){
  console.log(c);
}
```

> 字符串补全
```javascript
// 参数一：生成的字符串长度
// 参数二：进行补全的字符串
'12345'.padStart(7, '0'); //0012345 
'12345'.padEnd(7, '0'); // 1234500
```

### 数组拓展
> 合并数组
```javascript
let a = [1,2,3];
let b = [4,5];
let c = [7,8,9];
let d = [...a, ...b, ...c]; // [1,2,3,4,5,7,8,9] 不会去重
```

> 快速转换数组
```javascript
Array.of(3,4,5); // [3,4,5]
```


> 数组内容测试
```javascript
// 判断对象是否是数组
if(Array.isArray(obj)){...}

[1,2,3].includes(5); // false检索数据中是否有5

// 找出第一个匹配表达式结果，注意是只要匹配到一项，函数即返回
let a = [1,3,-4,10].find(function(value, index, arr){
  return value < 0;
});
console.log(a); // -4

// 找到第一个匹配表达式结果的所有下表
let a = [1,3,-4,10].findIndex(function(value, index, arr){
  return value > 0;
});
console.log(a); // [1,3,4]
```

> 内容过滤
```javascript
let a = [1,3,-4,10].filter(function(item){
  return item > 0;
});
console.log(a);// [1,3,10]
```

> 内容实例

    Object.keys()-获取对象中所有元素的键名（实际是下标，或者索引）
    Object.values()-获取数组中所有元素的数据
    Object.entries()-获得数组中所有的数据的键名和值
```javascript
for(let index of Object.keys(['a', 'b'])){
  console.log(index);
} // 0， 1

for(let ele of Object.values(['a', 'b'])){
  console.log(ele);
} // a,b

for(let [index, ele] of Object.entries(['a', 'b'])){
  console.log(index, ele);
} // 0 a, 1 b
```

### 对象扩展
> 属性的简介表示
```javascript
// 直接是同变量常量的名称为一个对象属性的名称
let a = 'abc';
let b = {a}; // {a: 'abc'}

function f(x, y){
  return {x, y};
}
// 等效于
function f(x, y){
  return {x: x, y: y};
}

let o = {
  f(){ return 1; }
}
// 等效于
let o = {
  f: function(){ return 1; }
}
```

> 判定对象是否数组
```javascript
if(Object.isArray(someObj)){...}
```

> 对象内容合并
```javascript
let a = {a:1,b:2}，b = {b:3}, c={b:4, c:5};
let d = Object.assign(a,b,c);
console.log(d); // {a:1, b:4, c:5}
console.log(a); // {a:1, b:4}
// 上面的合并方式会同时更新a对象的内容，a的属性如果有多次合并会被更新，
// 但自身没有的属性，其它对象有的属性不会被添加到a身上；
// 参数列表中的对象只会影响第一个，后面的参数对象不会被被修改。

// 推荐使用下面的方式来进行对象的合并
let a = {a:1,b:2}，b = {b:3}, c={b:4, c:5};
let d = Object.assign({},a,b,c); //第一个参数增加一个空对象，在合并时让它被更新，不影响实际的对象变量内容
console.log(d);//{a:1,b:4,c:5}//与上面的方式合并结果一致，使用这种方式, a 对象的内容就不会被影响了
```
对象内容合并的方向是按参数顺序进行合并
> 对象内容集合

Object.keys()-获取对象中所有元素的键名（实际是下标，或者索引）
```javascript
var obj = { a:1, b:2 };
var names = Object.keys(obj); // [a, b]
```
Object.values()-获取数组中所有元素的数据
```javascript
var obj = { a:1, b:2 };
var names = Object.values(obj); // [1, 2]
```
Object.entries()-获得数组中所有的数据的键名和值
```javascript
var obj = { a:1, b:2 };
var names = Object.values(obj); // [a=>1, b=>2]或[[a,1],[b,2]]
```
其实观察可发现，Object.keys(), Object.values(), Object.entries()，与 Java 的 MAP 中的方法是一致的，不论是方法名还是具体的用法，这也可以帮忙理解这些功能 API
### 结构赋值
```javascript
let [a,b,c] = [1,2,3];
// 定义了三个变量，并对应复制，如果参数不匹配则从前向后匹配，没有对应的就undefined赋值

let [a, b, c="default"] = [1,2]

let [a, ...b] = [1,2,3]

let [a,b,c] = 'yes'; // a-y,b-e,c-s

let {length} = 'yes'; // 3

let arr = [1,2]
let obj = {a:1, b:2};
function test({a = 10, b}){
  console.log('a: ', a);
  console.log('b: ', b);
}
test(obj);
```
> 对象的解构
```javascript
let obj = {a: 1, b:2};
let {a, b} = obj;

let obj = {a: 1, b:2};
let {a=0,b=5} = obj;

let obj = {a: 1, b:2};
let {a:A,b=5} = obj;

let obj = {a: 1, b:2};
let a = 0;
({a,b} = obj);

let obj = {
  arr: ['aaa', {a:1}]
};
let {arr:[b, {a}]} = obj;
```

### 模块化
> 最简单实例的场景
```javascript
// a.js
let a ={a:1,b:2,c:3}
export default a;

// b.js
import a from 'a.js'
console.log(a.a); // 1
```
以上简单的实例就两个脚本文件举例说明了两个文件在实际使用，可以进行互相引用，并获得目标文件中的数据；我们可以认为一个脚本文件就是一个 模块，那么在实际开发过程中，可以将业务处理内容，或是数据处理过程 抽象 在一个文件中，在需要使用时，由其它模块引入并使用其中的数据