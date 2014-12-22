---
isChild: true
title: 編譯樣板
anchor: compiled_templates
---

## 編譯樣板 {#compiled_templates}

PHP 不斷進化為成熟、物件導向的語言，但它作為樣板語言[沒有改善多少](http://fabien.potencier.org/article/34/templating-engines-in-php)。編譯樣板，像是 [Twig](http://twig.sensiolabs.org/) 或 [Smarty](http://www.smarty.net/)*，提供樣板專用的新語法，補足了這片空白。從自動逸脫到繼承以及簡化控制結構，編譯樣板設計地更容易撰寫、可讀性更高、使用上更為安全。編譯樣板更能在不同的語言中使用，[Mustache](http://mustache.github.io/) 就是一個極佳例子。由於這些樣板需要編譯，在效能方面會帶來些許影響，不過如果適當使用快取，影響就十分有限。

**雖然 Smarty 提供自動逸脫機制，不過這個功能並非預設啟用。*

### 編譯樣板範例

使用 [Twig](http://twig.sensiolabs.org/) 函式庫。

{% highlight text %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### 編譯模例使用繼承的範例

使用 [Twig](http://twig.sensiolabs.org/) 函式庫。

{% highlight text %}
{% raw %}
// template.php

<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
{% endraw %}
{% endhighlight %}

{% highlight text %}
{% raw %}
// user_profile.php

{% extends "template.html" %}

{% block title %}User Profile{% endblock %}
{% block content %}
    <h1>User Profile</h1>
    <p>Hello, {{ name }}</p>
{% endblock %}
{% endraw %}
{% endhighlight %}
