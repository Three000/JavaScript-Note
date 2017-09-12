## 闭包

* 封装私有变量
```
var mult = (function() {
    var cache = {};
    return function() {
        var args = Array.prototype.join.call(arguments, ',');
        console.log(args, typeof args, cache); // 1,2,3: 6 string {1,2,3: 6}
        if (args in cache) {
            return cache[args];
        }
        var a = 1;
        for (var i = 0, l = arguments.length; i < l; i++) {
            a = a * arguments[i];
        }
        return cache[args] = a;
    }
})();
mult(1, 2, 3); // 6
```
* 生命周期

`函数被调用时，局部变量会被销毁，会丢掉请求，通过闭包延长局部变量寿命`
```
var report = (function() {
    var imgs = [];
    return function(src) {
        var img = new Image();
        imgs.push(img);
        img.src = src;
    }
})();
```


## 高阶函数
### 函数可以作为参数传递
* 回调函数
* Array.prototype.sort
### 函数可以作为返回值传递
