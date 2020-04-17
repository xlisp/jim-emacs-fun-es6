### jim-emacs-fun-es6 JavaScript函数式的列表(如果必要的化引入流行的函数式的库)

* [python函数式的列表](https://github.com/FPTensorFlow/jim-emacs-fun-py)

* lambda

``` javascript
let fn = ( [a, b] ) => {
    return a + b
}
fn([1, 2]) //=> 3

```

* map

``` javascript
[[1,2],[3,4]].map((a, b) => a + b) //=> [ '1,20', '3,41' ]
```
* filter

``` javascript
['a',,'b'].filter(x => true) //=> [ 'a', 'b' ]
```

* doseq

``` javascript
[,'a'].forEach((x,i) => console.log(i)) //=> 1, undefined
```

* reduce

``` javascript
[1,,2].reduce((x,y) => x+y) //=> 3
```
* sort

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
* flatten

``` javascript
[1, 2, [3, 4]].flat()
//=> [ 1, 2, 3, 4 ]
```
* slice

``` javascript
[ 1, 2, 3, 4 ].slice(1, 2)
//=> [ 2 ]
```
* splice

``` javascript
[ 1, 2, 3, 4 ].splice(2)
//=> [ 3, 4 ]
```

* concat

``` javascript
[ 1, 2, 3, 4 ].concat([8, 9])
//=> [ 1, 2, 3, 4, 8, 9 ]
```
* combinations

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
```
