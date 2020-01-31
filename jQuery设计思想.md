# jQuery设计思想
![jQuery](images/jQuery.png)
[jQuery](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html)是目前使用最广泛的javascript函数库。全世界排名前100万的网站，有46%使用jQuery，远远超过其他库。微软公司甚至把jQuery作为他们的官方库。因此学习jQuery对于网页开发者来说是很有必要的

废话不多说，下面是我关于jQuery设计思想的第一篇笔记。
***
本篇笔记参考之以下网址
* 阮一峰笔记[http://www.ruanyifeng.com/blog/](http://www.ruanyifeng.com/blog/)

* jQuery 中文文档[https://www.jquery123.com/](https://www.jquery123.com/)

### 【目录】
  1. jQuery 一些业界共识
  2. jQuery 如何获取元素
  3. jQuery 的链式操作是怎样的
  4. jQuery 如何创建元素
  5. jQuery 如何移动元素
  6. jQuery 如何修改元素的属性
  
   
## 【正文部分】
## 1. jQuery 一些业界共识
* 高级的程序员写的代码往往可以化繁为简，这一个精神体现在编程的方方面面，比如  
`window.$ = window.jQuery`
`$div.get(0) = $div[0]`
`$.fn = $.prototype`
* 程序员们还会在一个jQuery构造的api对象前面加个标示，以表示它名花有主了，要不然谁知道它是DOM还是谁构造的  
`const $div = $('div#test')`



## 2. jQuery 如何获取元素
jQuery设计思想亮点之一，就是使用同一个函数，来完成取值（getter）和赋值（setter），即"取值器"与"赋值器"合一。到底是取值还是赋值，由函数的参数决定。  
         $('h1').html();//html()没有参数，意为取值
         $('h1').html('hello');//html有参数hello,表示要对h1进行赋值了
常见的取值和赋值函数如下:  

  * 　[.html()](https://api.jquery.com/html/) 取出或设置html内容

 * 　[.text()](https://api.jquery.com/text/) 取出或设置text内容

 * 　[.attr()](http://api.jquery.com/attr/) 取出或设置某个属性的值

 * 　[.width()](https://api.jquery.com/width/) 取出或设置某个元素的宽度
  
 * 　[.height()](https://api.jquery.com/height/) 取出或设置某个元素的高度
  
 *   [.val()](https://api.jquery.com/val/) 取出某个表单元素的值  

需要注意的是，如果结果集包含多个元素，那么赋值的时候，将对其中所有的元素赋值；取值的时候，则是只取出第一个元素的值（.text()例外，它取出所有元素的text内容）。

## 3. jQuery 的链式操作是怎样的
jQuery设计思想亮点之一，就是最终选中网页元素以后，可以对它进行一系列操作，并且所有操作可以连接在一起，以链条的形式写出来，比如:
  ` $('div').find('h3').eq(2).html('Hello');`
拆分开来就是下面这样：
```
    $('div') //找到div元素

　　　.find('h3') //选择其中的h3元素

　　　.eq(2) //选择第3个h3元素

　　　.html('Hello'); //将它的内容改为Hello
```
这是jQuery最令人称道、最方便的特点。它的原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。

jQuery还提供了[.end()](https://api.jquery.com/end/)方法，使得结果集可以后退一步：
```
     $('div')

　　　.find('h3')

　　　.eq(2)

　　　.html('Hello')

　　　.end() //退回到选中所有的h3元素的那一步

　　　.eq(0) //选中第一个h3元素

　　　.html('World'); //将它的内容改为World
```
##  4. jQuery 如何创建元素
这个很简单需要添加什么就直接往$('     ')里加就好了，
比如
```
    $('<p>Hello</p>');

　　$('<li class="new">new list item</li>');

　　$('ul').append('<li>list item</li>');
```
## 5. jQuery 如何移动元素
jQuery设计思想亮点之一，就是提供两组方法，来操作元素在网页中的位置移动。一组方法是直接移动该元素，另一组方法是移动其他元素，使得目标元素达到我们想要的位置。

假定我们选中了一个div元素，需要把它移动到p元素后面。

第一种方法是使用.insertAfter()，把div元素移动p元素后面：  
   ` $('div').insertAfter($('p'));`
第二种方法是使用.after()，把p元素加到div元素前面：  
    `$('p').after($('div'));`
表面上看，这两种方法的效果是一样的，唯一的不同似乎只是操作视角的不同。但是实际上，它们有一个重大差别，那就是返回的元素不一样。第一种方法返回div元素，第二种方法返回p元素。
## 6. jQuery 如何修改元素的属性
1. attr()函数获取标签的某个属性
```
1. //获取id为p的标签的属性值
2. $('#p').attr('class')
```
2. attr()修改或修改标签的属性值
```
1. //如果存在就是修改，如果不存在就是添加
2.$('#p').attr('class','red')
```
3. 删除某个属性
```
$('#p').removeAttr('name')
```
4. 添加class名称
```
 $('#p').addClass('blue')
```
5. 删除class名称
```
$('#p').removeClass('yellow')
```
6. 有class就删除 没有就添加
```
$('#p').toggleClass('asdf')
```
(完)
***

