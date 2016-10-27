                    整理了CSS3中基本全部的属性

CSS3
浏览器前缀
Trident内核：IE浏览器          -ms-    
Gecko内核：Firefox             -moz-    
Presto内核：Opera              -o-     
Webkit内核：Chrome和 Safari   -webkit-  

CSS3选择器
1.属性选择器
标签[attr]               标签中只要含有attr属性即可
标签[attr=value]         标签中的attr属性值为value，其中value既是开头，又是结尾
标签[attr^=value]        标签中的attr属性值以value开头
标签[attr$=value]        标签中的attr属性值以value结尾
标签[attr*=value]        标签中的attr属性值只要含有value即可

2.结构伪类选择器
()里面写数字，代表下标，下标从1开始，而不是0；还可以写一个n，n从一直++，比如隔行换色
nth-child()表示子元素，那么 标签:nth-child() 就表示为nth-child()子元素的父元素是这个：前面的标签，如果符合才应用样式
标签:nth-of-type() / 标签:nth-child()    
标签:first-of-type() / 标签:first-child()   
标签:last-of-type() / 标签:last-child()    
标签:only-of-type() / 标签:only-child()  唯一的，只有一个时才有作用 

:root   root根节点表示html  
        在css样式中:root{}相当于html{}，但是前者优先级更高，html指的是html的根节点，而:root不一定是html的根节点，也可能是其他文档结构的根节点，所以:root的范围更广一点
        
:not 表示相反的操作  即选择一个集合，把其中不符合条件的选择出来应用样式
:empty  把内容为空的选择出来，即为空标签，标签中不写任何内容如<div></div>
:target 表示目标  配合锚点链接使用，点击页面跳转到相应位置，用:target 标签应用到跳转相应位置后，该位置的样式

3.状态伪类选择器
:focus点击文本框显示样式input:focus{border:1px solid red;}，在firefox中点击文本框有一个默认的边框样式，需要初始化去掉边框input{outline:none}
:checked一般用于单选框和复选框中，不是单单应用于它本身，而是应用在input中包含的标签
::selection选中元素的操作，被选中的文字应用样式，在firefox没有标准化，需要变成::-moz-selection，加上了前缀才行
:first-letter  对第一个字符的操作
:first-line   对第一行的操作
:enabled 对可用状态的选择
:disabled 对禁止状态的选择  禁用 在firefox不能进行选择
:read-write 可读写 在firefox没有标准化，需要加上前缀
:read-only  只读 在firefox没有标准化，需要加上前缀  在firefox可以进行选择，进行复制粘贴这样一个文字的操作，这是与禁用的一个区别

:before 在元素的前面
:after 在元素的后面
两者结合content使用 ，下面举例 当鼠标移入文字两边出现 []
Css样式：div{ float:left; margin:20px; position:relative;}
div:hover:before{ content:”[“;  position:absolute; left:-5px; top:0;]
div:hover:after{ content:” ]”; position:absolute; right:-5px; top:0;}
Html样式：<div>html</div> <div>css</div>
:表示伪类  样式对于元素本身进行操作
::表示伪元素 感觉把样式加上了一个虚拟的元素身上，例如before和after

4.其他选择器
~是css3新增的 紧跟着的后面的所有的兄弟节点
+是css2.1本身有的，如div + span，紧跟着的后面的第一个兄弟节点是那个+后面的标签span，符合才应用样式 
>是css2.1本身有的， 选择子元素，即亲儿子元素，不包括孙子元素，常见应用于列表


