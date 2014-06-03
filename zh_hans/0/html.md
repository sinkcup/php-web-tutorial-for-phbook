#语义化HTML

打开浏览器，访问一个网站，看到了漂亮的网页。比如豆瓣（[douban.com](http://douban.com)）是这样的：
![豆瓣首页截图](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/douban_homepage.png)

右键“查看页面源代码”，看到了一行行的文本。是这样的：
![豆瓣首页HTML源代码截图](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/douban_homepage_sourcecode.png)

把这些代码复制下来，保存成index.html文件，用浏览器打开，看到了和访问douban.com一样的内容。如图：
![豆瓣首页HTML源代码保存到本地](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/douban_sourcecode_save_as_localfile.png)

这就是HTML，写的时候是一行行的文本，用浏览器打开，就会渲染成图形化的界面。

下面开始开发一个“在线阅读网站”，可以用来当小说网站、博客、新闻网站等等。

先来规划一下产品要做哪些功能？

* 首页：显示文章列表，列表里显示每篇文章的标题、摘要。

* 详情页：显示整篇文章。

* 发表页：给出文本框，录入保存文章。

首页的HTML代码如下：

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE html
        PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="zh-Hans" lang="zh-Hans">
        <head>
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
            <title>在线阅读</title>
        </head>
        <body>
            <h1>在线阅读</h1>
            <div><a href="./add_article.html">写文章</a></div>
            <ul>
                <li><a href="./get_article.html?id=1">论不同的科学上网的方式对数据造
    成的影响</a>
                    <p>摘要：通过对不同的科学上网的方式的体验和说明，试图探寻其造成>这种现象的背后的原因。并为其他研究者提供理论依据。 1) GoAgent  口感偏硬，数据刚>朗，不经任何的加工和修饰，尤其是在 Windows 下使用，一口咬下去让人头皮发麻。即便>最新的产品通过 rc4 稍稍润饰，但仍旧无法洗去那钻……</p>
                </li>
                <li><a href="http://tech.163.com/11/0401/15/70IJH2KI000915BF.html" target="_blank">奇虎360上市 员工平均身价580万</a>
                    <p>“360员工全部进入北京二环以内。”现场一位北京记者的一句戏言，引发现场爆发出欢呼。奇虎总裁齐向东对本报表示，360此举，确实创造了中国互联网的员工>致富神话。据了解，入职9个月以上的员工一般就能拿到股份，一般员工持股4000股左右，>按照每股34美元减去相关费用计算，获利约70多万元人民币……</p>
                </li>
                <li><a href="http://www.douban.com/note/214971831/" target="_blank">你想在一个暮气沉沉的大公司里写一天用不上的代码然后回家撸撸就睡？</a>
                    <p>在我们这里，你可以得到什么？
                    1.跟对一个老大，参与一个伟大的公司的创业；
                    2.在它伟大之前，就得以在一个甚至能输出价值观的牛逼公司里骄傲地工
    作；
                    3.虽然我们相信你不会舍得早早从这样的公司退休，但还是为你准备了一
    份上市时就足以让你退休、足以让你彻底沦为一个废物的股份/期权；
                    4.每人一把Herman Miller的Embody，或okamura的contessa。

                     来吧，小伙子们，这多半是你们一生一次的机会，把个人简历投到这里吧：
                     laoluomobile@gmail.com

                      罗永浩
                      </p>
                </li>
            </ul>
        </body>
    </html>


在浏览器中打开是这样的：
![ebook首页](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/ebook_index.png)

能看懂这些代码吗？如果看不懂，自学一下HTML语法就行了，很简单，预计需要1至2天时间。教程在这里：《梦之都HTML教程》[www.dreamdu.com](http://www.dreamdu.com/xhtml/)。

自学：2天。

注意：截图的Firefox右上角有个“0错误/0警告”，这是Firefox扩展HTML Validator，能保证你写出100%标准的HTML，特别方便，推荐安装。下载页面：[http://users.skynet.be/mgueury/mozilla/](http://users.skynet.be/mgueury/mozilla/)。

学完HTML，知道语义化是什么意思了，会写最简洁的HTML了，那咱们继续。

刚才的代码是首页，其他还有详情页、发表页，在这里：

代码下载：[https://github.com/sinkcup/php-ebook-online-reader/tree/0.1](https://github.com/sinkcup/php-ebook-online-reader/tree/0.1)

下载以后，你就可以看到截图里的精彩内容，知道如何“在北京买房”、“9个月挣到70w”、“30岁退休”，当然了，为了吸引青年男女，特意放了几篇XXOO相关的文章，其中有一篇是老罗写的，很精彩又不低俗，人格担保，你懂的。

##总结一下

###我的技术水平

<table>
    <tr>
        <th>HTML</th>
    </tr>
    <tr>
        <td>语义化：最简HTML</td>
    </tr>
</table>

###已解决的问题

* 零基础如何学习HTML

    自学[《梦之都HTML教程》](http://www.dreamdu.com/xhtml/)。

* 如何写出100%标准的HTML

    使用Firefox扩展[HTML Validator](http://users.skynet.be/mgueury/mozilla/)即可。

###待解决的问题

* 这些HTML代码都在电脑上存着，本地能打开，但别的电脑、手机如何访问呢？

    且听下回分解。
