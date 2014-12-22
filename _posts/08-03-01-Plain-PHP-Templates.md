---
isChild: true
title: 原生 PHP 樣板 
anchor: plain_php_templates
---

## 原生 PHP 樣板 {#plain_php_templates_title}

原生 PHP 樣板是直接拿 PHP 來寫樣板。這是很直覺的選擇，因為 PHP 事實上就是個樣板語言。這代表你可以在其他的語言中結合 PHP 使用，像是 HTML。這對 PHP 開發者相當有利，不需要額外學習新的語法，他們熟知可以使用的函式，所使用的編輯器也已經內建語法高亮和自動補完。此外，原生 PHP 樣板少了編譯階段，速度更快。

現今的 PHP 框架都會使用一些樣板系統，這當中多數預設使用原生的 PHP 語法。在框架之外，一些函式庫如 [Plates](http://platesphp.com/) 或 [Aura.View](https://github.com/auraphp/Aura.View) ，提供現今樣板常見功能，像是繼承、佈局、外掛等，讓原生PHP樣板更容易使用。

### 原生 PHP 樣板的範例

使用 [Plates](http://platesphp.com/) 函式。

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
{% endhighlight %}

### 原生 PHP 樣板使用繼承的範例

使用 [Plates](http://platesphp.com/) 函式。

{% highlight php %}
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
{% endhighlight %}

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>
{% endhighlight %}
