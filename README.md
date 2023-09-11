# jim-emacs-fun-es6 JavaScript函数式的列表(如果必要的化引入流行的函数式的库, 如underscore.js)

- [jim-emacs-fun-es6 JavaScript函数式的列表(如果必要的化引入流行的函数式的库, 如underscore.js)](#jim-emacs-fun-es6-javascript%E5%87%BD%E6%95%B0%E5%BC%8F%E7%9A%84%E5%88%97%E8%A1%A8%E5%A6%82%E6%9E%9C%E5%BF%85%E8%A6%81%E7%9A%84%E5%8C%96%E5%BC%95%E5%85%A5%E6%B5%81%E8%A1%8C%E7%9A%84%E5%87%BD%E6%95%B0%E5%BC%8F%E7%9A%84%E5%BA%93-%E5%A6%82underscorejs)
  - [相关资源](#%E7%9B%B8%E5%85%B3%E8%B5%84%E6%BA%90)
    - [python函数式的列表](#python%E5%87%BD%E6%95%B0%E5%BC%8F%E7%9A%84%E5%88%97%E8%A1%A8)
    - [Functional CSS的列表](#functional-css%E7%9A%84%E5%88%97%E8%A1%A8)
    - [R function programming list](#r-function-programming-list)
  - [lambda](#lambda)
  - [map](#map)
  - [filter](#filter)
  - [doseq](#doseq)
  - [reduce](#reduce)
  - [sort](#sort)
  - [flatten](#flatten)
  - [slice](#slice)
  - [splice](#splice)
  - [concat](#concat)
  - [combinations](#combinations)
  - [permutations](#permutations)

## 相关资源
### [python函数式的列表](https://github.com/FPTensorFlow/jim-emacs-fun-py)
### [Functional CSS的列表](https://github.com/chanshunli/jim-emacs-fun-tachyons-flex-css)
### [R function programming list](https://github.com/chanshunli/jim-emacs-fun-r-lisp)

## lambda

``` javascript
let fn = ( [a, b] ) => {
    return a + b
}
fn([1, 2]) //=> 3

```

## map

``` javascript
[[1,2],[3,4]].map((a, b) => a + b) //=> [ '1,20', '3,41' ]

[{id: 1, content: "bbb"},
 {id: 2, content: "ccc"}].map(item => {
     if (item.id === 2) {
         var temp = Object.assign({}, item); // 相当于Clojure的merge操作
         temp.content = "eeee";
         return temp;
     } else {
         return item;
     }
 }) // => [ { id: 1, content: 'bbb' }, { id: 2, content: 'eeee' } ]

```
## filter

``` javascript
['a',,'b'].filter(x => true) //=> [ 'a', 'b' ]
```

## doseq

``` javascript
[,'a'].forEach((x,i) => console.log(i)) //=> 1, undefined
```

## reduce

``` javascript
[1,,2].reduce((x,y) => x+y) //=> 3
```
## sort

``` javascript
const unsorted_object = {
    '0001': '13.1666',
    '0002': '11.0001',
    '0003': '10.6664',
    '0004': '13.1666',
    '0005': '7.3331',
};

const sorted_object = Object.entries(unsorted_object)
      .sort(([,v1], [,v2]) => +v2 - +v1)
      .reduce((r, [k, v]) => ({ ...r, [k]: v }), {});

//=>
{
  '0001': '13.1666',
  '0004': '13.1666',
  '0002': '11.0001',
  '0003': '10.6664',
  '0005': '7.3331'
}
```
## flatten

``` javascript
[1, 2, [3, 4]].flat()
//=> [ 1, 2, 3, 4 ]
```
## slice

``` javascript
[ 1, 2, 3, 4 ].slice(1, 2)
//=> [ 2 ]
```
## splice

``` javascript
[ 1, 2, 3, 4 ].splice(2)
//=> [ 3, 4 ]
```

## concat

``` javascript
[ 1, 2, 3, 4 ].concat([8, 9])
//=> [ 1, 2, 3, 4, 8, 9 ]
```
## combinations

``` javascript
var array = ["apple", "banana", "lemon", "mango"];

var result = array.flatMap(
    (v, i) => array.slice(i+1).map( w => v + ' ' + w )
);
//=>
[
  'apple banana',
  'apple lemon',
  'apple mango',
  'banana lemon',
  'banana mango',
  'lemon mango'
]
// or
var result = array.reduce( (acc, v, i) =>
    acc.concat(array.slice(i+1).map( w => v + ' ' + w )),
    []);
// or
var result = [].concat(...array.map(
    (v, i) => array.slice(i+1).map( w => v + ' ' + w ))
);
```
## permutations

``` javascript
const stringPermutations = str => {
    if (str.length <= 2) return str.length === 2 ? [str, str[1] + str[0]] : [str];
    return str
        .split('')
        .reduce(
            (acc, letter, i) =>
            acc.concat(stringPermutations(str.slice(0, i) + str.slice(i + 1)).map(val => letter + val)),
            []
        );
};
stringPermutations('abc')
//=> [ 'abc', 'acb', 'bac', 'bca', 'cab', 'cba' ]
```
## JavaScript递归

https://juejin.cn/post/7109287042613248013

本文总结了几个笔者在项目中经常使用的几个处理数形结构数据的递归方法，比如树形结构转成数组，寻找某节点的所有祖先节点，寻找某节点的所有子孙节点等，欢迎阅读~
给节点加level属性
某需求要使用节点的层数进行一些判断，后台返回数据没有层数对应的属性，此时可以使用递归方法为节点增加level属性：

```js
calculateLevel(arr, initLevel) {
    arr.forEach(element => {
      element.level = initLevel
      if(element.children){
        this.calculateLevel(element.children, initLevel + 1)
      }
    });
    return arr
  },
```
arr为节点数组，initLevel为初始层数（一般设置为0或者1）。遍历节点数组，数组每一个元素的level属性设置为initLevel。如果节点存在子节点则递归调用方法，注意第二个参数为initLevel + 1，因为子节点的层数要增加。
给节点加disabled属性
需求规定属性节点的层次数超过某个值之后，就不允许选择了，此时可以使用递归方法为节点增加禁用属性：
```js
  calculateDisable(arr, disLevel) {
    arr.forEach(element => {
      if (element.level >= disLevel) {
        element.disabled = true
      } else {
        element.disabled = false
      }
      if(element.children){
        this.calculateDisable(element.children, disLevel)
      }
    });
    return arr
  },
```
arr为节点数组，disLevel为要求的层数。遍历节点数组，检查节点的层数，如果层数超过disLevel则禁用属性为true否则为false。检查完当前节点后递归检查子节点。
树形结构转换为数组
将树形结构转为数组，然后用这个数组再做一些判断是经常遇到的场景，如下方法实现了将树形结构转换为数组：
```js
// 将递归的树结构展开为数组
const flatFunc = (res, data) => {
  // 递归出口
  if (!data.childrenList) {
    res.push({
      id: data.id,
      name: data.name,
      pid: data.pid,
      type: data.type,
      checked: data.checked
    })
    return
  }
  res.push({
    id: data.id,
    name: data.name,
    pid: data.pid,
    type: data.type,
    checked: data.checked
  })
  // 递归处理子节点
  for (let i = 0; i < data.childrenList.length; i++) {
    flatFunc(res, data.childrenList[i])
  }
}
```
flatFunc方法用于将树形结构转成数组，参数为结果数组res和树形结构数据data。如果data不存在子节点数组则将data放入结果集res中，退出递归方法。如果data存在子节点数组，那么data放入结果集后还要遍历子节点数组中的每一个元素进行递归处理。
寻找所有子孙节点
遇到了寻找某个节点的所有子孙节点（注意是子孙！不是儿子！）的需求，可以使用如下的代码来解决：
```js
// 在source数组中寻找item节点的所有子孙节点，结果存放于res
const getItemChildren = (res, source, item) => {
  // 递归出口
  if (item.childrenList === null) {
    return res
  }
  const childNode = source.filter((childItem) => {
    if (childItem.pid === item.id) {
      return childItem
    }
  })
  if (childNode.length === 0) {
    return res
  } else {
    // 孩子节点放入结果集中
    childNode.forEach((node) => res.push(node.id))
    // 寻找每一个孩子节点的子孙节点
    childNode.forEach((node) => {
      // 每一个孩子节点递归调用
      getItemChildren(res, rource, node)
    })
  }
}
```
res是结果数组，调用的时候传一个空数组即可。source是树形结构数据转换后的数组，item是目标元素。item的子节点数组如果是空则返回。遍历source数组中的每一元素，如果某个节点的pid等于item的id则说明此节点是当前节点的孩子节点。如果孩子节点数组不为空，首先将这些孩子节点放入结果集中，然后递归寻找每一个孩子节点的子孙节点。
寻找所有祖先节点
如果遇到了要寻找某个节点的所有祖先节点（父节点、爷爷节点......），则可以使用如下的代码：
```js
// 在source数组中寻找item节点的所有祖先节点，结果存放于res
const getItemAncestors = (res, source, item) => {
  // 递归出口
  if (item.pid === null) {
    return res
  }
  const parentNode = source.filter((parentItem) => {
    if (parentItem.id === item.pid) {
      return parentItem
    }
  })
  if (parentNode.length === 0) {
    return res
  } else {
    // 父节点存在
    res.push(parentNode[0].id)
    getItemAncestors(res, rource, parentNode[0])
  }
}
```
res是结果集, source是树形数据转换后的数组, item是目标元素。如果当前节点的pid为null说明它没有父节点，返回。否则在source中找到item的父节点。如果父节点存在则放入到结果集中并递归寻找父节点的祖先节点。
