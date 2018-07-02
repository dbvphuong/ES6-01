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
# 1.5 Block Scope: let + const  
### 1.5.1 Compare let and var   
let là câu lệnh khai báo biến ở phạm vi block mà nó dc khai báo.  
var là câu lệnh khai báo biến trong phạm vi function chứa nó.  
### 1.5.2 Closures scope, how do let work in closures, try example below  
```
for (let i = 0; i < 3; i++) {
  let btn = document.getElementById('btn' + i);
  btn.addEventListener('click', () {
    alert(i);
  });
}
```
### 1.5.3 What is const ? Example ?  
const dùng để khai báo 1 hằng số(không thể thay đổi trong quá trình chạy). Nhưng có thể thay đổi giá trị bên trong của giá trị của nó.  
ví dụ:  
```
const a=1;  
var a=2;
a;// báo lỗi vì a đã được khai báo, không thể thay đổi được  
```
### 1.5.4 Exercise: fix code below (anywhere) so the console.log will display true  
```
var x = 2, fns = [];

(function(){
  var x = 5;

  for (var i=0; i<x; i++) {
  }
})();

console.log((x * 2) === fns[x*2]()); // must be true
```
sửa lại là:  
```
var x = 2;
var fns;

(function(){
  var x = 5;

  for (var i=0; i<x; i++) {
  fns = i}
})();

console.log((x * 2) === fns); // true
```
# 1.6 Default Values and the Gather/Spread Operator  
Spread Operator cho phép chuyển đổi 1 chuỗi thành nhiều argument(khi gọi hàm) hoặc thành nhiều phần tử cho array  
Gather Operator cho phép thu thập tham số và được đặt trước dấu ...  
### 1.6.1 Default Values: how to define a functon with default value in ES6 ? And in ES6 ?  
### 1.6.1 Default Values: how to define a functon with default value in ES6 ? And in ES6 ?  
### 1.6.2 Lazy expression, evaluate the following code, how many times g have been called ?  
```
function g() {
  console.log('g');
}

function f(x = g()) {
}

f(1);
f();
f();
```
### 1.6.3 Evaluate the following code  
```
var x = 1;

function f(x = 2, fn = function() { return x }) {
  console.log(fn());
}

f();
```
kết quả ra 2, vì x nhận giá trị là 2 trước.  
### 1.6.4 What's a variadic arguments?  
### 1.6.5 What is arguments in a JavaScript function ?  
### 1.6.6 … operator can be used in 2 differents ways, see code below:  
```
function f(...args) { // gather arguments
}

var x = [1, 2, 3];
var y = [4, 5];
var z = [0, ...x, ...y ]; // spread out
```

