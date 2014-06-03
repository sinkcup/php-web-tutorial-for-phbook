#搭建开发环境服务器

这些HTML代码都在电脑上存着，本地能打开，但别的电脑、手机如何访问呢？

安装HTTP server即可，常见的有nginx、apache。本书以流行的nginx为例。

看过《计算机互联网导论》的童鞋可能知道，计算机有很多种：电脑、服务器、手机、平板、路由器等等，其中电脑是面向个人桌面的，分为两种：PC和Mac，PC上面主要安装Windows系统、Linux系统，Mac上面主要是OS X。引用那本书的两个数据表格：

##电脑操作系统市场占有率

<table>
    <tr>
        <th>硬件</th>
        <th>OS</th>
        <th>市场占有率</th>
    </tr>
    <tr>
        <td>x86 PC</td>
        <td>Windows（个人使用￥400起，公司商业使用￥1988起）</td>
        <td>90%</td>
    </tr>
    <tr>
        <td>x86 PC</td>
        <td>Linux（￥0）</td>
        <td>1%</td>
    </tr>
    <tr>
        <td>x86 Mac</td>
        <td>OS X（￥0）</td>
        <td>8%</td>
    </tr>
</table>

##各大公司使用的服务器操作系统

<table>
    <tr>
        <th>硬件</th>
        <th>OS</th>
        <th>谁在用</th>
    </tr>
    <tr>
        <td>x86-64 server（arm-64正在起步）</td>
        <td>Linux server</td>
        <td>Google、Facebook、腾讯、阿里、百度、小米、锤子、360等绝大部分互联网公司</td>
    </tr>
    <tr>
        <td>x86-64 server</td>
        <td>Windows server</td>
        <td>微软、事业单位、传统行业等非技术公司</td>
    </tr>
</table>

很明显，服务器大部分都是Linux的，因为系统免费又开源，可以自行修改定制；硬件可自由选择，便宜；命令行界面适合脚本编程实现自动化。

不过大陆高校与技术前沿脱节比较严重，编程教科书、机房都是Windows的，没有Linux，也没有Mac。如果你热爱编程，经过几年的实践，自然就去接触到Linux服务器自动化部署、代码自动化测试发布，这就是自动化，不再喜欢在界面上点来点去了。而且这时候你所在的公司也不一样了，到了前沿技术公司，没有Windows，只有Linux和OS X，和服务器环境一致或接近，比如Google、豆瓣、小米、饿了么，甚至二三线公司比如安居客。

举个例子，大家也许就明白了：“学校机房需要给1000台电脑安装盗版Office、QQ等几十个软件，你会怎么做？跑到每台电脑上点下一步？1天之内能完成吗？这时候就知道自动化的意义了。”。

