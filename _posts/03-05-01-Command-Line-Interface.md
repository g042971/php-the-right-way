---
isChild: true
title: 命令列介面
anchor: command_line_interface
---

## 命令列介面 {#command_line_interface_title}

PHP 主要是用來開發網頁應用程式，但用來開發命令列介面（CLI）程式也很好用。命令列程式可以幫你完成自動化的任務，如測試、部署和應用管理。

CLI 程式很強大，因為你可以直接使用應用的程式碼而不需要為它建立網頁圖形化介面。唯一要注意的是，請不要將你的 CLI 程式放置在公開的網頁根目錄下。

試著在命令列下執行 PHP：

{% highlight bash %}
> php -i
{% endhighlight %}

選項 `-i` 會像 [`phpinfo`][phpinfo] 函式一樣將你的 PHP 設定值顯示出來。

選項 `-a` 提供一個互動式介面，類似 ruby 的 IRB 或者是 python 的互動式介面。此外還有其他有用的 [命令列選項][cli-options]。

接下來，來寫一個簡單的 “Hello, $name” CLI 程式。首先建議一個名為 `hello.php` 的檔案如下。

{% highlight php %}
<?php
if ($argc != 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

PHP 會在程式執行時根據參數建立兩個特別的變數，[`$argc`][argc] 是一個整數，代表參數的 *個數*。[`$argv`][argv] 則是一個陣列變數包含了每個參數的 *值*。而第一個變數就是你的程式檔名，如此例中即是 `hello.php`。

命令執行失敗時，可以使用 `exit()` 表達式來返回一個非零整數來告知 Shell。常用的 exit 返回值可以查看 [列表][exit-codes]。

執行上述的程式，在命令列輸入：

{% highlight bash %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [學習如何從命令列執行 PHP][php-cli]
 * [學習如何在 Windows 下從命令列執行 PHP][php-cli-windows]

[phpinfo]: http://php.net/manual/en/function.phpinfo.php
[cli-options]: http://www.php.net/manual/en/features.commandline.options.php
[argc]: http://php.net/manual/en/reserved.variables.argc.php
[argv]: http://php.net/manual/en/reserved.variables.argv.php
[php-cli]: http://php.net/manual/en/features.commandline.php
[php-cli-windows]: http://www.php.net/manual/en/install.windows.commandline.php
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&topic=sysexits
