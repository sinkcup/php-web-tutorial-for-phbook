#表现与业务逻辑分离

##PHP和HTML混写，很乱啊，怎么解决？

一个页面分成两个文件即可，一个PHP做逻辑，一个HTML做模板。

比如“首页”`index.php`分成：`index.php`和`index.html`。`index.php`代码如下：

    <?php
    $articles = array();
    $file = './articles.json';
    if (file_exists($file)) {
        $tmp = file_get_contents($file);
        if (!empty($tmp)) {
            $articles = json_decode($tmp, true);
        }
    }

    $d = array(); //d 是 data的意思，后续会用到
    $d['articles'] = $articles;
    require_once __DIR__ . '/index.html';

`index.html`代码如下：

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
            <?php
                if (!empty($d['articles'])) {
                    echo '<ul>';
                    foreach ($d['articles'] as $k=>$v) {
                        $id = $k + 1;
                        echo '<li><a href="./get_article.php?id=' . $id . '">' . $v['title'] . '</a>';
                        echo '<p>' . mb_substr($v['content'], 0, 100, 'UTF-8') . '……</p></li>';
                    }
                    echo '</ul>';
                }
            ?>
        </body>
    </html>

##保存之后，在Firefox中页面怎么乱码了？

打开`add_article_submit.php`的源代码看一下，只输出了“保存成功”，那这不是一个网页。一个正常的网页需要包含DOCTYPE html、head、body等内容，其中head里的charset声明了编码，这样浏览器才能正常显示。所以添加一个`notice.html`模板即可。代码如下：

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE html
        PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="zh-Hans" lang="zh-Hans">
        <head>
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
            <title>提示：<?=$d['notice']['msg']?></title>
        </head>
        <body>
            <h1>提示：<?=$d['notice']['msg']?></h1>
            <p><a href="/">回到首页</a></p>
        </body>
    </html>

截图如下：

![notice ok](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/notice_ok.png)

##总结一下

###我的技术水平

<table>
    <tr>
        <th>HTML</th>
        <th>PHP</th>
        <th>数据存储</th>
        <th>HTTP协议</th>
        <th>计算机文化导论</th>
        <th>装备</th>
        <th>等级</th>
    </tr>
    <tr>
        <td>语义化</td>
        <td>让内容动起来</td>
        <td>单机文件</td>
        <td>GET、POST</td>
        <td></td>
        <td>PC + Windows</td>
        <td>0.2</td>
    </tr>
    <tr>
        <td></td>
        <td>表现与业务分离</td>
        <td></td>
        <td>charset</td>
        <td>Unicode</td>
        <td></td>
        <td>0.3</td>
    </tr>
</table>

代码下载：[https://github.com/sinkcup/php-ebook-online-reader/tree/0.3.0](https://github.com/sinkcup/php-ebook-online-reader/tree/0.3.0)

###已解决的问题

* PHP和HTML混写，很乱啊，怎么解决？

    把HTML单独保存，PHP中require即可，这样就实现了表现与业务逻辑分离。

* 保存之后，在Firefox中页面怎么乱码了？

    HTTP协议中有header，其中Content-Type用于指定是网页、文本还是json等等，编码推荐使用utf-8。如何查看header？Chrome/Firefox浏览器——》F12——》网络，或者命令行curl -i即可。

* ANSI与ASCII的区别，UTF-8与Unicode的区别，GB2312、CP936、GBK、GB18030的区别，为什么技术公司的程序（Android、iOS、Linux、OS X、Windows）都使用Unicode？
    请自行学习。

###待解决的问题

* 查看`get_article.php`的代码，读一篇文章，却把所有文章取了出来，再取其中一篇，这样浪费性能啊，如果文章有成千上万篇，那怎么办？

    且听下回分解。
