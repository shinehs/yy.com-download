前端时间做了一个下载页，用到的技术比较多，小技巧也比较多，特此立文mark一下自己的收获，也算是一个小小的分享，废话不多，高能走起！
======
1.loading。
------
先上图！这个是目前自己和团队都比较满意的一个效果，也是现在[下载页](http://www.yy.com/download)正在使用的loading效果Ψ(￣∀￣)Ψ。
 ![image](http://ww3.sinaimg.cn/large/639d3769jw1fbzic0ku2vg20b408c785.gif)

嗯，如果你觉得还不够酷炫，没关系！(下面我会想办法让你觉得它足够酷炫，不要怀疑往下看，这很TX！很TX！TX！！)--ps:TX的意思是这样的，07年的时候，马总还和陈一丹说：“十年后的腾讯，将成为中国最受人尊敬的互联网公司”，然而现在你看看，这个公司十年来，看似一直没改变什么作风，但是同行都在帮他们实现愿望啊！这是多么令人感动的事情啊，**你不够好，我就让自己变糟**，让你永远是最好的。中国互联网界，简直就是兄友弟恭，手足深情的典范![image](http://ww3.sinaimg.cn/large/639d3769jw1fbziz84l1rj202f02g3yc.jpg)。(*￣ω￣)鹅厂的各位大大别打我啊！我也是引用的！引用啊！并不是有意黑！是故意黑！！故意黑！！故意！！！意！！！！
效果1:
![image](http://ww1.sinaimg.cn/large/639d3769jw1fbziq5yvn7g20b408c10g.gif)
效果2:
![image](http://ww4.sinaimg.cn/large/639d3769jw1fbzis1g5q9g20b408cwlx.gif)
你感受一下，看看上面的效果，是不是感觉第一个好很多了。嗯，其实还是可以的对吧，那好，下面我们来深入这个loading的代码内部，坐稳了，老司机带你加速！带你上高速！(你先别误会，我不会像某车主对待摩拜那样，塞进后备箱就带你回湖南了，我不是那样的老司机![image](http://ww2.sinaimg.cn/large/639d3769jw1fbzj0kydsmj201e01eq2p.jpg)
loading其实很简单，是svg做的，其实svg用到的属性和效果也比较枯燥