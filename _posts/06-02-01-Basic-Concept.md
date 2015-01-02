---
isChild: true
title: 基本概念
anchor: basic_concept
---

## 基本概念 {#basic_concept_title}

我們可以用一個簡單而樸實的例子來說明這個概念。

這裡我們有一個 `Database` 類別它需要個配接器來跟資料庫溝通。
我們在建構式實例化配接器並建立寫死的依賴關係。
這使得測試困難並意味 `Database` 類別跟配接器有非常緊密地耦合。

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

這段程式碼可以用依賴注入重構並因此鬆開了依賴關係。

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(MySqlAdapter $adapter)
    {
        $this->adapter = $adapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

現在我們給 `Database` 類別它的依賴關係而不是它自己建立依賴關係。 我們可以建立
接受一個依賴關係參數的方法並用這個方法設定它，或者 `$adapter` 屬性是 `public` 我們可以直接設定它。
