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
