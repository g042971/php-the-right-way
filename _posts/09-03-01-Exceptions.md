---
isChild: true
title: 例外
anchor: exceptions
---

## 例外 {#exceptions_title}

例外是許多流行語言的標準配備，但它們往往被 PHP 開發人員忽視。像 Ruby 就是一個極端重視例外的語言，無論有什麼不對勁發生，像是 HTTP 請求失敗，或是資料庫的查詢有問題，甚至像找不到圖片，Ruby (或是所使用的gem)，將會丟出例外到畫面上，讓你立刻了解問題發生了。

PHP 看待這事則是相當隨意，呼叫「file_get_contents()」通常只會給出「FALSE」值和警告。許多較早的 PHP 框架像是 CodeIgniter 只是回傳 false、將訊息寫入記錄，頂多讓你使用像「$this->upload->get_error()」來檢視錯誤原因。這裡的問題出在你必須找出錯誤所在，並且檢視文件來查看這個類別使用什麼樣的錯誤方法，而不是明顯曝露錯誤。

另一個問題是發生在類別自動丟出錯誤到畫面並跳出程序。當你這樣做時，其他開發者動態處理錯誤的機會也被擋下了。例外應該丟出能讓開發人員意識到錯誤的存在，讓他們可以選擇處理的方式，例如：

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // 驗證失敗
}
catch(Fuel\Email\SendingFailedException $e)
{
    // 無法寄出信件
}
finally
{
    // 無論丟出什麼樣的例外都會執行，並且在正常程序繼續之前執行
}
{% endhighlight %}

### SPL 例外

原生的「例外」類別沒有提供太多除錯脈絡給開發人員，要修正的解法是建立一個特殊的「Exception」類型，方式是從原生「Exception」類別建立一個子類別：

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

如此一來，可以加入多重 catch 區塊，並且依不同的例外分別處理。這也可以建立<em>許多</em>客製例外，其中有些已經避免使用在 [SPL 擴充套件][splext] 提供的 SPL 例外。

舉例來說，如果你使用「__call()」魔術方法去呼叫了無效的方法，而不是丟出模糊的標準 Exception，或是建立客製例外專門處理，你可能已經幹了「throw new BadMethodCallException;」。

* [Read about Exceptions][exceptions]
* [Read about SPL Exceptions][splexe]
* [Nesting Exceptions In PHP][nesting-exceptions-in-php]
* [Exception Best Practices in PHP 5.3][exception-best-practices53]

[exceptions]: http://php.net/manual/en/language.exceptions.php
[splexe]: http://php.net/manual/en/spl.exceptions.php
[splext]: /#standard_php_library
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
