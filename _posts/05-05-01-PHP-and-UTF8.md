---
title: Working with UTF-8
isChild: true
anchor: php_and_utf8
---

## 處理 UTF-8 {#php_and_utf8_title}

_此章節由 [Alex Cabal](https://alexcabal.com/) 撰寫，節錄自
[PHP Best Practices](https://phpbestpractices.org/#utf-8) 並作為我們 UTF-8 建議的基礎_。

### 這不是開玩笑的，請小心與細心並前後一致地處理它。

PHP 至今在底層仍未支援 Unicode。而有許多方式可以確認  UTF-8 字串的處理是正確的，但通常不容易，還需要從上而下翻遍程序所有階層，從 HTML、SQL 到 PHP。我們將會聚焦在簡短的實踐總結。

### UTF-8 在 PHP 階層

基本的字串操作，像是連接兩個字串、賦值給變數，並不需要特別作 UTF-8 處理。然而，大部分字串函數，像是 `strpos()` 和  `strlen()` 則確實需要考慮。這些函數通常以 `mb_*` 作為開頭：像是 `mb_strpos()` 和 `mb_strlen()`。這類函數藉由[Multibyte String Extension]設計用來專門用來處理  Unicode 字串。

每次操作 Unicode 字串，都必須使用 `mb_*` 這類函數。例如，若你對 UTF-8 字串使用 `substr()` 有很大的機會結果會是包含半字元的亂碼，正確的方式是使用 `mb_substr()`。

困難的是，要記得每次都使用 `mb_*` 函數，萬一有個地方沒有用到，那麼你的 Unicode 字串就有可能在接下來的程序中被轉變成亂碼。
並不是所有的字串函數都有對應的 `mb_*` 函數，就算只有一處沒有正確轉換，都有可能會出現亂碼。

你應該在 PHP 程式的開頭使用 `mb_internal_encoding()` (或是在最上層的全域載入的地方使用)，若是有輸出訊息到瀏覽器，則要再加上 `mb_http_output()` 函數。明確定義你的字串編碼可以幫你省下許多頭痛的時間。

此外，許多 PHP 字串函數都允許設定字元編碼，你應該總是設定成 UTF-8，例如，`htmlentities()` 函數。而在 PHP 5.4.0 之後已經將 UTF-8 作為 `htmlentities()` 和 `htmlspecialchars()` 預設編碼。

最後，如果你建立的是分散式架構程式，且不能確定 `mbstring` 函數是啟用狀態，那麼則建議使用 [patchwork/utf8] 這個 Composer 套件。它將會自動判斷該環境能否使用 `mbstring` 函數。

[Multibyte String Extension]: http://php.net/manual/en/book.mbstring.php
[patchwork/utf8]: https://packagist.org/packages/patchwork/utf8

### UTF-8 在資料庫階層

如果你是使用 PHP 來存取 MySQL，有可能會發生使用非 UTF-8 編碼來儲存資料，即使你有遵照上述的注意事項。

為了確保字串從 PHP 到 MySQL 都是 UTF-8 編碼，請確認資料庫和資料表都是設定為 `utf8mb4` 字元集，且使用 `utf8mb4` 作為 PDO 連線字串，請見以下範例，這將是非常重要的。

請注意，你必須使用 `utf8mb4` 字元集來作為完整的支援 UTF-8，而非使用 `utf8` 字元集！原因請參見瞭解更多。

### UTF-8 在瀏覽器階層

使用 `mb_http_output()` 函數來確保 PHP 輸出 UTF-8 字串給瀏覽器。

瀏覽器需要藉由 HTTP 回應來得知此頁面要被解析成 UTF-8 編碼，藉由歷史的方法來達到需要包含[字元集 `<meta>` 標籤](http://htmlpurifier.org/docs/enduser-utf8.html) 在頁面的 `<head>` 標籤內。這種方式是非常有效的，但是設定這個字元集到 `Content-Type` 標頭實際上會[更快](https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly)。

{% highlight php %}
<?php
// 告訴 PHP 此頁面從頭到尾使用 UTF-8 字串
mb_internal_encoding('UTF-8');

// 告訴 PHP 此頁面輸出 UTF-8 字串到瀏覽器
mb_http_output('UTF-8');

// 我們的 UTF-8 測試字串
$string = 'Êl síla erin lû e-govaned vîn.';

// 使用多位元字串函數來進行轉換
// 注意我們如何裁剪非 Ascii 字符來作為演示
$string = mb_substr($string, 0, 15);

// 連接資料庫來儲存轉換字串
// 參見文件的 PDO 範例，以獲得更多的資訊
// 注意 `set names utf8mb4` 指令!
$link = new \PDO(
                    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
                    'your-username',
                    'your-password',
                    array(
                        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_EXCEPTION,
                        \PDO::ATTR_PERSISTENT => false
                    )
                );

// 資料庫以 UTF-8 編碼儲存我們轉換的字串
// 你的資料庫和資料表是設定成 utf8mb4 字元集，對吧？
$handle = $link->prepare('insert into ElvishSentences (Id, Body) values (?, ?)');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->bindValue(2, $string);
$handle->execute();

// 取得我們剛才存入的字串，來驗證儲存正確。
$handle = $link->prepare('select * from ElvishSentences where Id = ?');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->execute();

// 將結果存入物件，待會要輸出到 HTML
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

header('Content-Type: text/html; charset=UTF-8');
?><!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            print($row->Body);  // This should correctly output our transformed UTF-8 string to the browser
        }
        ?>
    </body>
</html>
{% endhighlight %}

### 瞭解更多

* [PHP 手冊: 字串操作](http://php.net/manual/en/language.operators.string.php)
* [PHP 手冊: 字串函數](http://php.net/manual/en/ref.strings.php)
    * [`strpos()`](http://php.net/manual/en/function.strpos.php)
    * [`strlen()`](http://php.net/manual/en/function.strlen.php)
    * [`substr()`](http://php.net/manual/en/function.substr.php)
* [PHP 手冊: 多位元字串函數](http://php.net/manual/en/ref.mbstring.php)
    * [`mb_strpos()`](http://php.net/manual/en/function.mb-strpos.php)
    * [`mb_strlen()`](http://php.net/manual/en/function.mb-strlen.php)
    * [`mb_substr()`](http://php.net/manual/en/function.mb-substr.php)
    * [`mb_internal_encoding()`](http://php.net/manual/en/function.mb-internal-encoding.php)
    * [`mb_http_output()`](http://php.net/manual/en/function.mb-http-output.php)
    * [`htmlentities()`](http://php.net/manual/en/function.htmlentities.php)
    * [`htmlspecialchars()`](http://www.php.net/manual/en/function.htmlspecialchars.php)
* [PHP UTF-8 一覽表](http://blog.loftdigital.com/blog/php-utf-8-cheatsheet)
* [Stack Overflow: 是什麼原因讓 PHP 與 Unicode 不相容?](http://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: PHP 和 MySQL 處理各種語言字串的最佳實務](http://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [如何使 MySQL 資料庫完整支援 Unicode](http://mathiasbynens.be/notes/mysql-utf8mb4)
* [使用可攜式 UTF-8 方式來使 PHP 支援 Unicode](http://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
