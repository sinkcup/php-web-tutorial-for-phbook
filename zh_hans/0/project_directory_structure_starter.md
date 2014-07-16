#目录规划意识的觉醒

##访问index.php是正常网页，但访问index.html看到了什么？

![访问模板文件](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/some_files_should_not_be_accessed.png)

如上图所示，访问`index.html`会看到代码片段，而不是正常的网页，这会给用户带来困惑。所以应该只允许访问`index.php`、`add_article.html`、`get_article.php`等文件，其他文件一律禁止访问，比如`index.html`这种模板文件。

如何禁止访问呢？

把允许访问的文件放在一个目录，修改HTTP Server的根目录指向这里即可。

本来项目里没有目录，所有文件都放在一起，是这样的：

    add_article_submit.php
    get_article.html
    get_article.php
    index.html
    index.php

改成下面的目录结构：

    htdocs/
        add_article_submit.php
        get_article.php
        index.php
    res/
        /layout/
            get_article.html
            index.html

然后找到nginx的配置文件，在这里：

* Windows：`C:\Wnmp\Conf\nginx.conf`

* Linux： `/etc/nginx/sites-enabled/default`

修改其中的server->root，重启nginx即可。如图所示：

![修改nginx conf root](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/nginx_root.png)

目录变了，包含就变了，记得`index.php`等php文件中的代码要改。以前是：

    require_once __DIR__ . '/index.html';

要改成：

    require_once __DIR__ . '/../res/layout/index.html';

然后访问`index.html`会出现404错误，即“不存在”。而访问`index.php`是可以的，如图所示：

![index.html 404](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/index_404.png)

##多个文件里都连了数据库，如果密码变了，每个地方都要改，怎么办？

同一件事情，重复做很多次，浪费了时间，是编程的大忌，违反了DRY原则（don't repeat yourself）。使用配置文件即可解决此问题。

配置文件用什么格式？打开PHP安装后的目录，会发现lib/php.ini文件，这是PHP的配置文件，由此可知PHP原生支持ini格式。本书也采用ini格式。配置文件当然也不应该让用户访问，所以单独建一个conf目录，现在项目目录结构如下：

    conf/
        db.ini
    htdocs/
        add_article.html
        get_article.php
        index.php
    res/
        /layout/
            get_article.html
            index.html

db.ini的内容如下：

    host="127.0.0.1"
    port="3306"
    dbname="reader"
    charset="utf8"
    username="root"
    password="1"

然后每个php页面解析配置文件，连接数据库，执行SQL。代码如下：

    $conf = parse_ini_file(__DIR__ . '/../conf/db.ini');
    $dsn = 'mysql:host=' . $conf['host'] . ';port=' . $conf['port'] . ';dbname=' . $conf['dbname'] . ';charset=' . $conf['charset'];
    $db = new PDO($dsn, $conf['username'], $conf['password']);

如图所示：

![php解析ini](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/php_parse_ini.png)

可以看到，如果数据库地址、用户名、密码改了，只用改db.ini即可，很方便。

代码下载：[https://github.com/sinkcup/php-ebook-online-reader/tree/0.5.0](https://github.com/sinkcup/php-ebook-online-reader/tree/0.5.0)

##总结一下

###我的技术水平

<table>
    <tr>
        <th>HTML</th>
        <th>PHP</th>
        <th>数据存储</th>
        <th>HTTP协议</th>
        <th>程序员的自我修养</th>
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
    <tr>
        <td></td>
        <td>PDO</td>
        <td>MySQL</td>
        <td></td>
        <td></td>
        <td></td>
        <td>0.4</td>
    </tr>
    <tr>
        <td></td>
        <td>目录规划</td>
        <td></td>
        <td></td>
        <td>DRY</td>
        <td></td>
        <td>0.5</td>
    </tr>

</table>


###已解决的问题

* 访问index.php是正常网页，但访问index.html看到了什么？

    用户看到了代码片段，这是不对的，目录规划隔离即可。

* 多个文件里都连了数据库，如果密码变了，每个地方都要改，怎么办？

    谨记DRY，使用ini配置文件。当然还可以使用PHP array、PHP object、JSON，请自行了解。

* 【锤子手机 Smartisan T1 正式发售版的实际使用体验如何？】

    喻梦萱：谢邀。。。 11日早上收到的，优先码来源是自己购买的发布会门票。总体感觉是…美哭了…非常非常精致。… [http://zhi.hu/5h2M](http://zhi.hu/5h2M)（分享自知乎）

###待解决的问题

* 单引号能保存吗？会导致什么后果？

    请按照截图进行实验。且听下回分解。

![单引号实验保存1](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/single_quote_mark.png)
![单引号实验保存2](http://com-163-sinkcup-php-web-tutorial-create-online-reader.qiniudn.com/sql_injection.png)