有的童鞋看到这个问题乐了，休息一下，请看这里：[zhi.hu/31MG](http://zhi.hu/31MG)

回到正题，现在假设你是一个编程菜鸟，热爱图形界面，痛恨命令行。没关系，本章就是面向菜鸟的，大家都是从这个阶段过来的，在大陆的Windows教育下，菜鸟热爱图形界面是正常的，不丢人。那你很可能用的是Windows，如果用的是Linux或OS X，那说明你爱钻研，领先同龄人好几年。

入门时，如何快速搭建开发环境？

Windows：下载wnmp（[getwnmp.org](http://www.getwnmp.org/)），图形界面的，点下一步安装，右键使用管理员权限启动即可。

Ubuntu（Linux有很多版本，本书以流行的Ubuntu为例）：一个命令即可

    sudo apt-get install nginx php5-fpm

Mac：

    brew install nginx

安装过程不再截图，不再详述，因为“DIY、装系统、装软件、Android刷机”对于计算机爱好者来说，是小意思。如果你刚刚大一，对这些不熟，没关系，多装几次就熟了，有问题“Google一下，你就知道的太多了”。如果装过几次，你发现自己对“CPU、内存、显卡、固态硬盘、系统、软件、网站”不感兴趣，嫌麻烦不爱折腾，那说明你真的不爱好计算机，千万不要学编程，立即停止阅读本书，转专业还来得及，钻研感兴趣的方向，否则工作几年差距越来越大，别人感兴趣，自然爱折腾爱钻研，进入BAT一线公司（[应届一本本科生起薪12w](http://zhi.hu/3yYh)），逐渐成为高级工程师、架构师、技术专家，或者去创业9个月挣70w，而你在一个不感兴趣的行业里，一直是入门级工程师打杂，只能在二线公司（新浪、网易、搜狐，应届本科生月薪几千），甚至在三流四流公司，一直工资低，碌碌无为。

装好以后，用浏览器访问[http://localhost/](http://localhost/)，看到一个简单的网页，是这样的：

![nginx](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/nginx.png)

这个网页在哪呢？找到以后，把上次下载的网站代码放进去，换掉它，就行了吧？

对。

Windows：在C:\Wnmp\html\，把index.php删除，然后把index.html等等放进去。

Linux：在/usr/share/nginx/html/，修改权限，然后把index.html等等放进去。

    sudo chmod -R 777 /usr/share/nginx/html

这时候用浏览器访问[http://localhost/](http://localhost/)，就看到网站了。不过localhost代表本机，别人还是访问不了。所以别人要通过IP访问，比如我的电脑IP是192.168.1.107，那访问[http://192.168.1.107/](http://192.168.1.107/)即可。如图：

![nginx localhost and IP](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/nginx_localhost_and_ip.png)

注意：这是内网IP，在同一个内网里可以访问，比如学校等大局域网环境。如果想对外提供网站服务，需要一个公网IP。那时候就需要购买云服务器了，那是另一个话题“搭建生产环境服务器”，以后再说。

IP都是数字太难记了，现在网站都是用域名啊。如何使用域名访问本网站呢？

很简单，域名是由域名注册商出售的，在google中搜索domain即可，各家价格都差不多，.com后缀约$8/年，还有很多有意思的后缀，比如[douban.fm](http://douban.fm)、[zhi.hu](http://zhi.hu)、[github.io](http://github.io)、[jianshu.io](http://jianshu.io)。但国内域名注册商大部分都不正规，你购买了域名，会发现实际管理员邮箱是商家的，最重要的资产是域名转移码，都不在你手里，这就很危险，你买的东西却不属于你，仍然属于商家。而在国外购买域名就很正规，管理员邮箱、转移码都是你的。

常见的国外域名注册商支持支付宝的有：[godaddy.com](http://www.godaddy.com/China)、[resellerclub.com](http://www.resellerclub.com)，支持VISA的就很多了，比如register.com、name.com。

网站正式运营的时候，需要购买顶级域名。现在只是学习开发，那申请一个免费的二级域名即可。提供免费二级域名的商家很多，比如在花生壳[oray.com](http://oray.com/)，注册登录后，进入我的控制台——域名管理——壳域名——添加域名即可。比如我申请了一个sinkcup.wicp.net，指向192.168.1.107，如图：

![oray subdomain](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/free_subdomain.png)

现在一个网站就诞生啦！点“写文章”，然后“发表”，观察发生了什么。

##总结一下

###我的技术水平

<table>
<tr>
<th>HTML</th>
<th>服务器部署</th>
</tr>
<tr>
<td>语义化：最简HTML</td>
<th>管理员权限GUI或CLI安装包</th>
</tr>
</table>

###已解决的问题

* 如何提供网站服务

安装HTTP server即可。

* 通过IP访问网站，很难记怎么办

购买顶级域名，或者申请免费的二级域名。

###待解决的问题

* 哪里能找到《计算机互联网导论》这本书？

找不到……我正在写的，还没写完……有一本讲互联网的书《浪潮之巅》，很精彩，推荐阅读，但不是面向大一新生互联网入门的，所以我才想到写一本导论。如果大家喜欢现在情况，而不是“第一台计算机是什么时候诞生的”这种导论……欢迎联系我，参加试读。

* 发表的文章怎么不见了？

且听下回分解。
