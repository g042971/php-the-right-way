---
isChild: true
title: 與資料庫溝通
anchor: databases_interacting
---

##與資料庫溝通 {#databases_interacting_title}

當開發者們開始學習PHP，他們常常將資料庫溝通的動作與他們的表達邏輯混合，而使得程式碼長得像這樣:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
</ul>
{% endhighlight %}

這是一個很糟的例子，主要是因為它很難除蟲，很難測試，很難閱讀，而且沒有限制的話，它將會輸出過多資料。

而有非常多的方法可以達到同樣的目的，一切都看你喜歡哪種，[物件導向](/#object-oriented-programming) 或是 [函數編程](/#functional-programming) - 但是一定要有基本的分離。

考慮以下最基本的步驟:

{% highlight php %}
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos($db) as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // 不好!!
}
{% endhighlight %}

這是一個好的開始，將這兩個程式碼放在不同的兩個檔案，你將會得到一些乾淨的分離。

創造一個類別來放置這個方法，你將會得到一個 "Model"，再創造一個簡單的 `.php` 檔案來放入表達的邏輯，你將會得到一個 "View"，這非常接近 [MVC] - 一個對多數的 [frameworks](/#frameworks_title) 非常普遍的物件導向架構。

**foo.php**

{% highlight php %}
<?php

$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// 使你的model可以被使用
include 'models/FooModel.php';

// 創造一個實例
$fooList = new FooModel($db);

// 展示你的view
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class Foo()
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<? foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<? endforeach ?>
{% endhighlight %}

這是對許多現代的frameworks非常基本的架構，你不需要每次都做這些，但是將表達邏輯和資料庫溝通的部分混合，在想要做[單元測試](/#unit-testing)的情況下，這是一個非常真實的問題

[PHPBridge] 有個叫 [Creating a Data Class] 的資源來說明非常相似的主題，而且對剛開始接觸這些概念的程式開發者而言，這是一個不錯的開始。

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
[PHPBridge]: http://phpbridge.org/
[Creating a Data Class]: http://phpbridge.org/intro-to-php/creating_a_data_class