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

obj.method(); // undefined
obj2.mthod(); // 10
```
Vì ở obj thì this trỏ tới window. còn ở obj2 thì do không có function ở trong setTimeout nên this sẽ trỏ đến obj2 .  

### 1.3.7 Promise  
Compare 2 Promise call below, what do you think ? If v is null or undefined what will happend ? How you handle that ?  
```
p.then(function (v) { return v.id });

p.then(v => v.id);
```
2 cấu trúc trên tương đương nhau.  
nếu v là null thì viết lại là:  
```
p.then(function () { return v.id });

p.then(() => v.id);
```
### 1.3.8 Exercise 01: rewrite all function below with arrow functions and try to avoid curly braces {} as much as possible  
```(function iife(){

  function foo(x) {
    var y = x * 2;

    return function bar(z) {
      if (z.length > 3) {
        return z.map( function baz(v){
          if (v > 3) return v + y;
          else return baz( v * 4 );
        } );
      }
      else {
        var obj = [];

        setTimeout( function bam(){
          obj.length = 1;
          obj[0] = this.w;
        }.bind( this ), 100 );

        return obj;
      }
    };
  }

  var p = foo( 2 );
  var list1 = [1,3,4];
  var list2 = list1.concat( 6 );

  list1 = p.call( { w: 42 }, list1 );
  list2 = p( list2 );

  setTimeout( function(){
    console.log( list1[0] === list2.reduce( function(s,v){
      return s + v;
    }, 0 ) );
  }, 200 );
})();
```
viết lại là:  
```
( iife = () => {

foo=(x)=> {
  var y = x * 2;

  return function bar(z) {
    if (z.length > 3) {
      return z.map( function baz(v){
        if (v > 3) return v + y;
        else return baz( v * 4 );
      } );
    }
    else {
      var obj = [];

      setTimeout( function bam(){
        obj.length = 1;
        obj[0] = this.w;
      }.bind( this), 100 );

      return obj;
    }
  };
}

var p = foo( 2 );
var list1 = [1,3,4];
var list2 = list1.concat( 6 );

list1 = p.call( { w: 42 }, list1 );
list2 = p( list2 );

setTimeout( () => {
  console.log( list1[0] === list2.reduce( (s,v) => {
    return s + v;
  }, 0 ) );
}, 200 );
})();
```
# 1.4 Classes  
### 1.4.1 Provide an example to create a new classed named Person which have 2 fields: id, name and 1 method: sayHello which print hello to the console 
```
class Person {
constructor(id,name){
this.so = id;
this.name = name;}
sayHello(){
console.log("hello" + this.name + this.so )
}
}
var phuong= new Person(10,"Phuong");
phuong.sayHello();
```
### 1.4.2 What is keyword extends and super, provide an example that used both keyword ?  
extends dùng để truyền giá trị của cha cho con.  
cú pháp: class con extends cha {};
super dùng để gọi các hàm trên đối tượng cha.  
### 1.4.3 Consider the following code, what will be printed out?  
```
class Cha {
  constructor() { this.id = 'a' }
  method() {
    console.log('Cha', this.id)
  }
}

class Con extends Cha {
  method() {
    super.method();
    console.log('Con', this.id)
  }
}
```
Hiển thị ra:  
Cha a  
Con a  
vì hàm Con được nhận các giá trị của hàm method() nhờ super.method()  
### 1.4.4 What is static keyword ?   
là gọi super trên một function có giá trị cố định.  
