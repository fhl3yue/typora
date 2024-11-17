### HTML

大体框架

```html
<!DOCTYPE html>
<html lang="en"> //语言 english
<head>
    <meta charset="UTF-8"> // 字符编码
    <meta http-equiv="X-UA-Compatible" content="IE=edge"> // 兼容IE
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> // 视口
    <title>Document</title> // 网页标题
</head>
<body>
    <a href="https://www.baidu.com" target = "_blank" > baidu </a> 
    
</body>
</html>
```

### 注释

```html
    <!--    
    == /* */
    -->
```

### 图片标签

```html
<img src="https://www.baidu.com/img/flexible/logo/pc/result.png" alt="百度logo"> 
    <!--    
    src alt 相互补充 不出现前者才会出现后者
	后面还可以带有 align = "" 的属性 来达成某种效果
    -->
```

### 超链接跳转

```html
<a href="https://www.baidu.com">百度一下</a>
```

### 音频标签

```html
    <audio controls>
        <source src="C:\Users\LWQ\Desktop\Admin\JAY\爱在西元前.flac" type="audio/mpeg">
    </audio>
```

### 视频标签

```html
    <video width="760" height="480" controls>
        <source src="C:\Users\LWQ\Desktop\Admin\JAY\✿Nightcore✿  Ama no Jaku 【Whispering】.mp4" type="video/mp4">
    </video>
```

### 框架标签

内置可展开的html

```html
    <iframe
        src="tpy.html" width="760" height="480" frameborder="0" scrolling="no">
    </iframe>
```

### 表格标签

```html
    <table border="1" width = "500" height = "600"  align = "center" >
        <tr>
            <td align = "center">1</td>  
            <td align = "center">2</td>
            <td align = "center">3</td>
        </tr>
        <tr>
            <td align = "center">4</td>
            <td align = "center">5</td>
            <td align = "center">6</td>
        </tr>
        <tr>
            <td align = "center">7</td>
            <td align = "center">8</td>
            <td align = "center">9</td>
        </tr>
    </table>
```

### 合并单元格

```html
    <table border="1" width = "500" height = "600"  align = "center" >
        <tr>
            <td align = "center" colspan = "3"> 123 </td>
            
        </tr>
        <tr>
            <td align = "center">4</td>
            <td align = "center">5</td>
            <td align = "center" rowspan="2">6<br>9</td>
        </tr>
        <tr>
            <td align = "center">7</td>
            <td align = "center">8</td>
            <!-- <td align = "center">9</td> -->
        </tr>
        
    </table>

colspan  列合并 rowspan 行合并
```

### 无序列表

```html
<!-- 
ul<li*10>a + tab
-->    
<ul>
        <li type = "circle">1</li>
        <li type = "square">2</li>
        <li type = "none">3</li>
    </ul>
```

### 有序列表

控制编号的两个属性

```html
    <ol type = "A" start = "3">
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ol>
```

### 自定义列表

```html
    <dl>
        <dt>1</dt>
        <dd>ABC</dd>
        <dd>DEF</dd>
        <dt>2</dt>
        <dd>usb</dd>
        <dt>3</dt>
        <dd>kkl</dd>
    </dl>
```

### 列表导航栏

```html
     <style>
        ul {
            list-style-type: none;
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #333;
        }

        li {
            float: left;
        }

        li a {
            display: block;
            color: white;
            text-align: center;
            padding: 14px 16px; 
            text-decoration: none;
        }

    </style>
    
 	<ul>
        <li><a href="https://mirror.codeforces.com/">主页</a></li>   
        <li><a href="https://mirror.codeforces.com/top">热门</a></li>
        <li><a href="https://mirror.codeforces.com/catalog">指南目录</a></li>
        <li><a href="https://mirror.codeforces.com/contests">比赛</a></li>
        <li><a href="https://mirror.codeforces.com/blog">博客</a></li>
        <li><a href="https://mirror.codeforces.com/contests/with-virtual-participation">虚拟比赛</a></li>
        
    </ul>
```

### 表单

```html
<form action = "https://mirror.codeforces.com" method = "post">
        <input type = "text" name = "username" placeholder = "用户名" />
        <br>
        <input type = "password" name = "password" placeholder = "密码" />
        <br>
        <input type = "submit" value = "登录" />
        <input type = "reset" value = "重置" />
    </form>




    <form action = "https://mirror.codeforces.com" method = "get">
        <table>
            <caption> 登录 Codeforces</caption> 
            <tr>
                <td>账户/邮箱</td>

                <td><input type = "text" name = "handle" /></td>
            </tr>
            <tr>
                <td>密码</td>
                
                <td><input type = "password" name = "password" /></td>
            </tr>
            <tr>
                <!-- 空格 -->
                
                <td><input type = "checkbox" name = "remember" /></td>
                <td>记住我一个月</td>
            </tr>
            
            <tr>
                <td><input type = "submit" value = "登录" /></td>
                <td><input type = "submit" value = "注册" /></td>
            </tr>

            <tr>
                <td><input type = "submit" value = "忘记密码" /></td>
            </tr>
        </table>        
    </form>
```

### 盒子

```html
    <div id="hover">KK AK ICPC</div>
```



### CSS

内嵌式

css 三种使用方法

```html
   <style>
        ul {
            list-style-type: none;
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: white; 
        }

        li {
            float: left;
        }

        li a {
            display: block;
            color: black;
            text-align: center;
            padding: 14px 16px; 
            text-decoration: none;
        }
        .name{
            font-size: 20px;
            color: black;
            text-align: center;
            padding: 14px 16px; 
            text-decoration: none;
        }
        #hover{
            background-color: #4CAF50;
            color: white;
        }
    </style>
    


    <ul>
        <li><a href="https://mirror.codeforces.com/" id = "hover">Codeforces</a></li>
    </ul>

    <div class = "name">KK AK ICPC</div>
    <br>
    <div id="hover">KK AK ICPC</div>
```