CSS3文本属性
1.text-shadow  文字的阴影 参数：x(x轴偏移量)  (y轴偏移量)  blur(模糊值)  color 多阴影(通过一个，隔开，设置这样一个多阴影)
举例即text-shadow:10px 10px 10px red,-10px -10px 10px yellow; 
火焰字就是通过多组文字阴影进行设置而成的{ text-shadow:0 0 4px white,0 -5px 4px #ff3,2px -10px 6px #fd3,px -15px 11px #f80,2px -25px 17px #f20; }

2.text-stroke    文字的描边 参数： w(描边的宽度)  color(描边颜色)  目前只有webkit支持，所以要写成-webkit-text-stroke 因此没有列入w3c标准 描边再加上颜色设置为透明的属性color:transparent 就可以变成一个镂空字

3.text-overflow  文字的移除隐藏操作
单行省略：width:150px;  white-space:nowrap;(一行显示) overflow:hidden;(多余文字隐藏) text-overflow:ellipsis;(省略号) 这几句话即可实现
多行省略只有webkit支持，width:150px;  overflow:hidden; -webkit-line-clamp:2;(第几行出现省略号)  -webkit-box-orient:vertical; display:-webkit-box; 这几句话即可实现

4.direction   文字的排列方向  参数： rtl(从右向左)    ltr(从左向右)   两个都要配合unicode-bidi:bidi-override(文字的排版方式从右向左)使用

5.@font-face     嵌入字体  参数：font-family  src   
好处：图片大小改变比较麻烦，嵌入字体可以直接改变大小与颜色，操作方便；图标要发送http请求，嵌入字体引入一次之后，把它看作了一个文字，不需要再发送请求，性能提高了
图标库font awesome ： 下载后把里面的font 和 css文件复制走  然后引入复制文件中的css下的font-awesome.css，（可以查看font-awesome.css文件下的@font-face   font-family后的名字可以自定义），找到图标的class名直接复制，然后在css样式下自定义
Icomoon 是一个专门制作图标的网站  把本地的svg import icons添加到网站上，点击一个刚加入的，然后点击制件generate Font 跳转到一个页面 点击download 下载


CSS3背景属性
1.background-size 背景图的尺寸  参数：length(可以写width 或height或者两个都有) percent(百分比 写一个参数表示宽度，第二个就默认为高度自适应)  cover(覆盖整个区域，可能有部分背景图被隐藏)  contain(包含在整个容器当中，使背景图完整地显示在容器中，容器中可能会有部分空白)  背景图做得大一点，通过缩放来适应不同的尺寸

2.background-origin 背景图的位置 参数：padding-box(默认是在padding的左上角) border-box(在border的左上角)  content-box(在内容的左上角)

3.bakcground-clip 背景的裁接 参数：padding-box(padding以外都被裁接掉了不显示)  border-box(默认什么都没被裁接掉)  content-box(padding和border都被裁接掉)

4.多背景设置 通过，分割(先写的背景图层级高显示在上面，后写的层级低)


CSS3透明度RGBA
参数：
1.opacity(透明度0-1)  opacity:0.5改变容器内的所有透明度

2.rgba(只透明背景，不透明背景上的文字，不仅可以应用到背景，也可以应用到文字、边框上，只要涉及到颜色都可以用，比如color:rgba(0,0,0,0.5) )

3.linear-gradient(线性渐变，不是加给background，而是加在background-image上，比如background-image:linear-gradient(to left, red ,yellow ,blue)   颜色可添加多个，方向加在第一个属性位置，可以单个使用to left/ to right/to top/to bottom，也可以组合使用/ to left bottom/ to right bottom/…) 还可以设置角度background-image:linear-gradient(10deg ,red yellow ,blue) 正数表示顺时针  还可以选择一个百分比background-image:linear-gradient(to bottom, red 10%, yellow 90%)

4.radial-gradient(径向渐变 从中心点向四周渐变) 没有标准化，需要加前缀 background-image:-moz-radial-gradient( left, red ,yellow ,blue) 去掉left前面的to，还是支持百分比 background-image:radial-gradient(bottom, red 10%, yellow 90%)



CSS3边框 圆角 多颜色 图片样式 阴影

1.CSS3边框属性
border-radius参数值可以写一个具体的数值10px 或者是百分比50%，一个椭圆角30px/50px ( x轴30px、y轴50px)
border-color  只有firefox支持 要加前缀，不支持混合写，要单分开写，写成-moz-border-left-color:blue yellow green pink; (多边框颜色) 配合用border:4px solid black;

2.CSS3图片设置
border-image 参数：url 宽度不写单位  延伸方式(repeat平铺向两侧  round中间向两侧自适应填充  stretch拉伸地填充) 

3.边框阴影
box-shadow 参数： x  y  blur  spread(模糊范围，在原来的基础上，向四周扩散的范围)  color  insert(内阴影)默认是外阴影，不用写
多阴影：box-shadow:0 -10px 15px red,10px 0 15px blue,10px 0 15px green,-10px 0 15px yellow 上右下左阴影

1.CSS3过渡属性trannsition 复合样式 可以分开来写  给父元素添加
Transition 参数：transition-duration表示时间(s、ms)  transition-property表示属性(all表示全部属性，也可以单指某个属性，如width)  transition-delay表示延迟时间(单位：s、ms时间可以取正数表示延迟执行，负数表示提前执行)运动形式(linear匀速、 ease 逐渐慢下来、ease-in加速、ease-out减速、ease-in-out先加速后减速、cubic-bezier(.29,-0.51,.32,1.48)bezier曲线 )  transition-timing-function参数 :steps(数字)可实现逐帧动画 


CSS3变形transform

1.transform 参数如下：
位移translate(x轴偏移量100px,y轴偏移量)--x,y相对于它自身进行偏移  复合样式写法transform:translateX(100px)  translateY(20px);
缩放scale(宽度放大2,高度缩小0.5)—接受的是一个比例值，元素的中心点缩放  复合样式写法 transform:scaleX(2)  scaleY(0.5)
旋转rotate(数值加单位10deg)  支持rotateX (上下转) rotateY(左右转)  写rotateZ跟rotate效果一样，是默认
斜倾skew(20deg,20deg) 同时也支持skewX skewY 向右为负值
执行顺序:从右向左，translate会受到之前的影响

2.transform-origin 基点设置 
transform-origin:center cemter/right bottom/100px 0  -2d
transform-origin中X  Y轴可以写单词，但Z轴必须写具体的数字  -3d


CSS3动画属性

1.animation:yhl 3s 1s infinite   @keyframes yhl { 0%{height:20px;} 100%{height:50px;} }
animation-name运动名字是自定义的 ，相当于定义一个函数名
animation-duration 运动的总时间 
animation-delay  运动延迟时间
animation-iteration-count  运动次数 infinite(无数次)
animation-timing-function 跟transition运动形式一样，默认ease 一共6种
@keyframes  关键帧  后接前面自定义的名字，相当于函数中的调用函数名

2.animation-fill-mode
forwards 运动停在终点
backwards 运动停在起点 (默认)

3.animation-direction 运动方向
alternate 奇偶性的，运动方向正好是反向的，就是出去回来来回反复
normal  正常的，不管奇数还是偶数都一样，都是出去，朝一个方向运动

4.animation-play-state 动画的播放状态 在js中用 对象.style.animationPlayState = “paused”
paused 暂停
running 运动


CSS3 -3D

1.perspective  景深  离屏幕多远的距离去观察元素  值越大幅度越小，值越小，视觉越近

2.backface-visibility  背面隐藏
hidden  背面隐藏  即使设置透明属性也不可见
visible  默认显示

3.transform-style
flat
preserve-3d  为了让多个子元素产生立体空间，配合景深一起用，两者同时出现

4.transform   3D
rotateX()
rotateY()   transform：rotate3d(0,1,0,90deg)  跟分开来写效果一样 1表示针对于哪个轴
rotateZ()
translateZ() 视觉上变大 向屏幕外偏移
scaleZ()   对立体图形有效  Z轴厚度变化  transform:scale3d(1,1,0.5)效果一样
3d 写法 translate3d(0,0,100px) 跟translateZ(100px)一样

5.perspective-origin 观察的基点 值取top left right bottom 可以自由组合


CSS3事件  利用事件来重复的添加动画效果

1.transitionend  过渡结束后触发  这个对象中elapsedTime代表总共持续的时间，跟transition中时间一致 explicitOriginalTarget当前的目标源  propertyName 当前变化的属性  type 事件类型是transitionend
在js中用一个监听事件，写成绑定的形式:
对象.addEventListener(“transitionend”,function(ev},false);

2.animationstart 动画开始时触发
在js中用一个监听事件，写成绑定的形式:
对象.addEventListener(“animationstart”,function(ev},false);

3.animationend 动画结束时触发

4.animationiteration 每次执行动画的时候触发 触发总次数-1


CSS3的分档布局

1.column-count  分栏的个数 没有标准化，要加前缀-moz-、-webkit
加了高度，在FF内容留空白， 在chrome下跟高度走

2.column-width 要加前缀
对分栏的宽度进行设置 会受到分栏个数的影响，所以两者不同时出现

3.column-gap 分栏的间距 加前缀

4.column-rule 分栏的边线 栏与栏之间的一个线段 –moz-column-rule:1px #f00 solid;

5.column-span 合并分栏 加给子元素 –webkit-column-span:all; 只在webkit支持 写成all占所有的分栏，写成1只占一栏


CSS3弹性盒模型

1.display:flex
display:box; flex-box:1;对种写法老式有兼容问题不推荐

2.flex-direction 主轴排列方向 加给父元素
row(默认) 水平靠左
row-reverse水平相反的一个排列，父元素靠右  并且子元素顺序相反321
column 垂直靠上
column-reverse垂直靠底

3.justify-content 主轴对齐
flex-start (默认) 靠左
flex-end  靠右，子元素顺序是正的123
center 居中
space-between 端点对齐，剩下的空白平均分配
space-around 子元素之间空白是平均分配 端点也有空白被分配到

4.align-items 侧轴对齐，跟主轴相反的轴 相对于主轴来说
flex-strat
flex-end
center

5.flex-wrap换行
nowrap  不换行(默认)
 wrap  换行
wrap-reverse   朝相反的方向 在另一头开始排

6.align-content 行之间对齐方式
flex-start 行与行之间没有任何空隙 ，从最开头排
flex-end  行与行之间没有任何空隙 ，从结尾排
center
space-between  最开头和结尾没有空隙地排
space-around  最开头和结尾有空隙地排

7.针对子元素
order  默认每个子元素都是0  order:1  就把1排在最后了，值越大，排得越往后
align-self 子元素的对齐方式 子元素高度或宽度不相同的情况下  align-self:start;(默认) 取值：start/end/center
flex  弹性布局 flex:1 flex:2 flex:3   分别占了1/6  2/6  3/6  可实现两侧弹性，中间不变 ，拉伸窗口随之自适应


CSS3媒体查询  注意顺序  一般放在最后 不然会覆盖别的样式   
先写大设备的尺寸，再过渡到小设备   在适配手机时 一般要float:none; width:100%; 手机上可能不需要浮动  在一些小设备上可能要隐藏一些功能display:block;与display:none的切换
media queries 
1.all   all 表示所有设备
@ media all and (min-width:500px) and ( max-width:700px) {
 #div1{ width:100px; height:100px; background:red; }  }
2.not  not写在all前面 表示相反的意思
3.min-width
4.max-width
5.orientation:portrait  竖屏  @media all and (orientation:portrait) {}
6.orientation:landscape  横屏  @media all and (orientation:landscape) {}
7.link写法
 <link href=”media.css” rel=”stylesheet”  media =”all and (min-width:500px) and ( max-width:700px)” />


CSS3其他

1.resize 改变图形样式 一定要配合overflow:hidden; 
resize:both; 出现拖拽图标both表示可以拖拽宽度 horizontal只能拖拽宽度 vertical 只能拖拽高度

2.box-sizing 改变盒模型的属性
border-box  
content-box

3.mask 遮罩 png格式的图片，图片透明 没有标准化，需要加前缀-webkit- 只支持webkit
url 引进图片路径
x  x偏移量
y  y偏移量
repeat/no-repeat
mask-position  单独分开，针对x 和 y  也可以复合写

4.box-reflect  倒影 只有webkit支持 加前缀
above 倒影在上边
below 倒影在下边
left  倒影在左边
right 倒影在右边
距离 倒影离原来的图片有多远
渐变 : 运动的方式，起点(x轴、y轴) ，终点(x轴、y轴) ，颜色从哪里到哪里
–webkit-gradient(linear, 0% 0%,100% 100%, from( rgba(255,255,255,0)),to(white))

5.blur模糊
filter:blur(0px) 写0跟正常图一样，值越大，模糊越厉害 chrome要加前缀

6.CSS3相关的插件
animate.css  动画
jquery.transit 跟transform transition有关 基于jquery
jquery.skrollr 视觉差 基于jquery 
