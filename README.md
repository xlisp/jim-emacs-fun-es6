<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [jim-emacs-fun-es6 JavaScript函数式的列表(如果必要的化引入流行的函数式的库)](#jim-emacs-fun-es6-javascript%E5%87%BD%E6%95%B0%E5%BC%8F%E7%9A%84%E5%88%97%E8%A1%A8%E5%A6%82%E6%9E%9C%E5%BF%85%E8%A6%81%E7%9A%84%E5%8C%96%E5%BC%95%E5%85%A5%E6%B5%81%E8%A1%8C%E7%9A%84%E5%87%BD%E6%95%B0%E5%BC%8F%E7%9A%84%E5%BA%93)
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

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### jim-emacs-fun-es6 JavaScript函数式的列表(如果必要的化引入流行的函数式的库)

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
