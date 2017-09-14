## this

```javascript
window.id = 'div2';
var obj = {
    id: 1,
    click: function() {
        console.log(this.id);
        return (function(d) { // 普通函数 this指向全局
            console.log(this.id) // div2
            document.getElementById('div1').onclick = () => { // 箭头符号this指向代码初始化时候的作用域，所以与onclick无关。
                console.log(this.id); //  div1 ? div 2 ? 1 ？     div2
            }
        })(this)
    }
}
obj.click(); // 作为对象调用 IIFE前的this.id == 1
var a = obj.click;
a(); // 作为普通函数调用 this.id == div2
```


### this 作用域万金油

* 作为对象调用，this指向对象
* 作为普通函数调用，this指向全局
* 作为构造函数调用，this指向构造函数
* 箭头符号指向代码初始化时外层作用域

#

## apply && call
`call是apply语法糖,apply性能优于call`
- 修正this
```javascript
var getId = (function(func) {
    return function() {
        return func.apply(document, arguments);
    }
})(document.getElementById);
getId('id');
```
`Function.prototype.bind`
```javascript
getId = document.getElementById.bind(document);
```