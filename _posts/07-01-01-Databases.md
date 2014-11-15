---
title: 資料庫
anchor: databases
---

# 資料庫 {#databases_title}

你的PHP程式碼常常需要使用資料庫來保存資訊，這時，你有一些選擇來連接並與你的資料庫互動，在**PHP 5.1.0之前**的推薦方案是使用一些原生的驅動程式，例如[mysqli], [pgsql], [mssql]等等。

如果你在應用程式中只使用 _一個_ 資料庫，原生的驅動程式(native driver)是一個很好的選擇。但是，假如你使用了MySQL和一點點的MSSQL，或是你需要連接到Oracle資料庫，那麼你就不能只使用同一個驅動程式，你將需要針對每個不同的資料庫學習API &mdash; 而這些行為非常的愚蠢。

## MySQL 擴充套件

PHP的[mysql]擴充套件已經不再主動的開發，[官方也在PHP 5.5.0時不贊成使用]，意思是mysql擴充套件將在接下來的幾個釋出版本移除。如果你正在使用類似`mysql_connect()` 和 `mysql_query()`這些`mysql_*`開頭的函式，這些函式將在未來的幾個版本不能使用了。這代表你將需要重寫程式，所以最好的選擇就是開始使用 [mysqli] 或是 [PDO]。

**如果你正要開始寫程式，那麼絕對不要使用 [mysql] 擴充套件: 請轉而使用[MySQLi extension][mysqli]或是使用[PDO]。**

* [PHP: 為MySQL選擇API](http://php.net/manual/en/mysqlinfo.api.choosing.php)
* [MySQL開發者們的PDO教學](http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers)

## PDO 擴充套件

[PDO] 是從 &mdash; PHP 5.1.0 &mdash; 可以開始使用的一個和資料庫連結的抽象程式庫，它提供了一個共同的介面來和不同的資料庫溝通。例如，你可以使用同一套程式碼和MySQL或是SQLite溝通。

{% highlight php %}
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO不會轉譯你的SQL請求，或是模擬失去的特性。它只是簡單的使用同一個API去連向各個不同類型的資料庫。最重要的是， `PDO` 允許你簡單的直接將外部的輸入插進你的SQL請求，而不需要擔心SQL注入攻擊(SQL injection attacks)。讓我們假設一個PHP腳本接收一個數字ID當作請求參數。這個ID是用來從資料庫取得使用者的資料。這是`錯誤`的使用方式。

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- 不!
{% endhighlight %}

這是一個很糟糕的程式碼，你正在插入一個未處理過的請求參數到資料庫請求中。這會導致你在一瞬間被駭入。用一個實際的案例來解釋這個情況:[資料庫注入攻擊](http://wiki.hashphp.org/Validation)。想像一下有一個駭客使用一個網址類似這樣`http://domain.com/?id=1%3BDELETE+FROM+users`。這將會造成 `$_GET['id']` 變數的值變成 `1;DELETE FROM users` ，這會刪除所有你的使用者！因此你應該要使用PDO bound parameters對這個ID輸入消毒。

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- PDO自動消毒這個變數
$stmt->execute();
{% endhighlight %}

這個是正確的程式碼，它在PDO敘述上使用了bound parameter。這些動作在被放入資料庫請求之前逃脫了外部的ID輸入以避免潛藏的資料庫注入攻擊。

* [學習PDO]

你應該要注意到資料庫連線沒有自行關閉而耗盡資源的問題，這個問題不是沒有前例的。當使用PDO的時候，你可以藉由摧毀物件來自行結束連線，以確保所有關聯到這個物件的東西都被刪除。例如，將它的值設為NULL。如果你沒有明確的將它關閉，那麼PHP會在腳本結束時自動的關閉連線，除非你使用的是持續的連線。

* [學習PDO連線]

[學習PDO]: http://www.php.net/manual/en/book.pdo.php
[學習PDO連線]: http://php.net/manual/en/pdo.connections.php
[官方也在PHP 5.5.0時不贊成使用]: http://php.net/manual/en/migration55.deprecated.php
[資料庫注入攻擊]: http://wiki.hashphp.org/Validation

[pdo]: http://php.net/pdo
[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[mssql]: http://php.net/mssql
