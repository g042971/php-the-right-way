---
isChild: true
title: Composer 與 Packagist 
anchor: composer_and_packagist
---

## Composer 與 Packagist {#composer_and_packagist_title}

Composer 是一個**傑出**的PHP套件管理程式。在 `composer.json` 檔案中寫入你專案所要使用的套件在打上一點簡單的指令，Composer 將會自動幫你下載並設定你專案中所需要的套件。

現在已經有許多 PHP 函式庫相容於 Composer，並且隨時都可以在你的專案中使用.這些"packages(套件)"都會列在 [Packagist][1]，這是一個官方的 Composer 相容的套件倉庫。

### 如何安裝 Composer

你可以區域性的安裝 Composer (在你目前工作的目錄;這裡不是很推薦)或是全域(e.g. /usr/local/bin).我們假設你想安裝區域的 Composer.從你專案的根目錄輸入:

    curl -s https://getcomposer.org/installer | php

這串指令將會下載 `composer.phar` (一個PHP執行檔)。你可以使用 `php` 執行這個檔案用來管理你的專案套件。
**註記:**假如你是直接下載程式來編譯，請先確認你下載編譯的檔案是否安全

#### Windows環境下安裝

對於Windows的使用者而言最簡單取得及執行的方法就是使用 [ComposerSetup][6] 安裝檔，安裝檔會提供全域性的 composer 及設定你的 `$PATH`，所以你可以直接在命令視窗中的任何目錄下使用 `composer`。

### 如何手動安裝 Composer

要手動安裝Composer是一件較進階的技術;僅管如此還是有許多開發者有各種原因喜歡使用這種互動式的應用程式安裝 Composer。在安裝前請先確認你的PHP安裝項目如下：

- 符合滿足Composer要求或以上的PHP版本
- `.phar` 類型檔案可以正確的被執行
- 相關的目錄權限有開放
- 相關有問題的擴展套件沒有被讀取
- 相關的 `php.ini` 設定已完成

由於手動安裝沒有做這些檢查，你必須自已衡量決定是否值得做這些事，以下是如何取得 Composer 手動安裝：

    curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

路徑 `$HOME/local/bin` (或是你選擇的路徑) 應該在你的 `$PATH` 環境變數中。這將會影響 `composer` 這個指令是否有效.

當你已經安裝到文件叫你執行 Composer 指令是 `php composer.phar install`時，你可以使用下列指令替代:

    composer install

本章節我們假設你已經全域性的安裝 Composer。

### 如何設定及安裝獨立套件

Composer 會持續的追縱你專案的獨立套件透過一個叫 `composer.json` 的檔案。 如果你希望你可以自已管理這個檔案。或是使用Composer它他自已會管理。`composer require` 這個指令會新增一個專案獨立套件進去且如果你沒有 `composer.json` 這個檔案他會直接建立。這裡有個範例是為你的專案加入 [Twig][2]這個獨立套件。

    composer require twig/twig:~1.8

另外 `composer init` 這個指令將會指引你建立一個完整的 `composer.json` 檔案在你的專案之中。無論你使用哪種方式當你已經建立你的 `composer.json` 檔案，你可以告訴 Composer 去下載及安裝你的獨立套件進 `vendors/` 目錄中。這這指令也適用於所有你已經下載並已經提供一個 `composer.json` 的專案：

    composer install

接下來，新增這一行到你的應用程式中主要 PHP 檔案，這將會告訴 PHP 使用 Composer 的自動讀取器並在你的專案中使用獨立套件。

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

現在你可以使用你專案中的獨立套件且它們會自動完成讀取的動作。

### 更新獨立套件

Composer 會建立一個檔案叫 `composer.lock` 並存放每個套件實際下載的版本編號當你第一次執行 `php composer.phar install` 時。假如你要分享你的專案給其他開發者。當 `composer.lock` 這個檔案也在你分享的檔案之中的話。 當別的開發者執行 `php composer.phar install` 這個指令時他們將會得到與你相同一樣的版本套件。 當你要更新你的獨立套件時請執行 `php composer.phar update`。

這是最有用且當你需要靈活的定義你所需要的套件版本. 舉例來說一個版本定義為 ~1.8 時他的意思為任何比 1.8.0 新的版本，但小於 2.0.x-dev"。你也可以使用 `*` 這個符號在 `1.8.*` 之中。現在Composer在更新時將會升級你的獨立套件至最新符合你所限制的版本。

### 更新通知

要接收關於新版本的更新通知。你可以註冊 [VersionEye][3]，這是一個網頁服務可以監控你的 Github 及 BitBucket 帳號中的 `composer.json` 檔案並且當有新套件更新時會寄 email 給你。

### 確認你的獨立套件資安議題

[Security Advisories Checker][4] 是一個網頁服務及一個指令工具二者都會檢查你的 `composer.lock` 檔案且告訴你假如你需要更新任何獨立套件。

* [其他學習Composer相關資源][5]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: https://www.versioneye.com/
[4]: https://security.sensiolabs.org/
[5]: http://getcomposer.org/doc/00-intro.md
[6]: https://getcomposer.org/Composer-Setup.exe
