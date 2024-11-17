根据$CSS$选择器来获取$DOM$元素

1.选择匹配的第一个元素

```javascript
document.querySelector('css选择器');
<ul>
    <li>1</li>
</ul>
document.querySelector('ul li:first-child');
```

能够对抓取的元素进行修改

$document.querySelectorAll('css选择器')$  得到一个伪数组 但是没有一些$push$功能  需要遍历

### 设置/修改$DOM$元素

$.innerText$  修改文字内容 得到纯文本 不解析标签

$.innerHTML$ 修改内容并解析标签

```html
<body>
  <div class="wrapper">
    <strong>传智教育年会抽奖</strong>
    <h1>一等奖：<span id="one">???</span></h1>
    <h3>二等奖：<span id="two">???</span></h3>
    <h5>三等奖：<span id="three">???</span></h5>
  </div>
  <script>
    const person = ['周杰伦','林俊杰','陶喆','蔡依林','张学友'];
    const random = Math.floor(Math.random()*person.length);
    const one = document.querySelector('#one');
    one.innerHTML = person[random];
    person.splice(random,1);
    const random1 = Math.floor(Math.random()*person.length);
    const two = document.querySelector('#two');
    two.innerHTML = person[random1];
    person.splice(random1,1);
    const random2 = Math.floor(Math.random()*person.length);
    const three = document.querySelector('#three');
    three.innerHTML = person[random2];
  </script>
</body>
```

**操作元素常用属性**

修改标签元素属性，比如通过$src$ 更换图片

```javascript
const pic = document.querySelector('img');
pic.src = './b02.jpg';
pic.title = '演唱会';
```

生成$N,M$随机数函数 

```javascript
function getRandom(N,M){
            return Math.floor(Math.random()*(M-N+1)+N);
        }
```

**操作元素样式属性**

通过$style$ $className$ $classList$  操作$css$

```javascript
    <style>
        .box{
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>
<body>
    <div class = "box"></div>
    <script>
        const box = document.querySelector('.box');
        box.style.backgroundColor = 'red';
        box.style.width = '300px';
        box.style.height = '300px';
    </script>
</body>


    <style>
        body {
            background: url(./desktop_1.jpg) no-repeat top center/cover;
        }
    </style>
</head>
<body>
    <script>
        function getRandom(N,M){
            return Math.floor(Math.random()*(M-N+1)+N);
        }
        let random = getRandom(1,10);
        // 标签选择body，因为body是唯一的标签，可以直接写document.body.style.background
        document.body.style.background = `url(./desktop_${random}.jpg) no-repeat top center/cover`;
    </script>
</body>
```

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 200px;
            background-color: red;
        }
        .box{
            width: 400px;
            height: 400px;
            background-color: blue;
            position: relative;
        }
        
    </style>
</head>
<body>
    <div></div>
    <script>
        const div = document.querySelector('div');
        div.className = 'box';
        //已经是class就不用加点 .box了
    </script>
</body>
</html>
```

为了解决$className$ 容易覆盖以前的类名，我们可以通过$classList$方式追加和删除类名

![image-20241015143851573](C:/Users/LWQ/AppData/Roaming/Typora/typora-user-images/image-20241015143851573.png)

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box{
            width: 200px;
            height: 200px;
            color: black;
        }
        .active {
            color: red;
            background-color: pink;
        }
    </style>
</head>
<body>
    <div class = "box"> 问字 </div>
    <script>
        const box = document.querySelector('.box');
        // 追加类
        //box.classList.add('active'); 
        //删除类
        //box.classList.remove('active');
        //切换类  无则添加 有则删除
        box.classList.toggle('active');
    </script>
</body>
</html>
```

**操作表单元素 属性**

