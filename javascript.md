# 错题集合

## 写在前面

本篇文章仅记录本人平时刷题时犯的错误。内含大量基础题，因为想要夯实基础，所以平时会多刷一些基础题。

### 12.14及之前

- 代码输出

  ```js
  var name = 10;
  var obj = {};
  console.log(name + 10 + obj)
  //'1010[Object,Object]'
  ```

  > + HTML DOM name属性 (window.name)
  >
  >   name 属性可设置或返回存放窗口的名称的一个<u>字符串</u>。[来源](https://www.w3school.com.cn/jsref/prop_win_name.asp)
  >
  > + 对象转字符串时默认结果：[Object Object]

- 代码输出

  ```js
  (function() {
      var x=foo();
      var foo=function foo() {
          return "foobar"
      };
      return x;
  })();
  //Uncaught TypeError: foo is not a function
  ```

  > - 声明提升
  >
  >   > ```js
  >   > var x = foo();
  >   > var foo=function foo() {...}
  >   > ```
  >
  >   声明提升，函数体不提升，上述代码可以写为：
  >
  >   > ```js
  >   > var foo;
  >   > var x = foo();
  >   > foo = function foo() {...}
  >   > ```
  >   >
  >   > 执行到x = foo()时，foo()未被定义为函数，所以输出：Uncaught TypeError: foo is not a function

- 代码输出

  ```js
  var myObject = {
      foo: "bar",
      func: function() {
          var self = this;
          console.log(this.foo);  
          console.log(self.foo);  
          (function() {
              console.log(this.foo);  
              console.log(self.foo);  
          }());
      }
  };
  myObject.func();
  //"bar"
  //"bar"
  //undefined
  //"bar"
  ```

  > - this 指向
  >
  > - 匿名函数具有全局作用域
  >
  >   第一个输出：this 指向myObject对象
  >
  >   第二个输出：self是this的副本，同指向myObject对象
  >
  >   第三个输出：匿名函数的执行是全局的。匿名函数this指向window.
  >
  >   第三个输出：因为匿名函数所处的上下文中没有self，所以通过作用域链向上查找，从包含它的父函数中找到了指向myObject对象的self