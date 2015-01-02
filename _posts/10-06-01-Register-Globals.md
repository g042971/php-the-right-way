---
isChild: true
title: 註冊全域變數
anchor: register_globals
---

## 註冊全域變數 {#register_globals_title}

**注意:** 從 PHP 5.4.0 開始， `register_globals` 的設定已經被移除且不再被支援。如果你還保留這個設定，就意味著你該更新你的應用程式了。

當開啟 `register_globals` 設定時，`$_POST` ， `$_GET` 及 `$_REQUEST` 中的變數會自動註冊為全域變數，此時你的應用程式將無法辨識資料的原始來源，導致相當容易產生安全的漏洞。

例如: `$_GET['foo']` 會被註冊為全域變數 `$foo` ，他將會覆蓋掉程式中未定義的變數。
如果你的使用的 PHP < 5.4.0 ，請__再三確認__已經把 `register_globals` 給__關閉__。

* [在 PHP manual 中了解註冊 _globals](http://www.php.net/manual/en/security.globals.php)
