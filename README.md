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
Tips:其实这个属性我在写keyframes的时候是故意分开的，有些人觉得奇怪为什么stroke-dasharray要写2个，其实这个我只是为了兼容低版本的安卓机器，因为只写stroke-dasharray:0,794，很多安卓机器是无法识别的，iOS一直表现不错，但是对于2条属性iOS又无法识别，那么好，我只能写成这种类似hack的形式了。:dizzy_face:
不打算对svg的这两个属性做太多介绍，但是还是附上一些学习资源吧，毕竟都是自己一路过来菜的坑。
[svg相关教程][https://segmentfault.com/a/1190000007309718]
如果你不会画svg的图，也没关系拉，作为一个大前段，你肯定是会用PS的把！那这份教程拿好！[图片变svg相关教程][http://www.cnblogs.com/coco1s/p/6230165.html]
嗯，有童鞋说，拿了以上资源还是无法写出类似的效果啊，最后的颜色什么的是怎么填充上去的？喂喂喂，童鞋，你又直线思维了:flushed:，现在我们该直角转弯了！事情总是这样的，你不是学过透明度渐变等等知识吗，那你想一想，如果在svg动画快要结束的时候，把一张事先准备好的图片，偷偷的通过改变透明度的方式呈现出来，:sunglasses:同时，svg透明度逐渐变小，是不是！图片向前，svg向后！完美的衔接！就像svg被填充上了颜色！有木有！干的漂酿！没毛病老铁！:sunglasses:
嗯，细心的童鞋又发现了问题，就算是这样，那你怎么保证他们能够很自然的衔接啊:triumph::triumph::triumph:难不成让我用js去判断AnimationEnd吗？这样不妥吧？喂喂喂童鞋，你这个有点僵硬啊，难道我们大css不能解决以上问题吗？:scream::scream:(别用很吃惊的眼神看着我，这就是可以，而且可以做的好很，很细致！很完美！强迫症患者的福音！)，帅哥！到底怎么耍！:unamused:既然你诚心诚意的问了，那么我就大发慈悲的告诉你，来来来，咱们也不卖关子，意识流先走一波：
应该大家都搞过flash的关键帧动画吧，那如果把两个有关联的动画想象成是2条同时开始的关键帧动画，只不过前面的时间我让动画1显示，到了后面动画一逐渐消失，与此同时动画二逐渐出现，最后看起来的效果会怎样![image][http://ww4.sinaimg.cn/large/639d3769jw1fbzksqlhxij201c01cmwx.jpg],你感受一下，来走起！
时间轴的概念我就不讲述了直接上一张比较有代表性的图：
![image][http://ww1.sinaimg.cn/large/639d3769jw1fbzl1e6q91j20xl03et99.jpg]
嗯，细心的童鞋又发现了问题，就算是这样，那你怎么保证他们能够很自然的衔接啊:triumph::triumph::triumph:难不成让我用js去判断AnimationEnd吗？这样不妥吧？喂喂喂童鞋，你这个有点僵硬啊，难道我们大css不能解决以上问题吗？:scream::scream:(别用很吃惊的眼神看着我，这就是可以，而且可以做的好很，很细致！很完美！强迫症患者的福音！)，帅哥！到底怎么耍！:unamused:既然你诚心诚意的问了，那么我就大发慈悲的告诉你，来来来，咱们也不卖关子，先上一组代码玩玩：
![image][http://codepen.io/shinehs/pen/QdvOjQ]
>>>>>>> 35cf3ae792e03fe81f41b193e7a1fd909fd5e3aa