z=[0,1,2,3,4,5];
### 1.6.7 In which way the … operator is used in following code  
```
function g(...arr) { // ???
}

var a = [1, 2, 3];
var b = [4, 5, 6];

g(...a, ...b); // ???
```
funcion g() thu thập các giá trị a, b vào.  
### 1.6.8 Exercise: fix the following code so console.log will print true  
```
function f() { }

function g() {
  var a1 = [2, 4];
  var a2 = [6, 8, 10, 12];

  return f();
}

console.log(g().join("") === "281012"); // must print true
```
sửa lại là:  
```
function f() { }

function g() {
  var a1 = [2, 4];
  var a2 = [6, 8, 10, 12];
delete a2[0];
var a2 = [2,...a2];
  return a2;
}

console.log(g().join("") === "281012");
```
# 1.7 Destructuring  
### 1.7.1 What is destructuring ? Example ?  
destructuring là phương pháp giải nén các phần tử của mảng hoặc object thành biến.  
ví dụ:  
```
var [a,b,c,d,e,f] = [1,2,3,4,5,6];  
console.log(a); // 1
console.log(d,c); //4 3
```
### 1.7.2 Can you use destructuring and default values together ? Provide example?  
Có thể sử dụng giá trị default đi cùng với destructuring,giá trị destructoring luôn đè lên giá trị default example:  
```
var[a=1,b=2,c=3] = [5,6];
console.log(a);//5
console.log(b);//6
console.log(c);//3
```
### 1.7.3 Use Array destructuring to swap 2 variables ?  
Hai giá trị biến có thể đc hoán đổi vị trí cho nhau:  
```
var a=4;
var b=7;
var [a,b]=[b,a];
console.log(a);//7
console.log(b);//4
```
### 1.7.4 Dumping values: provide example that extract the 3rd element in an array and don't care about the 1st, 2nd element ? Provide example that swap 2 numbers ?  
```
var [,,c] = [1,2,3];
console.log(c);//3
```
### 1.7.5 Nested Array Destructuring: in case we have an array like this [[1, 2], [3, 4], [5, 6]] use destructuring to extract the number 1 to variabled called a   
trích số 1 từ mảng trên:  
```
var x = [[1,2],[3,4],[5,6]];
var [[a,],,] = x;
console.log(a);
```
### 1.7.6 Chain multiple array destructuring  
var o = {a:[1,2], b:[3,4], c:[5,6]};
### 1.7.7 Object Destructuring: provide an example that use destructuring to extract property in an object ?  
```
var a={x:3 , y:5 , z:"hay noi"};
var {x,y,z} = a;
console.log(x);//3
```
### 1.7.8 Object destructuring with default values ?
```
var {x=2, y=3} = {y:5};
console.log(x);// 2
consolo.log(y);// 5
```
### 1.7.9 Nested Object Destructuring: in case we have an object like this { nested: { a: 10 } }, provide an example that use destructuring to extract value of a in inside nested object  
Dúng destructuring để trích xuất đối tượng trong {nested: {a:10 } }.  
```
var x = {nested: {a:10 } };
var {nested: y} = x;
console.log(y);// {a:10}
```
### 1.7.10 Destructuring and Function Parameters: consider the array destructuring for parameters what will be printed out ?  
```
function fn([ x, y ]) {
  console.log(x, y);
}

fn(1, 2); // sai cú pháp
fn([ 1, 2 ]); // 1 2
fn([ 1 ]); // 1
fn([ ]); // undefined

function g({ a, b, c }) {
  console.log(a, b, c);
}

g({
  a: 1,
  b: 2,
  c: 3
}); // 1 2 3
```
### 1.7.11 Exercise: practice object destructuring, object constructuring  
```
function ajax(url,cb) {
  // fake ajax response:
  cb({
    foo: 2,
    baz: [ 6, 8, 10 ],
    bam: {
      qux: 12
    }
  });
}
function check(data) {
  console.log(
    56 === (
      data.foo +
      data.bar +
      data.baz[0] + data.baz[1] + data.baz[2] +
      data.bam.qux +
      data.bam.qam
    )
  );
}

var defaults = {
  foo: 0,
  bar: 4,
  bam: {
    qux: 0,
    qam: 14
  }
};
function response(/* TODO: object destructuring */) {
  check({
  /* TODO: object constructuring */
  });
}
ajax("http://fun.tld",response);
```
Lời giải  
```
function ajax(url,cb) {
  cb({
    foo: 2,
    baz: [ 6, 8, 10 ],
    bam: {
      qux: 12
    }
  });
}
function check(data) {
  console.log(
    56 === (
      data.foo +
      data.bar +
      data.baz[0] + data.baz[1] + data.baz[2] +
      data.bam.qux +
      data.bam.qam
    )
  );
}
var defaults = {
  foo: 0,
  bar: 4,
  bam: {
    qux: 0,
    qam: 14
  }
};
function response({foo,
                  bar = defaults.bar ,
                  baz,
                  bam: {qux ,
                        qam = defaults.bam.qam
                      }
            }) {
  check({ foo,
          bar,
          baz,
          bam:{qux,
		qam}
  });
}
ajax("http://fun.tld",response);
```
# 1.8 Object Literal Extensions  
### 1.8.1 Concise properties: consider the following code what do you think ?  
```
var x = 2, y = 3;
var o1 = {
  x: x,
  y: y
}
var o2 = {
  x,
  y
}
console.log(o1); // {x:2, y:3}
console.log(o2); // {x:2, y:3}
```
### 1.8.2 Concise Methods: consider the following code what do you think ?  
```
var o1 = {
  x: function() {
    console.log('o1.x');
  },
  y: function() { }
}
o1.x();// o1.x
var o2 = {
  x() {
     console.log('o2.x');
  },
  y() {}
}
o2.x();// o2.x
```
vì var x = function (){} bằng với function x(){}  
### 1.8.3 ES5 Getter/Setter: consider the following code  
```
var o = {
  _id: 10,
  get id() { return this._id++; },
  set id(v) { this._id = v; }
}
o.id; // 10
o.id = 100;
o.id; // 100?
```
get, set là lấy giá trị hàm ra và thay đổi giá trị chúng.  

