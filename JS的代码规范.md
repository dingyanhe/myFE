#JS的代码规范

引自[这里](https://github.com/yuche/javascript)

## 类型
1. **基本数据类型**
	* 字符串
	* 数值
	* 布尔类型
	* `null`
	* `undefined`
```javascript
	const foo = 1;
	let bar = foo;
	bar = 9;
	console.log(foo, bar); // 1, 9
```

2. 复杂数据类型
	* 对象
	* 数组
	* 函数
```javascript
	const foo = [1, 2];
	const bar = foo;
	bar[0] = 9;
	console.log(foo[0], bar[0]);
```

## 引用
1. 对所有的引用使用`const`,不要使用`var`。

	> **？**这样能确保你无法对引用变量重新赋值，也不会导致出现BUG或难以理解。

```javascript
	// bad
	var a = 1;
	var b = 2;

	// good
	const a = 1;
	const b = 2;
```

2. 如果你一定要可变动的引用，使用`let`代替`var`。

	> **？**因为`let`是块级作用域，而`var`是函数作用域。

```javascript
	// bad
	var count = 1;
	if(true){
		count ++;
	}

	// good, use the let
	let counter = 1;
	if(true){
		counter++;
	}
```

3. 注意`let`和`const`都是块级作用域。

```javascript
	// `const`和`let`只存在于他们被定义的区域内
	{
		let a =1;
		const b = 1;
	}
	console.log(a); // Uncaught ReferenceError: a is not defined
	console.log(b); // Uncaught ReferenceError: b is not defined
```

## 对象
1. 使用字面量创建对象。
```javascript
// bad
const item = new Object();

// good
const item = {};
```

2. 如果你的代码在浏览器环境下执行，别使用*保留字*作为键值。
```javascript
// bad
const superman = {
  default: { clark: 'kent' },
  private: true,
};

// good
const superman = {
  defaults: { clark: 'kent' },
  hidden: true,
};
```

3. 使用同义词替换需要使用的保留字。
```javascript
// bad
const superman = {
  class: 'alien',
};

// bad
const superman = {
  klass: 'alien',
};

// good
const superman = {
  type: 'alien',
};
```

4. 创建有动态属性名的对象时，使用可被计算的属性名称。

	> **?**因为这样可以让你在一个地方定义所有的对象属性。

```javascript
function getKey(k) {
  return `a key named ${k}`;
}

// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

5. 使用对象方法的简写。

```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

6. 使用对象属性的简写。

	> **?**更短更有描述性

```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
};
```

7. 在对象属性声明前把简写的属性分组。

	> **?**这样更能清楚地看出哪些属性使用了简写。

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  episodeOne: 1,
  twoJedisWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};

// good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJedisWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};
```


### 未完待续...
