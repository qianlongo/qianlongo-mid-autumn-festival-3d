


![3d.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/29ab4ac11fcc4c86beb58ec67458b74e~tplv-k3u1fbpfcp-watermark.image?)

## 背景

[点击查看太阳、地球、月亮3D旋转](https://qianlongo.github.io/qianlongo-mid-autumn-festival-3d/src/sun-earth-moon-rotate.html)

[点击查看太阳、地球、月亮3D旋转2](https://qianlongo.github.io/qianlongo-mid-autumn-festival-3d/src/sun-earth-moon-rotate-no-bg.html)



[点击查看太阳、地球、月亮3D旋转源码](https://github.com/qianlongo/qianlongo-mid-autumn-festival-3d)



中秋佳节即将到来，远在他乡的孩子们马上可以回家和父母一起吃月饼，看月亮，聊聊工作、谈谈理想，想想还挺惬意。

抬头望向天空时，你是否想知道太阳、地球、月亮的绕行轨迹如何通过css3来实现？来吧，这篇文章会从零和你一起学习如果画一个`3D小球`，`如何绘制漫天的繁星`、`如何实现行星轨迹3D图`

## 关键元素

1. 一个旋转的3D球
2. 漫天繁星，会眨眼睛那种哦
3. 旋转的行星轨道

## 如何画一个3D球


![3dball.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0f8df3ccb752447ebccb587e1690b97c~tplv-k3u1fbpfcp-watermark.image?)

您也可以直接[点击这里](https://qianlongo.github.io/qianlongo-mid-autumn-festival-3d/src/ball-rotate.html)查看，效果更好



### 先欣赏几张图

> 在画球之前我们先欣赏几张图

**《冰河世纪》的小松鼠**
隔着屏幕我仿佛都碰着到这灵敏的鼻子

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3fe59703def44d39991f5b4b5b1d8b1f~tplv-k3u1fbpfcp-watermark.image?)

**透过显示器的枪？**


![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7b2ec2c0224d47de8ce18704b146b89b~tplv-k3u1fbpfcp-watermark.image?)

**摸摸狗头**

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4dd70fb3fd074231b2fd78bfc14275cc~tplv-k3u1fbpfcp-watermark.image?)

### 再画个人人都会的圆

> 看完上面的图，聪明的你一定猜到了，咱们只要在2d平面上加几天竖线，3D的感觉就出来了

**html**

``` html

<div class="ball-container">
  <div class="ball-bg"></div>
  <div class="ball"></div>
</div>

```

**css**

``` css
.ball-container{
  width: 200px;
  height: 200px;
  border-radius: 50%;
  perspective: 500px;
  position: relative;
}

.ball {
  transform-style: preserve-3d;
  position: absolute;
  width: 100%;
  height: 100%;
}

.ball-bg{
  width: 100%;
  height: 100%;
  position: absolute;
  border-radius: 50%;
  background-image: linear-gradient(
    45deg,
    #ff9a9e 0%,
    #fad0c4 99%,
    #fad0c4 100%
  );
}

```
通过上面的代码，我们得到的是一个粉粉的圆，接下来试试加上几条线，能不能有3D的感觉

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2d685cc30a22458d9720974d8de4e2e2~tplv-k3u1fbpfcp-watermark.image?)

### 添上4条竖线

``` css
.ball-line {
  width: 100%;
  height: 100%;
  background-color: transparent;
  border: solid 0.5px #fad0c4;
  border-radius: 50%;
  margin: -0.5px;
  position: absolute;
  box-sizing: border-box;
}

.ball-line:nth-of-type(1) {
  transform: rotateY(45deg);
}
.ball-line:nth-of-type(2) {
  transform: rotateY(90deg);
}
.ball-line:nth-of-type(3) {
  transform: rotateY(135deg);
}
.ball-line:nth-of-type(4) {
  transform: rotateY(180deg);
}


```
为了让线不那么粗影响整体球的感觉，我们加了0.5px，看起来有一点点3d的感觉了，最后让球旋转起来试试

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c693a54efabd44f2a3a637f75d71d91a~tplv-k3u1fbpfcp-watermark.image?)

