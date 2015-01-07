---
isChild: true
title: Windows 安裝
anchor: windows_setup
---

## Windows 安裝 {#windows_setup_title}

在 Windows 下有多種安裝 PHP 的方式，你可以 [下載安裝檔][php-downloads] 並使用 `.msi` 的安裝檔。從 PHP 5.3.0 之後，該安裝檔將不再提供下載與支援。

如果是為了學習或者是本地端開發需求，從 PHP 5.4 之後，你可以使用內建的網頁伺服器，省去設定伺服器的麻煩。如果你想要也包含網頁伺服器以及 MySQL 的一鍵安裝包，那像是 [網頁平台安裝包][wpi] 的工具，如 [Zend Server CE][zsce]、[XAMPP][xampp]、[EasyPHP][easyphp] 和 [WAMP][wamp] 將會幫助您快速建立 Windows 開發環境。不過這些工具將會與正式執行環境會有些許差別，如果你是在 Windows 開發，而部署至 Linux 上的情況下，請小心。

如果你希望將網頁部署到 Windows 上，那 IIS7 將會提供最穩定且最佳的性能。你可以使用 「phpmanager][phpmanager] (IIS7 圖形化插件) 能讓你簡單設定並管理 PHP。IIS7 也有內建 FastCGI，你僅需將 PHP 設定為他的處理器即可。詳情請見 [dedicated area on iis.net][php-iis]。

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/en/products/server-ce/
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
