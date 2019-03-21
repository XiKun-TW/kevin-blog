---
layout:     post
title:      "CSS Animation"
subtitle:   "Brief intruduce of CSS Animation"
date:    2018-11-10
author:     "惠坤"
image: "http://image.kevinxi.me/uploads/big/5e6599a76d4995355b29bfc9bf063ed1.jpg"
tags:
    - CSS
    - Tech
URL: "/2018/11/10/css-animation/"
categories: [ CSS ]
---

<h1>CSS Animation</h1>

<h2>Why Animation</h2>

目前网页内容越来越丰富，首先动画本事可以让网页看起来更加炫酷，其次合理的运用CSS动画可以大大的提升网页的用户体验。我们可以看看下面的一个关于网页动画的例子。

[运行该代码](https://codepen.io/Gougougogogo/pen/OzNLRm)

```markdown
<!--HTML-->
<div class="hamburger">
    <div class="hamburger-box">
        <div class="hamburger-inner"></div>
    </div>
</div>
<div class="drawer-box">
    <div class="drawer-box-text">
        <p>我没有动画</p>
    </div>
</div>

<div class="hamburger hamburger-with-animation">
    <div class="hamburger-box">
        <div class="hamburger-inner"></div>
    </div>
</div>
<div class="drawer-box drawer-with-animation">
    <div class="drawer-box-text">
        <p>我有动画</p>
    </div>
</div>
<div class="hamburger js-hamburger hamburger-with-infinite">
    <div class="hamburger-box">
        <div class="hamburger-inner"></div>
    </div>
</div>
<div class="drawer-box drawer-with-infinite">
    <div class="drawer-box-text">
        <p>我全是动画</p>
    </div>
</div>
```

```scss
//css

@keyframes drawer-box-animation {
    from {
        opacity: 0;
        transform: translateX(10px);
        width: 90%;
    }

    50% {
        opacity: 1;
        width: 100%;
        transform: translateX(0);
    }

    to {
        opacity: 0;
        width: 90%;
        transform: translateX(10px);
    }
}

.hamburger:hover + .drawer-box {
  color: #ff2c2d;
  width: 100%;

  &  .drawer-box-text {
    opacity: 1;
  }
}

.hamburger:hover + .drawer-box.drawer-with-infinite {
  animation-name: drawer-box-animation;
  animation-iteration-count: infinite;
  animation-duration: 1s;
}


.hamburger:hover .hamburger-inner {
  transform: translate3d(0, 0 ,0) rotate(45deg);
}

.hamburger:hover .hamburger-inner:before {
  transform: rotate(-45deg) translate3d(-5.71429px,-6px,0);
  opacity: 0;
}

.hamburger:hover .hamburger-inner:after {
  transform: translate3d(0,-10px,0) rotate(-90deg);
}

.hamburger:hover + .drawer-box {
  color: #ff2c2d;
  width: 100%;

  &  .drawer-box-text {
    opacity: 1;
  }
}

.hamburger:hover + .drawer-box.drawer-with-infinite {
  animation-name: drawer-box-animation;
  animation-iteration-count: infinite;
  animation-duration: 1s;
}

.drawer-box.drawer-with-animation {
  transition: width 0.25s ease-in-out;

  & .drawer-box-text {
    transition: opacity 0.25s ease-in;
    transition-delay: 0.15s;
  }
}
```

*看完后是不是发现，有动画的网页明显显得更加 高！大！上！*

<h2>How to animation?</h2>

目前网页使用CSS来实现动画有两种方式：

1. CSS Transition
2. CSS Animation

<h2> What is css transition? </h2>

简而言之，Transition 就是可以让你的元素在规定时间平滑属性值（从一个数值到另一个），何为平滑？其实平滑就是我们所说的动画，它可以让物体从一个状态缓慢的变化到另外一个状态。

那么如何写让一个网页元素具备平滑过度的功能呢？我们先来看看 CSS Transition 都有哪些属性:

```scss
.element {
    //属性值：让该属性应用平滑变化机制（all代表应用于所有属性)
    transition-property: width, opacity;
    //规定时间： 定义多长时间内完成变化 （单位可是 s、ms...)
    transition-duration: .5s;
    //如何平滑： 定义变换进度和时间之间的关系
    transition-timing-function: ease;
    //何时开始： 定义多久后开始平滑变化
    transition-dely: .5s;
}
```
我们再通过例子来看看如何运用 Transition：

[运行该段代码](https://codepen.io/Gougougogogo/pen/JMXPaY)

```html
<div class="popout-window with-animation"></div>
<div class="popout-window"></div>
```

``` scss
.popout-window {
    width: 10%;
    background-color: #525252;
}

.popout-window:hover {
    width: 100%;
}

.popout-window.with-animation {
    transition-property: width;
    transition-duration: 1s;
    transition-timing-function: ease-in;
}
```
我们可以注意到，其实transition的运用比较简单，只要在元素的css中加入 transition 这个属性值。从例子中我们可以看到 `transition-property` 是 `width`，也就是说，当该元素的宽度发生变化时就会应用平滑过渡的机制，平滑过渡所用的时间在 `transtion-duration` 中定义.

那么 `timing-function` 是什么呢？ timing-function 其实是定义：描述元素平滑过渡进度和所用时间关系的函数。举个简单的例子，我定义了我元素的宽度从 10% 到 100% 之间用2s来进行平滑过渡。那么我每隔100ms，我的元素宽度增长多少呢？ 时间和元素增长的关系可以是线性增长关系，也可以是曲线增长关系，而 timing-function 就是定义这种关系。常用的 timing-function 有以下几种：

1. linear
2. ease
3. ease-in
4. ease-out
5. ease-in-out
6. steps
7. cubic-bezier

我们可以看看下面的例子来了解下每个timing function 是什么样子的：

[运行该代码](https://codepen.io/Gougougogogo/pen/eyZYbB)

```html
<div class="runing-box liner">
    liner
</div>
<div class="runing-box ease">
    ease
</div>
...
<div class="runing-box ease-out">
    ease-out
</div>
<div class="runing-box ease-in-out">
    ease-in-out
</div>
<div class="runing-box ease-in-out">
    steps
</div>
```

```scss
.runing-box {
    position: absolute;
    left: 0;
    //...
    transition-property: left;
    transition-duration: 3s;
}
.running-box:hover {
    left: calc(100% - 200px);
}
.liner {
    transition-timing-function: linear;
}
...
.steps {
    transition-timing-function: steps(5, start);
}
```

不难发现，在整个动画运行过程中，`cubic-bezier` 是最奇怪的，我们可以通过该[网站](http://cubic-bezier.com/)来具体了解 `cubic-bezier`。

到此为止大家应该了解transition的用法，那么是不是transition可以实现所有的动画？

答案是不能，因为从transition的定义中我们不难发现，它是一个让元素从状态A平滑过渡到状态B，所以transition描述的动画总是会结束的，它无法让动画一直run起来。 接下来我们将到的CSS animation 则可以做到这点。

<h2>CSS Animation</h2>

CSS3 可以让大多数HTML元素呈现动画效果的技术。从定义我们可以看出，CSS Animation 是从 CSS3 开始的，它的作用是让页面元素呈现动画效果。

我们来看看Animation都有哪些属性：

```scss
//定义一个名为text-animation的动画桢
@keyframes text-animation {
	from {
		font-size: 16px;
	}
	20% {
		font-size: 20px;
	}
	to {
		font-size: 18px;
	}
}

.element {
	//定义动画名称
	animation-name: text-animation;
	//定义动画运行的时间
	animation-duration: 1s;
	//定义动画执行的次数
	animation-iteration-count: 1;
	//定义动画的运行状态
	animation-play-state: running;
	//定义元素在应用该动画初始和结束时的状态
	animation-fill-mode: none;
	//定义动画的运行方向
	animation-direction: normal;
	//定义动画运行进度和时间的关系
	animation-timing-function: linear;
	//定义动画延迟执行时间
	animation-delay: 1s;
}
```

我们来看一个应用动画的例子：

[运行该代码](https://codepen.io/Gougougogogo/pen/KZzwzg)

```html
<div class="text-animation">
    我是栗子
</div>
```

```scss
@keyframes text-animation {
	from {
		font-size: 16px;
	}
	20% {
		font-size: 20px;
	}
	to {
		font-size: 38px;
	}
}

.text-animation {
    animation-name: text-animation;
    animation-duration: .3s;
    animation-iteration-count: infinite;
}
```
CSS animation中的 `duration`,`delay`, `timing-function`和transition中的是一样的，所以在此不再做赘述，我们重点来看看其他的属性。

<h3>animation-iteration-count</h3>

iteration-count 定义了动画的执行次数，默认值为1

<table class="dataintable">
    <tbody><tr>
    <th style="width:40%;">值</th>
    <th>描述</th>
    </tr>
    <tr>
    <td>数值（比如：1，2，3，4）</td>
    <td>动画执行次数</td>
    </tr>
    <tr>
    <td>infinite</td>
    <td>一直执行该动画</td>
    </tr>
	</tbody>
</table>

<h3>animation-play-state</h3>

animation-play-state定义了动画的执行状态，paused为暂停执行动画，running为执行动画。

<table class="dataintable">
    <tbody><tr>
    <th style="width:40%;">值</th>
    <th>描述</th>
    </tr>
    <tr>
    <td> paused</td>
    <td> 暂停执行该动画 </td>
    </tr>
    <tr>
    <td> running </td>
    <td> 执行该动画 </td>
    </tr>
	</tbody>
</table>

我们来看下面的例子：

[执行该代码](https://codepen.io/Gougougogogo/pen/WdwbZG)

```html
<div class="text-animation">
    我是栗子
</div>
```

```scss
@keyframes text-animation {
	from {
		font-size: 16px;
	}
	20% {
		font-size: 20px;
	}
	to {
		font-size: 38px;
	}
}

.text-animation {
    animation-name: text-animation;
    animation-duration: .3s;
    animation-iteration-count: infinite;
}

.text-animation:hover {
	animation-play-state: paused;
}
```

<h3>animation-fill-mode</h3>

animation-fill-mode 定义元素在应用该动画初始和结束时的状态.
<table class="dataintable">
<tbody><tr>
<th style="width:15%;">值</th>
<th>描述</th>
</tr>
<tr>
<td>none</td>
<td>不改变默认行为。</td>
</tr>
<tr>
<td>forwards</td>
<td>当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）。</td>
</tr>
<tr>
<td>backwards</td>
<td>在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。</td>
</tr>
<tr>
<td>both</td>
<td>向前和向后填充模式都被应用。</td>
</tr>
</tbody></table>
    
我们假设场景如下：

```scss
@keyframes text-animation {
	from {
		color: blue;
	}
	
	to {
		color: red;
	}
}

.text-animation {
	color: white;
	animation-name: text-animation;
	animation-play-state: paused;
}

.text-animation:hover {
	animation-play-state: running;
}
```
根据设置不同的 fill mode，字体的颜色变化如下：

<table class="dataintable">
<tbody><tr>
<th style="width:15%;">Fill Mode</th>
<th>颜色变化</th>
</tr>
<tr>
<td>none</td>
<td>白、蓝、红、白</td>
</tr>
<tr>
<td>forwards</td>
<td>蓝、红、白</td>
</tr>
<tr>
<td>backwards</td>
<td>白、蓝、红</td>
</tr>
<tr>
<td>both</td>
<td>蓝、红</td>
</tr>
</tbody></table>

<h3>animation-direction</h3>

animation-direction 定义了动画的播放顺序（从起始桢到结束桢还是结束桢到起始桢）

<table class="dataintable">
        <tbody><tr>
            <th>值</th>
            <th>描述</th>
            </tr>
            <tr>
                <td>normal</td>
                <td>默认值。动画应该正常播放。</td>
            </tr>
            <tr>
                <td>reverse</td>
                <td>动画应该反向播放。</td>
            </tr>
            <tr>
                <td>alternate</td>
                <td>动画应该轮流反向播放。(奇数次正向播放，偶数次反向播放)</td>
            </tr>
            <tr>
                <td>alternate-reverse</td>
                <td>动画应该轮流反向播放。(奇数次反向播放，偶数次正向播放)</td>
            </tr>
        </tbody>
    </table>

我们来看看下面的例子：

[运行该代码](https://codepen.io/Gougougogogo/pen/xpVbeM)

```html
<div class="runing-box-animation">
    normal
</div>
<div class="runing-box-animation reverse">
    reverse
</div>
<div class="runing-box-animation alternate">
    alternate
</div>
<div class="runing-box-animation alternate-reverse">
    alternate-reverse
</div>
```

```scss
@keyframes running-box-animation {
    from {
        left: 0;
    }

    to {
        left: calc(100% - 200px);
    }
}
.runing-box-animation {
    animation-name: running-box-animation;
    animation-duration: 3s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
    animation-direction: normal;
}
.runing-box-animation.alternate {
        animation-direction: alternate;
}
.runing-box-animation.reverse {
    animation-direction: reverse;
}
```
目前基本上网页上所有复杂的动画都可以借助css的方式来实现，出于性能的考虑，如果可以使用css来做动画，尽量避免使用js的方式去做动画。
