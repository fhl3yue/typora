### let const 

$let$  局部声明

$const $ 全局声明



**String Number Boolean null undefined**

字符串，数字，布尔值，空值，未定义

```javascript
console.log(typeof A);  // A 的类型
```

**连接  & 模板字符串**

```const username = "dzk";
const username = "dzk";
const age = 20;
const hello = `My name is ${username} and I am ${age}`;
console.log(hello);
console.log("My name is " + username + " and I am " + age);
```

**字符串函数**

```javascript
const s = "Hello World!";
const A = "dzk,like,kan,p";
console.log(s.length); // 12
console.log(s.toUpperCase()); // HELLO WORLD!
console.log(s.toLowerCase()); // hello world!
console.log(s.substring(0, 5));// Hello
console.log(s.split(" "));// [ 'Hello', 'World!' ]
console.log(A.split(","));// [ 'dzk', 'like', 'kan', 'p' ]
```

**数组**

```javascript
const fruit = ["apple", "banana", "cherry"];
fruit.push("orange");
console.log(fruit);
console.log(Array.isArray(fruit));// 判断是不是数组
console.log(fruit[0]);
console.log(fruit.indexOf("banana"));// 查询位置
fruit.unshift("kiwi");//前插入
fruit.pop();//尾出
fruit.shift(); //头出 
console.log(fruit);
```

**对象**

```javascript
const Du_zk = {
    age : 20,
    Name : "duzhongkun",
    gender : "male",
    height : 1.76,
    weight : 6,
    bmi : function(){
        return this.weight / (this.height * this.height);
    },
    isFat : function(){
        return this.bmi() > 25;
    },
    hobbies : ["watching", "reading", "table tennis"],
    address : {
        province: "shandong",
        city: "linyi",
    },
};
for(let key in Du_zk){
    console.log(key, Du_zk[key]);
}
console.log(Du_zk.bmi());
console.log(Du_zk.isFat());
console.log(Du_zk.hobbies[1]);
console.log(Du_zk.address.city);
Du_zk.email = "duzhongkun@163.com";
console.log(Du_zk.email);
delete Du_zk.email;
```

**对象数组**

```javascript
const todos = [
    {
        id: 1,
        text: 'Take out trash',
        isCompleted: false,
    },
    {
        id: 2,
        text: 'Meeting with boss',
        isCompleted: true,
    },
    {
        id: 3,
        text: 'Dentist appointment',
        isCompleted: false,
    },
];

console.log(todos[1].text); // Meeting with boss
const todoJSON = JSON.stringify(todos);// 转化
console.log(todoJSON);
//[{"id":1,"text":"Take out trash","isCompleted":false},{"id":2,"text":"Meeting with boss","isCompleted":true},{"id":3,"text":"Dentist appointment","isCompleted":false}]
```

**JSON**

**JSON**：是一种轻量级的数据交换格式，使用文本表示结构化数据，通常是字符串格式。

**JSON**：常用于数据传输，如在前后端通信中，API返回的数据通常是JSON格式。

JSON格式通常更易于人类阅读，结构清晰。JSON可以被解析为对象数组。

JSON的数据类型包括字符串、数字、布尔值、数组和对象，不能包含函数或未定义的值。

**对象数组**：在编程语言中，尤其是JavaScript，表示一组对象的集合，通常是数组的形式。

**对象数组**：用于存储和操作数据，适合在代码中进行逻辑处理和迭代。

对象数组是编程语言中直接可用的结构，具有更强的可操作性。

对象数组可以包含方法和其他复杂的数据结构。

[Free Online JSON Formatter - FreeFormatter.com](https://freeformatter.com/json-formatter.html)  形式转换平台

**If**

```javascript
//x is 10
//y is not 10
//y is 10

const x = 10;
if(x === 10) {
    console.log("x is 10");
}

const y = "10";
if(y === 10) {
    console.log("y is 10");
}
else{
    console.log("y is not 10");
}

if(y == 10) {
    console.log("y is 10");
}
else{
    console.log("y is not 10");
}
```

**switch**

```javascript
const x = 10;
const color = x > 10 ? "blue" : "red";
switch (color) {
  case "blue":
    console.log("The color is blue");
    break;
  case "red":
    console.log("The color is red");
    break;
  default:
    console.log("The color is neither blue nor red");
};
```

**for while**

```javascript
const Du_zk = {
    age : 20,
    Name : "duzhongkun",
    gender : "male",
    height : 1.76,
    weight : 6,
    bmi : function(){
        return this.weight / (this.height * this.height);
    },
    isFat : function(){
        return this.bmi() > 25;
    },
    hobbies : ["watching", "reading", "table tennis"],
    address : {
        province: "shandong",
        city: "linyi",
    },
};
for(let key in Du_zk){
    console.log(key, Du_zk[key]);
}
let keys = Object.keys(Du_zk);
while(keys.length){
    let key = keys.pop();
    console.log(key, Du_zk[key]);
}
let keyss = Object.keys(Du_zk);
for(let i = 0; i < keyss.length; i++){
    console.log(keyss[i], Du_zk[keyss[i]]);
}

```

![image-20240928144318846](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20240928144318846.png)

![image-20240928144412744](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20240928144412744.png)

```javascript
let = unname = prompt("请输入你的名字");
        alert("你好" + unname);
```

```javascript
大家好，我叫${name}
```

![image-20240928165651060](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20240928165651060.png)



![image-20240928220807308](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20240928220807308.png)![image-20240929220227404](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20240929220227404.png)

![image-20240929224516380](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20240929224516380.png)

```javascript
arr.sort();  // 升序
        arr.sort(function(a, b) {
            return b - a;
        });//降序
```

![image-20241002204608397](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20241002204608397.png)

**匿名函数**

```javascript
let fn = function(){
            alert('hello world')
        }
fn()

let btn = document.querySelector('button');
        btn.onclick = function(){
            alert('hello world');
        }
选择按钮元素：document.querySelector('button') 这行代码通过CSS选择器选择页面中的第一个<button>元素，并将其赋值给变量btn。
添加点击事件监听器：btn.onclick = function(){...} 这行代码为按钮添加了一个点击事件监听器。当按钮被点击时，会执行后面的函数。
显示提示框：在点击事件监听器的函数中，alert('hello world') 这行代码会弹出一个提示框，显示文本“hello world”。
```

**立即执行函数**

```javascript
(function(x,y){
            //console.log(x+y);
            alert(x+y);
        })(1,2);
//无需调用 直接运行
```

**逻辑中断**

```javascript
function fn(x,y) {
            x = x || 0;
            y = y || 0; // 相当于默认值零   本质上是利用bool 导致语段中断
            return x+y;
        }
        fn();
```

![image-20241012225546195](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20241012225546195.png)

