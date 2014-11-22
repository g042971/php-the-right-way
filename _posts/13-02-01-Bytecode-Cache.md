---
isChild: true
anchor: bytecode_cache
---

## Bytecode 快取 {#bytecode_cache_title}

當 PHP 檔案被執行時，會先被編碼成 bytecode ，（也被稱為 opcode ），然後才會執行這些 bytecode。如果 PHP 檔案沒有被修改，編成的 bytecode 也不會改變。這意味這編碼這一步驟是浪費 CPU 資源的。

這就是 Bytecode 快取的用途。它會將編好 bytecode 存在記憶體，並且在往後的呼叫中重複使用，以防止多餘的編譯。
設定 bytecode 快取僅需要花上幾分鐘，然後應用程式的執行速度就能得到飛快的提升。實在沒有理由不使用它。

在 PHP 5.5 之後，內建有 bytecode 快取， [OPcache](http://php.net/manual/en/book.opcache.php) ，更早的版本也可以使用。

其他流行的 bytecodes 快取：

* [APC](http://php.net/manual/en/book.apc.php) (PHP 5.4 and earlier)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (part of Zend Server package)
* [WinCache](http://www.iis.net/download/wincacheforphp) (extension for MS Windows Server)