# 1.9 Template Strings  
### 1.9.1 Template Strings: what is template strings ?  
template strings là dùng ` ` để thu gọn cách viết chuỗi.  
Cú pháp:  
dấu xuống dòng là xuống dòng, ${expression} là chèn biểu thức.
### 1.9.2 Consider this code below, rewrite it using ES6 template string  
```
var name = 'That Duy';
var chaoDuy = 'Hello ' + name + '!';

console.log(chaoDuy);
console.log(typeof chaoDuy);
```
viết lại:  
```
var name = 'That Duy';
var chaoDuy = `Hello ${name}!`;

console.log(chaoDuy);
console.log(typeof chaoDuy);
```
### 1.9.3 Interpolated Expression: can we use function inside ${…} if yes provide an example
```
var a = ` toi la ${1+2}`;  
console.log(a);// toi la 3  
```
### 1.9.4 Tag Functions: consider the code below  
```function f(strings, ...values) {
  console.log(strings);
  console.log(values);
}

var s = 'Fresher Academy';
f`Hello ${s}`; // ["Hello ","", ["Hello ",""]]
                  ["Fresher Academy"]
```
### 1.9.5 Exercise  
```
function upper(strings,...values) {
  // TODO
}
var name = 'Nguyen Van A',
  account = 'anv',
  classname = 'Fresher Academy ES6';

console.log(
  `Hello ____ (@____), welcome to the ____!` ===
  'Hello NGUYEN VAN A (@ANV), welcome to the FRESHER ACADEMY ES6!'
);
```
bai lam:  
```
function upper(strings,...values) {
var text = "";
  for(var i = 0; i< strings.length; i++){
    if(i< values.length){text += strings[i] + values[i].toUpperCase();}
    else{text += strings[i];}
  }
return text;
}
var name = 'Nguyen Van A',
  account = 'anv',
  classname = 'Fresher Academy ES6';
console.log(
  upper`Hello ${name} (@${account}), welcome to the ${classname}!` ===
  'Hello NGUYEN VAN A (@ANV), welcome to the FRESHER ACADEMY ES6!'
);
```
# 1.10 Modules  
### 1.10.1 What is module pattern ?  
Mô hình module là chương trình được chia làm nhiều phần, mỗi phần là 1 module,trong module chứa code và có tính tự đóng gói cao.  
### 1.10.2 What is ES6 import/export ?  
Cách nhập(import):  
import {tên module} "module.js"  
tên module là tên module do mình đặt, module.js là nơi chứa file module gắn với biến tên module.  

Cách xuất(export):  
export{tên module cần xuất};
### 1.10.3 What is export default ? How to import a exported default function ?  
Xuất giá trị mặc định hàm:  
export default function(){};  
Xuất giá trị mặc định lớp:  
export default class{};  
Cách xuất 1 giá trị mặc định từ function:  
import ten from "noi chua module";  
export default ten;
### 1.10.4 Circular Module Dependency: A imports B, B imports A, how does this work ?  

# 1.11 Module Loaders  

# 1.12 Collections  
### Map  
map luôn có dạng key=>value. key ở đây có thể là string, number,const,NaN.  
Khởi tạo: var a = new Map()  
Thêm phần tử: a.set('Name', 'Cao phương');  
Xóa phần tử: a.delete("Name");  
Kiểm tra phần tử tồn tại: a.has('Name')  
Đếm tổng số phần tử: a.size  
Xóa toàn bộ phần tử: a.clear();  

Bài lọc array:  
```
var arr = [1,2,3,4,6,2,4];
var mymap = new Map();
var arr1=[];
for(var i=0; i<arr.length; i++){
  mymap.set(arr[i],arr[i]);
}
console.log(mymap);
for(var[key,value] of mymap){
  arr1.push(key);
}
console.log(arr1)
```
# 1.13 Proxies  
### 1.15.1 Array add of(..), from(..)* and fill(..). Provide example using them  
Array.of() là 1 phương pháp tạo array mới.  
fill(giá trị cần điền, giá trị đầu, giá trị cuối) dùng để điền giá trị mặc định vào 1 array.  
ten_array.from() là sao chép 1 array mới có giá trị đúng bằng ten_array.  
