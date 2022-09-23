## 纯 CSS 飞行直升机动画制作指南

今天，我们来学习如何仅用HTML和CSS来构建一个漂亮的动画项目。这里假设大家都是中级CSS开发人员。

在这个项目中将用到的以下CSS3动画属性：

- CSS转换
- 3D变换
- CSS过渡效果
- 动画
- 自定义动画帧

兴奋吗？让我们开始吧！

## 使用HTML定义直升机结构

首先让我们在`main`元素中定义一个容器，命名为`helicopter`，接着在这个容器中按顺序写入4个`div`元素，每个`div`元素的`class`属性值如下：

- cockpit
- tail
- main
- rotor

在`rotor`类中，你需要添加一个具有`rotator`类的`div`，然后在这个`rotator`类内部再添加两个空`div`。

```
<html>
 <head>
 </head>
 <body>
  <main class="helicopter">
     <div class="cockpit"></div>
     <div class="tail"></div>
     <div class="main"></div>
     <div class="rotor">
       <div class="rotator">
         <div></div>
         <div></div>
       </div>
     </div>
     <main>
 </body>
</html>
```

## 直升机结构设计

现在让我们来设计HTML结构，使其变成直升机形状。

`body`

```
body {
  /* 将元素居中 */
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

``.cockpit``类

```
.cockpit {
    position: absolute;
    overflow: hidden;
    z-index: 1;
    width: 195px;
    height: 195px;
    border-radius: 100px 40px 50px 50px;
    background-color: #44d2fd;
}
```

![](https://i.postimg.cc/7ZNWJzbk/image.png)

现在为这个`cockpit`类添加玻璃。在`.cockpit`的`:before`和`:after`上定义玻璃形状：

```
.cockpit::before {
    content: "";
    position: absolute;
    z-index: 1;
    top: -10px;
    left: -25px;
    width: 170px;
    height: 170px;
    border-radius: 40px;
    background-color: #302e37;
}
.cockpit::after {
    content: "";
    position: absolute;
    z-index: 1;
    top: -60px;
    left: -60px;
    width: 170px;
    height: 170px;
    border-radius: 40px;
    background-color: rgba(255, 255, 255, 0.05);
}
```

输出：

![](https://i.postimg.cc/QdP0Tqsv/image.png)

`.tail`类

将样式应用于`.tail`类：

```
.tail {
    position: absolute;
    top: 50px;
    left: 150px;
    transform-origin: left center;
    border-top: 10px solid transparent;
    border-bottom: 80px solid transparent;
    border-left: 350px solid #2fadd2;
    border-bottom-right-radius: 10px;
    height: 10px;
}
```

输出：

![](https://i.postimg.cc/QNbmbDhQ/image.png)

`.main`类

这个类是直升机的旋转体：

```
.main {
    position: absolute;
    left: 130px;
    top: -10px;
    width: 40px;
    height: 20px;
    background: #302e37;
}
```

输出：

![](https://i.postimg.cc/htH1jP1B/image.png)

`.rotor`类

```
.rotor {
    width: 700px;
    height: 700px;
    border-radius: 350px;
    position: absolute;
    top: -360px;
    left: -200px;
    z-index: 2;
    overflow: hidden;
    background-color: #a299ab;
    opacity: 0.12;
    transform: scaleY(0.075);
}
```

输出：

![](https://i.postimg.cc/y6vhRTyn/image.png)

在设计完直升机螺旋桨的样式后，为了使该旋翼更逼真，现在定位到该`rotor`内的两个空`div`。这样当我们在下个部分应用`rotate`动画时，你将会看到漂亮的动画。

```
.rotator div {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -350px;
    margin-top: -30px;
    width: 700px;
    height: 80px;
    background-color: #fff;
}

.rotator div:nth-child(1){
    transform: rotate(0deg);
}

.rotor div:nth-child(2) {
    transform: rotate(90deg);
}
```

输出：

![](https://i.postimg.cc/q7syvc7s/image.png)

## 那么怎么让直升机飞起来呢？

到目前为止，我们已创建了直升机的形状和外观样式。但是没有动画制作和关键帧，那就不是动画。所以，使用CSS animation属性来赋予这个直升机飞行的力量。

## 定义@Keyframes

在使用`animation`属性之前，我们需要创建关键帧。对于这个项目，我们创建两个`@keyframes`：

- bounce
- rotate

`bounce`

```
@keyframes bounce {
    0%,100%{
        transform: translate(0px, -50px) rotate(-15deg);
    }
    50% {
        transform: translate(0px, 50px) rotate(-10deg);
    }
}
```

`rotate`

```
@keyframes rotate {
    0% {
        transform: rotate(0deg);
    }
    100%{
        transform: rotate(360deg);
    }
}
```

## 使用动画属性

现在，将这两个`@keyframes`添加到`.helicopter`和`.rotator`类中。

`.helicopter`类

```
.helicopter {
    /* adding bounce keyframes with duration 5s and infinite loop */
    animation: bounce 5s infinite; 
}
```

`.rotator`类

```
.rotator {
  position: absolute;
  width: 700px;
  height: 700px;
  border-radius: 350px;
  animation: rotate 0.6s linear infinite; */\* added rotate @keyframs \*/*
}
```

输出：

![](https://i.postimg.cc/jdDf7Y5d/image.gif)

## 结语

到这里，我们知道了如何仅使用CSS来创建复杂的形状和动画。你甚至都不必接触JavaScript。希望你喜欢这个项目。

感谢大家的阅读。编码快乐