---
title: 程式碼風格指南
anchor: code_style_guide
---

# 程式碼風格指南  {#code_style_guide_title}

PHP 社群百花齊放，擁有大量的函式庫、框架和元件。PHP 開發者通常會選擇多個外部套件並將它們整合進單一專案中。因此 PHP 程式碼遵循（盡可能接近）一個共通的程式碼風格就會非常重要，這讓開發者可以輕鬆地將多個外部套件整合在自己的專案當中。

[Framework Interop Group][fig] 提出並通過了一系列的風格建議。其中有部分是關於程式碼風格的，即 [PSR-0][psr0]、[PSR-1][psr1]、[PSR-2][psr2] 和 [PSR-4][psr4]。這些建議是由一系列專案像是 Drupal, Zend, Symfony, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium 所採用。你可以在您的專案中使用或者是繼續使用您自己的風格。

理想狀況下，你應該遵循一個已知的標準來撰寫 PHP 程式碼。可能是 PSR 的組合或者是 PEAR 或 Zend 程式碼標準的其中一個。這代表其他開發者能夠方便的閱讀與使用你的程式碼，且使用這些套件的應用程式能夠平順地與許多第三方套件一起使用。

* [閱讀 PSR-0][psr0]
* [閱讀 PSR-1][psr1]
* [閱讀 PSR-2][psr2]
* [閱讀 PSR-4][psr4]
* [閱讀 PEAR 編碼準則][pear-cs]
* [閱讀 Zend 編碼準則][zend-cs]
* [閱讀 Symfony 編碼準則][symfony-cs]

你可以使用 [PHP_CodeSniffer][phpcs] 來檢查程式碼是否符合這些準則，而文字編輯器 [Sublime Text 2][st-cs] 的套件也可以提供即時檢查。

使用 Fabien Potencier 的 [PHP Codeing Standards Fixer][phpcsfixer] 可以自動修正你的程式碼語法，讓其符合標準，不用你自己手動修復。

所有的變數名稱和程式碼結構建議使用英文編寫。註解可以使用任何語言，只要讓現在及未來的夥伴能夠容易閱讀即可。

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
