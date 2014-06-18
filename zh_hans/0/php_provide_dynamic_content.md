#PHP让内容动起来

发表的文章怎么不见了？

因为那是静态HTML网页，不能处理数据。这时候就需要PHP了。

首先要配置一下nginx服务器，当发现请求了PHP文件时，就传递给PHP程序进行处理。

Windows：无需配置。wnmp已经默认配置好了，启动PHP和nginx即可。

Linux：按照下面的图片进行修改。

    sudo vi /etc/nginx/sites-enabled/default

![nginx conf php](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/nginx_conf_php.png)

修改完毕，重启nginx。

    sudo /etc/init.d/nginx reload

然后开始写代码。修改“发表页”add_article.html的表单，提交到PHP。代码如下：

    <h1>写文章</h1>
    <form action="add_article_submit.php" method="post">

add_article_submit.php收到数据，保存到哪里呢？最简单的方法：本地文件。代码如下：

    <?php
    $input = $_POST;
    $file = './articles.json';
    $data = array();
    if (file_exists($file)) {
        $tmp = file_get_contents($file); //读取文件，变成字符串
        if(!empty($tmp)) {
            $data = json_decode($tmp, true); //json解码成array
        }
    }
    $data[] = $input;
    file_put_contents($file, json_encode($data)); //把字符串保存到文件
    echo '保存成功';

能看懂这些代码吗？如果看不懂，学一下PHP语法，很简单。看这里：《PHP官方手册：第一个 PHP 页面》[http://www.php.net/manual/zh/tutorial.firstpage.php](http://www.php.net/manual/zh/tutorial.firstpage.php)

自学：0.5天。

然后把这些代码下载下来：[https://github.com/sinkcup/php-ebook-online-reader/tree/0.2.0](https://github.com/sinkcup/php-ebook-online-reader/tree/0.2.0)

在浏览器里访问，尝试录入一篇文章。如图：

![ebook add article](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/ebook_add_article.png)

![ebook add article submit](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/ebook_add_article_submit.png)

然后回到首页，刷新，看到文章列表，可以点进去阅读，如图：

![ebook articles](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/ebook_index_php_articles.png)

![ebook get article](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/ebook_get_article_php.png)

##总结一下

###我的技术水平

<table>
    <tr>
        <th>HTML</th>
        <th>PHP</th>
        <th>数据存储</th>
        <th>HTTP协议</th>
    </tr>
    <tr>
        <td>语义化：最简HTML</td>
        <td>让内容动起来</td>
        <td>文件存数据</td>
        <td>GET、POST</td>
    </tr>
</table>

###已解决的问题

* 提交的内容跑哪里去了？

    可以存到本地文件里

* GET和POST有什么区别？该用哪个？

    简单的说：GET表示读，POST表示写。

* 【阿里 IPO 后员工套现 410 亿美元，对杭州这个城市会有怎样的影响？】

    匿名用户：现身说法，房子有了，目前的代步车是mini，套现后换辆路虎揽胜，还有让妻子去香港生孩子，这就是我的计划。[http://zhi.hu/4OKR](http://zhi.hu/4OKR)（分享自知乎）

###待解决的问题

* PHP和HTML混写，很乱啊，怎么解决？

    且听下回分解。

* 保存之后，在Firefox中页面怎么乱码了？

    且听下回分解。
