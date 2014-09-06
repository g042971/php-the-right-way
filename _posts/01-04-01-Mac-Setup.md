---
isChild: true
anchor: mac_setup
---

## Mac 安裝  {#mac_setup_title}

OSX 會預載 PHP 在系統中，但版本略舊於最新的穩定版本。Lion 預載 PHP 5.3.6，Mountain Lion 是 5.3.10，而 Mavericks 則是 5.4.17。

要更新 OSX 上的 PHP 你可以透過一系列 Mac [套件管理器][mac-package-managers]，推薦使用 [php-osx by Liip][php-osx-downloads]。

你也可以 [自行編譯][mac-compile]，如果你要這樣做，你必須安裝 Xcode 或者是 Apple 提供的 [“Xcode 命令列工具”][apple-developer] 作為替代，他們都可以在 Apple 的 Mac 開發者中心下載。

如果想要安裝包含 PHP、Apache、MySQL 的一鍵安裝包，可以試試 [MAMP][mamp-downloads] 或 [XAMPP][xampp]，他們都有不錯的圖形化管理工具。

[mac-package-managers]: http://www.php.net/manual/en/install.macosx.packages.php
[mac-compile]: http://www.php.net/manual/en/install.macosx.compile.php
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
[apple-developer]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/index.html
[php-osx-downloads]: http://php-osx.liip.ch/
[xampp]: http://www.apachefriends.org/en/xampp.html
