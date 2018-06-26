## 实现如下功能
```js
window.jQuery = ???
window.$ = jQuery

var $div = $('div')
$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi
```

## 实现思路（根据需求推倒）
* 传入一个选择符参数
* 调用返回一个普通对象，含有 `addClass` 和 `textContent` 方法
* 对象的方法，要访问外层函数作用域中的变量（即选择符），此处产生一个闭包使得选择符变量拥有更长的生命周期。


## 代码实现
```js 
function jQuery(selector) {
  const element = document.querySelectorAll(selector);
  return {
    addClass: function(className) {
      [...element].forEach(item => item.classList.add(className));
    },
    setText: function(text) {
      [...element].forEach(item => item.textContent = text);
    },
  };
}
```