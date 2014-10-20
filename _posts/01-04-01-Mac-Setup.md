---
isChild: true
anchor: mac_setup
---

## Mac 安裝  {#mac_setup_title}

OSX 會預載 PHP 在系統中，但版本略舊於最新的穩定版本。Lion 預載 PHP 5.3.6，Mountain Lion 是 5.3.10，而 Mavericks 則是 5.4.17，Yosemite 則是 5.5.9，但在 PHP 5.6 出來之後，這些往往是不夠的。

這裏有許多方式可以在 OS X 上安裝 PHP。

### 透過 Homebrew 安裝 PHP

[Homebrew](http://brew.sh/) 是一個強大的 OS X 專用套件管理系統，它可以讓您輕鬆地安裝 PHP 和各種擴充套件(extensions)。

[Homebrew PHP] 是一個包含與PHP相關的Formulae，能讓您透過 homebrew 安裝PHP。也就是說，你可以透過 `brew install`指令，安裝「php53」、「php54」、「php55」、或「php56」，並且透過修改你的路徑（ PATH ）變數去切換各種版本。

### 透過phpbrew 安裝 PHP

[phpbrew] 是一個專門安裝與管理多重 PHP 版本的工具。它在應用程式或專案 PHP 版本需求不同的情況下會非常有用，讓你不再需要使用虛擬機器處理這種情況。

### 編譯原始碼

另一個可以讓你控制你要安裝的PHP版本的選擇就是[自行編譯][mac-compile]。在這種方法，您必須先確認您是否已經透過「Apple Developer: Mac Dev Center」下載、安裝 Xcode 或是 ["Command Line Tools for XCode"]。

### 整合包 (All-in-One Installers)

上述所列的解決方式主要是針對 PHP 本身，並且不包含：像是 Apach 、 Nginx 、或是 SQL 伺服器。整合包像是 [MAMP][mamp-downloads] 和 [XAMPP][xampp] 會幫你安裝這些軟體並且將他們綁在一起，但是易於安裝的背後就是犧牲了一些彈性。

[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[mac-compile]: http://www.php.net/manual/en/install.macosx.compile.php
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer

["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[phpbrew]: https://github.com/phpbrew/phpbrew
[xampp]: http://www.apachefriends.org/en/xampp.html