### 让球旋转起来


``` css

@keyframes rotate {
  0%{
    transform: rotateY(0) rotateX(0);
  }

  100%{
    transform: rotateY(360deg) rotateX(360deg);
  }
}

.ball {
  /* 添加动画 */
  animation: rotate 10s infinite linear; 
}

```

**旋转的3D球就画好啦**

![3dball.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0f8df3ccb752447ebccb587e1690b97c~tplv-k3u1fbpfcp-watermark.image?)


## 再画一副漫天繁星的天空

> 闭上眼睛回想一下你记忆中夜晚的天空，闪烁的星星是那么的平静,安详，像是一只只明亮的眼睛,又像一盏盏亮晶晶的银灯。

**dom结构**

``` html
<div class="container">
  <div class="stars"></div>
</div>

```
**关键css**

``` css

 @keyframes shine {
  0% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}

```

**关键js**

> 考虑星星的数量众多，且宽高不同最好，这里我们通过js来动态生成星星

``` javascript
  const $ = document.querySelector.bind(document);
  const $body = $("body");
  const canvasWidth = $body.offsetWidth;
  const canvasHeight = $body.offsetHeight;
  // 创建一个带自定义样式的dom
  const createElement = (styles, tag = "div") => {
    const ele = document.createElement(tag);

    Object.keys(styles).forEach((attr) => {
      ele.style[attr] = styles[attr];
    });

    return ele;
  };

  const drawStars = () => {
    // 创建文档碎片，缓存dom片段，减少dom操作
    const $starFragment = document.createDocumentFragment();
    const $stars = $(".stars");
    /*
    // 创建任意数量的星星
      1. 位置不同
      2. 大小不同
      3. 动画延时不同
    */
    const createStar = (size, num) => {
      while (num--) {
        const left = Math.random() * (canvasWidth - size) + "px";
        const top = Math.random() * (canvasHeight - size) + "px";        const width = size + "px";
        const delay = Math.random() * 5;
        const styles = {
          width,
          height: width,
          left,
          top,
          borderRadius: "50%",
          position: "absolute",
          background: "#ffffff",
          animation: `shine 2s linear ${delay}s infinite`,
        };
        const $star = createElement(styles);

        $starFragment.appendChild($star);
      }
    };
    // 创建不同大小的星星
    createStar(1, 500);
    createStar(2, 40); 
    createStar(3, 30);
    createStar(4, 20);

    $stars.appendChild($starFragment)};

    drawStars();
```

![star.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2ae589e0b3b24e148555475a60d58e2f~tplv-k3u1fbpfcp-watermark.image?)

## 太阳、地球、月亮运动全景

> 有了前面的星空背景以及3D小球基础，接下来我们可以开始画真正的运行轨迹图啦！！！

### 把自己转动的太阳先画出来

> 太阳无疑是最亮的崽，咱们先把他给整出来


![sun.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0bbd47658b744735b643b2ba0d17f4fa~tplv-k3u1fbpfcp-watermark.image?)

``` html

<div class="sun">
  <div class="ball-container">
    <div class="ball">
      <div class="ball-line"></div>
      <div class="ball-line"></div>
      <div class="ball-line"></div>
      <div class="ball-line"></div>
    </div>
    <div class="ball-light"></div>
  </div>
</div>

```

