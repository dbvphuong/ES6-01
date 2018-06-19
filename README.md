# ES6-01  

# 1.1 Reference:  
1.1.1 ES6: http://blog.thefirehoseproject.com/posts/12-reasons-es6-future-javascript-web-development/  
1.1.2 ES6 Features  
https://github.com/lukehoban/  
http://es6-features.org/#Constants  
1.1.3 JS Engines: https://developer.telerik.com/featured/a-guide-to-javascript-engines-for-idiots/  
1.1.4 Transpilers: https://scotch.io/tutorials/javascript-transpilers-what-they-are-why-we-need-them  
# 1.2 History  
### 1.2.1 What's is ECMAScript ?  
ECMAScript là tiêu chuẩn của ngôn ngữ javascript.  
### 1.2.2 What is JavaScript Engine ? Can you name a few JavaScript Engine used in some popular Browsers such as Chrome, Firefox, IE 
        
Javascript Engine là một quá trình máy ảo thông dịch và thực thi code javascript.  
1 vài javascript engine như v8-chorm, SpiderMonkey-firefox.  
### 1.2.3 What is Future JavaScript ?  
future javascript is ES6.  
### 1.2.4 What is problem you have if you want to use Future JavaScript in Present Browsers?  

### 1.2.5 What is transpiler ?  

### 1.2.6 What is Babel ? Try Babel online here: https://babeljs.io/repl/  
Babel là công cụ dùng để chuyển đổi code javascript từ phiên bản mới về phiên bản cũ hơn để các trình duyệt không đọc được bản ES mới có thể đọc hiểu được.  
# 1.3 Arrow Function  
### 1.3.1 Arrow Function syntax ?  
Tên_function = (a,b) => {nội dung function};  
Tương đương với:  
Tên_function(a,b){nội dung function};
### 1.3.2 Compare arrow function syntax to ES5 function syntax ?  
Khác về cách khai báo hàm(ở ES5 thì có chữ function trước tên hàm, còn ở ES6 thì mất chữ function nhưng thêm dấu suy ra sau tên hàm.)  
### 1.3.3 Các biến thể của hàm Arrow, hãy thử chúng trong Babel Repl, sửa lỗi nếu có  

### 1.3.4 True or false: arrow functions are anonymous ?  
const myFunc = x => 4;  
console.log(myFunc.name);  
True, vì hàm chỉ có 1 biến x nên không cần ngoặc đơn  
### 1.3.5 Disadvantages: lost reference outside callback, hard to debug in stack strace  

### 1.3.6 this  
Evaluate the code below, can you explain what happens ?  
```
var obj = {
  a: 10,
  method: function method() {
    setTimeout(function () {
        console.log(this.a);
    }, 200);
  }
}

var obj2 = {
  a: 10,
  method: function method() {
    setTimeout(() => {
        console.log(this.a);
    }, 200);
  }
}

obj.method(); // ??
obj2.mthod();
```
