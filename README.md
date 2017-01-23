前端时间做了一个下载页，用到的技术比较多，小技巧也比较多，特此立文mark一下自己的收获，也算是一个小小的分享，废话不多，高能走起！
======
1.loading。
------
先上图！这个是目前自己和团队都比较满意的一个效果，也是现在[下载页](http://www.yy.com/download)正在使用的loading效果Ψ(￣∀￣)Ψ。
 ![image](http://ww3.sinaimg.cn/large/639d3769jw1fbzic0ku2vg20b408c785.gif)

嗯，如果你觉得还不够酷炫，没关系！(下面我会想办法让你觉得它足够酷炫，不要怀疑往下看，这很TX！很TX！TX！！)--ps:TX的意思是这样的，07年的时候，马总还和陈一丹说：“十年后的腾讯，将成为中国最受人尊敬的互联网公司”，然而现在你看看，这个公司十年来，看似一直没改变什么作风，但是同行都在帮他们实现愿望啊！这是多么令人感动的事情啊，**你不够好，我就让自己变糟**，让你永远是最好的。中国互联网界，简直就是兄友弟恭，手足深情的典范!( ﹁ ﹁ ) 。(*￣ω￣)鹅厂的各位大大别打我啊，祝你们鸡年大吉，每天一个敬业福！我也是引用别人的！引用啊！并不是有意黑！是故意黑！！故意黑！！故意！！！意！！！

######效果1:
![image](http://ww1.sinaimg.cn/large/639d3769jw1fbziq5yvn7g20b408c10g.gif)

######效果2:
![image](http://ww4.sinaimg.cn/large/639d3769jw1fbzis1g5q9g20b408cwlx.gif)

######深入:
你感受一下，看看上面的效果，港真！是不是感觉第一个好很多了，是不是有种想说干的漂酿的赶脚！嗯，其实还是可以的对吧，那好，下面我们来深入这个loading的代码内部，坐稳了，老司机带你加速！带你上高速！(你先别误会，我不会像某车主对待摩拜那样，塞进后备箱就带你回湖南了，我不是那样的老司机![image](http://ww2.sinaimg.cn/large/639d3769jw1fbzj0kydsmj201e01eq2p.jpg)
loading其实很简单，是svg做的，其实svg用到的属性和效果也比较枯燥最多就几个
```javascript
    stroke-dashoffset: 640;
    stroke-dasharray: 794; 

    stroke-dasharray:0,794;
```
**Tips**:其实这个属性我在写keyframes的时候是故意分开的，有些人觉得奇怪为什么stroke-dasharray要写2个，其实这个我只是为了兼容低版本的安卓机器，因为只写stroke-dasharray:0,794，很多安卓机器是无法识别的，iOS一直表现不错，但是对于2条属性iOS又无法识别，那么好，我只能写成这种类似hack的形式了。:dizzy_face:
不打算对svg的这两个属性做太多介绍，但是还是附上一些学习资源吧，毕竟都是自己一路过来菜的坑。
[svg相关教程](https://segmentfault.com/a/1190000007309718)
**如果你不会画svg的图**，也没关系拉，作为一个大前端，你肯定是会用PS的把！那这份教程拿好！[图片变svg相关教程](http://www.cnblogs.com/coco1s/p/6230165.html)
嗯，有童鞋说，拿了以上资源还是无法写出类似的效果啊，最后的颜色什么的是怎么填充上去的？喂喂喂，童鞋，你又直线思维了,现在我们该直角转弯了！来来来坐稳~准备第二波飙车，
![image](http://ww4.sinaimg.cn/large/639d3769jw1fc0asacyabj20ds07rq5a.jpg)

**事情总是这样的**，你不是学过透明度渐变等等知识吗，那你想一想，如果在svg动画快要结束的时候，把一张事先准备好的图片，偷偷的通过改变透明度的方式呈现出来，:sunglasses:同时，svg透明度逐渐变小，是不是！图片渐渐出现，svg慢慢消失！完美出现衔接效果！整段都显得棒棒哒！就像svg慢慢画完然后被填充上了颜色，有辣么一丢丢小小的成就感！有木有！干的漂酿！没毛病老铁！礼物订阅走一波！:sunglasses:

![image](http://ww1.sinaimg.cn/large/639d3769jw1fc0au5tejkj203m030mwx.jpg)

嗯，细心的童鞋又发现了问题，就算是这样，那你怎么保证他们能够很自然的衔接啊:triumph::triumph::triumph:难不成让我用js去判断AnimationEnd吗？像是这样：
```javascript
svgObj.addEventListener("webkitAnimationEnd", function() {
    imgObj.addClass('running');
});
imgObj.addEventListener("webkitAnimationEnd", function() {
    svgObj.addClass('running');
});
```
这样不妥吧？喂喂喂童鞋，你这个姿势,很僵硬啊，难道我们大css不能解决以上问题吗？:scream::scream:(别用很吃惊的眼神看着我，这就是可以，而且可以做的好很，很细致！细节很完美！强迫症患者的福音！简直就是css患者的救星！)，帅哥！到底怎么耍！![image](http://ww1.sinaimg.cn/large/639d3769jw1fc0b0hhrwhj201a01b0n7.jpg)(你看，长相一般的人，会一个css技巧不算什么，但是我就不同了，如果我会某个css技巧，他们就会说，卧槽长得这么帅还会这么多技巧，牛B!)
![image](http://ww1.sinaimg.cn/large/639d3769jw1fc0au5tejkj203m030mwx.jpg)

:unamused:既然你诚心诚意的问了，那么我就大发慈悲的告诉你，来来来，咱们也不卖关子，意识流先走一波：
应该大家都搞过flash的关键帧动画吧，那如果把两个有关联的动画想象成是2条同时开始的关键帧动画，只不过前面的时间我让动画1显示，到了后面动画1逐渐消失，与此同时动画2逐渐出现,覆盖，最后看起来的效果会怎样
![image](http://ww4.sinaimg.cn/large/639d3769jw1fbzksqlhxij201c01cmwx.jpg),你感受一下，来走起！
时间轴的概念我就不讲述了直接上一张比较有代表性的图：

![image](http://ww1.sinaimg.cn/large/639d3769jw1fbzl1e6q91j20xl03et99.jpg)

再来一个动画像是这样：

![image](http://ww4.sinaimg.cn/large/639d3769jw1fc0bkje92lg20b408cnb5.gif)
动画1逐渐消失，动画二逐渐出现，互相补充了对方消失时间内视觉的空白(

![image](http://ww4.sinaimg.cn/large/639d3769jw1fbzksqlhxij201c01cmwx.jpg)

,这个用fp做出来的动画效果并不是很完美，因为动画2一开始alpha=0%也是显示出来的，不造为什么，who care!)，是不是！赶脚到了一些什么！（有童鞋说，神马鬼！完全可以用一个动画实现你这个图的效果啊，唉哟不错哦~但是童鞋，这里是讲css实现效果上的一个小思路辣，我们要的是思路和姿势！并不是一个动画走天下哈）嗯，讲到这里，聪明的童鞋可能已经想关掉网页了，唉唉唉，别急啊，学知识都是由浅入深的，你以为到这里，我就讲完了？too naive!(图样图森破)，还是要先照顾一下不怎么懂的童鞋，来我们看代码例子!（是不是感觉又回到了大学课堂上，老师先对着睡意阑珊的你们讲一大堆你们认为不太重要的理论！然后才到你最关注的那一句！下面我们来一个栗子！
![image](http://ww3.sinaimg.cn/large/639d3769jw1fc0bqwwv01j201m017we9.jpg))

```javascript
//图片
.load__illustration {
  position:absolute;
  left:-1px;
  top:-1px;
  opacity:0;
  animation:opimg 1.25s linear 1 forwards;
}
//svg动画
.loadContent__text {
  animation:fillText 1.25s linear 1 forwards;
  
  stroke-dasharray: 794; 
  stroke-dashoffset: 794;
  opacity:1;
}

@keyframes opimg {
  0% {
    opacity:0;
  }
  80% {
    opacity:0;
  }
  83.625% {
    opacity:1;
  }
  100% {
    opacity:1;
  }
}
@-webkit-keyframes fillText {
  0%{
    -webkit-stroke-dasharray:0,794;
    stroke-dasharray:0,794;
    -webkit-stroke-dasharray: 794; 
    stroke-dasharray: 794; 
    -webkit-stroke-dashoffset: 794;
    stroke-dashoffset: 794;
    opacity:1;
  }
  80%{
    opacity:1;
  }
  83.375% {
    -webkit-stroke-dasharray:160,794;
    stroke-dasharray:180,794;
    -webkit-stroke-dasharray: 794; 
    stroke-dasharray: 794; 
    -webkit-stroke-dashoffset: 640;
    stroke-dashoffset: 640;
    opacity:0;
  }
  100%{
    -webkit-stroke-dasharray:0,794;
    stroke-dasharray:0,794;
    -webkit-stroke-dasharray: 794; 
    stroke-dasharray: 794; 
    -webkit-stroke-dashoffset: 794;
    stroke-dashoffset: 794;
    opacity:0;
  }
}
```
有木有一种，切，我还以为是什么高深姿势呢？原来就是2个keyframes互相交替出现而已，233333，童鞋，能够熟练灵活的运用你所学到的姿势，不也是一件很快乐的事情么？技术没有高低，选择最合适的，就是最好的吧，这里的效果，用以上两个姿势足够了，你觉得呢？

**TIPS2:** 这种动画其实需要算一些细节，例如图片出现的时机是80%-83.625%，而svg消失的时机也是80%-83.375%，这里是为了互相覆盖的时候不能够被人看出img和svg"互换"的间隙，需要无缝连接，可能你会问，帅哥，既然动画细节的控制这么谨慎，那这个3.***的小数和从80开始消失你都是怎么计算出来的？其实我也没有一个一成不变的公式，但是我可以给你一些建议，我会首先把2个动画的时间固定为同样长(因为这样比较好控制，当然你也 可以让动画1的时间短一些，2长一些，但是处理结尾的时候就会比较痛苦，因为100%和0%的衔接会比较难搞)，嗷对了，对于复杂的动画你还要记得打点还远哦，什么意思呢？就是保证动画在0%的时候已经是初始化的状态了，打个比方，
```javascript
......
@keyframes demo-1 {
  0% {
    opacity: 1;
    filter:alpha(opacity=100);
    @include attr2all(transform, matrix(1.2,0,0,1.2,0,0));
  }
  1.5625% {
    opacity: 1;
    filter:alpha(opacity=100);
  }
  23.4375% {
    opacity: 1;
    filter:alpha(opacity=100);
  }
  26.5625% {
    opacity: 0;
    filter:alpha(opacity=0);
    @include attr2all(transform, matrix(1,0,0,1,0,0));
  }
  100% {
    opacity: 0;
    filter:alpha(opacity=0);
    @include attr2all(transform, matrix(1.2,0,0,1.2,0,0));
  }
  98.4375% {
    opacity: 0;
    filter:alpha(opacity=0);
    @include attr2all(transform, matrix(1.21176,0,0,1.21176,0,0));
  }
  100% {
    opacity: 1;
    filter:alpha(opacity=100);
  }
}
@keyframes demo-2 {
  23.4375% {
    opacity: 1;
    filter:alpha(opacity=100);
    @include attr2all(transform, matrix(1.2,0,0,1.2,0,0));
  }
  26.5625% {
    opacity: 1;
    filter:alpha(opacity=100);
  }
  48.4375% {
    opacity: 1;
    filter:alpha(opacity=100);
  }
  51.5625% {
    opacity: 0;
    filter:alpha(opacity=0);
    @include attr2all(transform, matrix(1,0,0,1,0,0));
  }
  100% {
    opacity: 0;
    filter:alpha(opacity=0);
    @include attr2all(transform, matrix(1.2,0,0,1.2,0,0));
  }
}
......
```
这样的一组css动画其实很简单，就是2张图片的景深效果，当然，这里的代码只是其中一部分，因为剩下的部分会在另外一篇文章中补充完整，嘿嘿~~先卖个关子~，其实这里想要和大家讲的点就是demo2的51.5625%和100%这里，其实有童鞋会问为什么多一个51.5625%，**我的解释有2点：**
######1.为了控制动画出现的实际，不是从0到100而是精准在某个时间段上显示，这样可以更加精准的调整动画。
######2.类似于关键帧动画，其实demo1 demo2 ...demoN，都是一个完整动画的补间部分，补间当然是要严格控制在一个时间段内出现的辣~这样整个动画显示起来才更细致，效果才更好，对吧~
我也是按照设计大人需要的效果，一点点调试这个参数，最终实现效果的，过程可能比较痛苦，但是慢工出细活嘛，当你看到整个动画跑起来完美无瑕的时候，你就会感觉有一种小小的成就感，和众人猴塞雷的眼光！这可能就是我们前端肯花时间研究一些技术，深入一些细节的原因和动力吧，23333(当然，如果产品是个萌妹子，我可能会写的更好，桔子哥别打我~)，而这个时候，你就可以大大方方的让他们不要单行性能的问题，因为我基本没有js脚本，都是css！优秀！鸡贼！

![image](http://ww4.sinaimg.cn/large/639d3769jw1fc0cbbzz6nj204z050a9z.jpg)

好再上一个codepen的源码，反正没有什么好隐藏的，来来来，看看源码愉快玩耍！(注：后面在上线前做了一些调整，可能代码并非写的那么好，但是效果达到了，也请各位大神轻喷~)[CODEPEN上的loding源码](http://codepen.io/shinehs/pen/QdvOjQ)