``` javascript
.ball-container {
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  left: 50%;
  margin-left: -35px;
  top: -35px;
  animation: rotateContainer 20s linear infinite;
}

.ball {
  transform-style: preserve-3d;
  border-radius: 50%;
  width: 100%;
  height: 100%;
  animation: rotateSelf 10s infinite linear;
  position: absolute;
}

.ball-light {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  position: absolute;
}

.ball-line {
  width: 100%;
  height: 100%;
  background-color: transparent;
  border: solid 0.5px #fcd670;
  border-radius: 50%;
  margin: -1px;
  position: absolute;
}

.ball-line:nth-of-type(1) {
  transform: rotateY(45deg);
}

.ball-line:nth-of-type(2) {
  transform: rotateY(90deg);
}

.ball-line:nth-of-type(3) {
  transform: rotateY(135deg);
}

.ball-line:nth-of-type(4) {
  transform: rotateY(180deg);
}

.sun {
  transform-style: preserve-3d;
  position: absolute;
}

.sun .ball-container {
  width: 100px;
  height: 100px;
  animation: none;
}

.sun .ball-light {
  background-image: linear-gradient(
    to right,
    #ff8177 0%,
    #ff867a 0%,
    #ff8c7f 21%,
    #f99185 52%,
    #cf556c 78%,
    #b12a5b 100%
  );
  box-shadow: 0 0 100px #ff8177;
}

.sun .ball-line {
  border-color: #ff8177;
}

/* 球自身的旋转 */
@keyframes rotateSelf {
  0% {
    transform: rotateY(0) rotateX(0);
  }

  100% {
    transform: rotateY(360deg) rotateX(360deg);
  }
}

```

### 地球绕着太阳转

> 地球绕着太阳转主要需要考虑两个关键点： 1。 椭圆形轨道 2. 地球绕着椭圆形轨道旋转

#### 地球绕行轨道


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0d7f33d13b904751921e1aa8ea47281a~tplv-k3u1fbpfcp-watermark.image?)

如何才能画出这样的轨道图？ 其实可以看成是一个正面的圆沿着X轴旋转了一定的角度，让其看起来比较有空间感

**第一步：先画出正面的圆**

``` html
<div class="earch"></div>
```

``` css

.earch {
  transform-style: preserve-3d;
  position: relative;
  width: 50vw;
  height: 50vw;
  border: solid 0.5px #ffffff;
  border-radius: 50%;
  box-shadow: 0 0 22px #fff;
}


```


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3b4748f05ff9435b9eb60e04a6db0a5c~tplv-k3u1fbpfcp-watermark.image?)


**第二步：绕着X轴旋转**

``` css

.earch {
  transform-style: preserve-3d;
  position: relative;
  width: 60vw;
  height: 60vw;
  border: solid 0.5px #ffffff;
  border-radius: 50%;
  transform: rotateX(75deg);
  box-shadow: 0 0 22px #fff;
}


```


![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/96b6e372bac544e9b9e56867c306d072~tplv-k3u1fbpfcp-watermark.image?)

#### 把旋转地球画出来

> 地球的画法和太阳没有太大的区别，这里我们主要想一下如何才能画出一个绕着刚才画出的轨迹运动的地球


![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bfc83b96d04644f18914b8daabec67fc~tplv-k3u1fbpfcp-watermark.image?)


公园里的这个器材大家应该都玩过哈，人站上去时，转动底部的罗盘，罗盘在转，人也就跟着转了。应用到这里，可以把轨迹比作是踩脚的罗盘，而人则是地球。

让轨迹运动，球则相对于轨迹静止，轨迹运动了，球自然也就看起来在动了。

``` html
<!-- 外部的罗盘 -->
<div class="earch">
  <!-- 地球 -->
  <div class="ball-container">
    <div class="ball">
      <div class="ball-line"></div>
      <div class="ball-line"></div>
      <div class="ball-line"></div>
      <div class="ball-line"></div>
    </div>
    <div class="ball-light"></div>
  </div>
</div>

```

