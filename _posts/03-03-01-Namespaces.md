---
isChild: true
title: 命名空間
anchor: namespaces
---

## 命名空間 {#namespaces_title}

如前所述，PHP 社群裡許多開發者已經開發了大量的程式碼。這意味著一個函式庫的的 PHP 程式碼可能使用了另外一個函式庫中相同的類別名稱。如果他們使用同一個命名空間，那將會產生衝突導致異常。

_命名空間_ 解決了這個問題。如 PHP 手冊裡所描述，命名空間類似作業系統中的目錄，兩個同名的文件可以共存於不同的目錄下。同理兩個同名的 PHP 類別可以在不同的 PHP 命名空間下共存，就這麼簡單。

因此把你的程式碼放在你的命名空間下就非常重要，避免其他開發者擔心與第三方函式庫衝突。

[PSR-0][psr0] 提供了命名空間的推薦使用方式，它提供一個標準的文件、類別和命名空間的使用慣例，進而讓程式碼做到隨插即用。

2013 年 12 月，PHP-FIG 發布了新的自動加載標準：[PSR-4][psr4]，期望將來替換 PSR-0 標準。但 PSR-4 要求 PHP 5.3 以上的版本，而許多專案都還是使用 PHP 5.2，所以目前兩個都能使用。如果你在新應用或套件中使用自動加載標準，應優先考慮使用 PSR-4。

* [閱讀命名空間][namespaces]
* [閱讀 PSR-0][psr0]
* [閱讀 PSR-4][psr4]

[namespaces]: http://php.net/manual/en/language.namespaces.php
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