```css

/* 轨道旋转 */
/* 因为需要保持倾斜的角度，所以初始和终态都是rotateX(75deg) */
@keyframes rotateTrack {
  0% {
    transform: rotateX(75deg) rotateZ(0);
  }
  100% {
    transform: rotateX(75deg) rotateZ(360deg);
  }
}

 /* 消除轨道旋转对子元素的影响 */
@keyframes rotateContainer {
  0% {
    transform: rotateZ(0) rotateX(-75deg);
  }
  100% {
    transform: rotateZ(-360deg) rotateX(-75deg);
  }
}

.earch {
  transform-style: preserve-3d;
  position: relative;
  width: 60vw;
  height: 60vw;
  border: solid 0.5px #ffffff;
  border-radius: 50%;
  transform: rotateX(75deg);
  animation: rotateTrack 20s linear infinite;
  box-shadow: 0 0 22px #fff;
}

.earch .ball-light {
  background-image: linear-gradient(to top, #37ecba 0%, #72afd3 100%);
  box-shadow: 0 0 1000px #72afd3;
}

.earch .ball-line {
  border-color: #72afd3;
}


```
于是旋转的地球也画好啦！最后只剩下离绕着地球旋转的月亮了


![earth.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/79b90b1a513f4a01b6a06941237ec046~tplv-k3u1fbpfcp-watermark.image?)

### 月亮绕着太阳转

> 整体思路和地球绕着月亮转是差不多的，但是需要注意的是

1. 月亮绕行地球的速度大于地球绕行太阳的速度，

2. 注意消除地球轨迹旋转对月亮整体的影响


``` html
<div class="earch">
  <div class="ball-container">
    <div class="ball">
      <div class="ball-line"></div>
      <div class="ball-line"></div>
      <div class="ball-line"></div>
      <div class="ball-line"></div>
    </div>
    <div class="ball-light"></div>
  </div>
  <!-- 月亮部分 -->
  <div class="moon-container">
    <div class="moon">
      <div class="ball-container">
        <div class="ball">
          <div class="ball-line"></div>
          <div class="ball-line"></div>
          <div class="ball-line"></div>
          <div class="ball-line"></div>
        </div>
        <div class="ball-light"></div>
      </div>
    </div>
  </div>
</div>

```

``` css
/* 这一层是消除父元素earth，旋转动画带来的影响 */
.moon-container {
  width: 400px;
  height: 400px;
  position: absolute;
  left: 50%;
  margin-left: -200px;
  top: -200px;
  border-radius: 50%;
  animation: moonTrack 20s linear infinite;
}
/*画出轨迹，并旋转*/
.moon {
  width: 100%;
  height: 100%;
  border: solid 0.5px #ffffff;
  box-shadow: 0 0 22px #fff;
  border-radius: 50%;
  position: absolute;
  left: 0;
  top: 0;

  animation: rotateTrack 4s linear infinite;
  transform-style: preserve-3d;
}
/*消除轨迹运动影响并且设置更快的旋转速度*/
.moon .ball-container {
  width: 50px;
  height: 50px;
  top: -25px;
  margin-left: -25px;
  animation: rotateContainer 4s linear infinite;
}
/*自转动画调快一些*/
.moon .ball {
  width: 50px;
  height: 50px;
  animation: rotateSelf 5s infinite linear;
}

.moon .ball-light {
  background-image: linear-gradient(
    -20deg,
    #ddd6f3 0%,
    #faaca8 100%,
    #faaca8 100%
  );
  box-shadow: 0 0 1000px #ddd6f3;
}

.moon .ball-line {
  border-color: #ddd6f3;
}

```
![3d.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/29ab4ac11fcc4c86beb58ec67458b74e~tplv-k3u1fbpfcp-watermark.image?)

## 结语

> 月深了，鸟儿都早早睡了，祝大家中秋节开森快乐，晚安，接下来打算再写一篇`玉兔奔月的3D实现文章`，希望大家喜欢。



## 参考



 1. [ 【中秋】纯CSS实现日地月的公转](https://juejin.cn/post/7006507905050492935#heading-0)

2. [渐变颜色](http://color.oulu.me/deta2.html)

3. [带你玩转css3的3D！](https://juejin.cn/post/6844903439965618189)









