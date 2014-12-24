---
isChild: true
title: 錯誤報告 
anchor: error_reporting
---

## 錯誤報告 {#error_reporting_title}

錯誤報告可以用來找到應用程式的錯誤，但是也可能將應用程式的結構暴露在外，產生安全性的問題。為了防止這類問題的發生，你需要為你的開發環境及上線環境進行不同的設定。

### 開發環境

如果要在<strong>開發環境</strong>顯示錯誤訊息，你需要在 `php.ini` 中進行以下設定：

    display_errors = On
    display_startup_errors = On
    error_reporting = -1
    log_errors = On

> 設定為 `-1` 表示顯示任何的錯誤訊息，包括未來版本新增的錯誤類型或參數，和 PHP 5.4 中的 `E_ALL` 相同。 - [php.net](http://php.net/manual/function.error-reporting.php)

`E_STRICT` 錯誤參數是在 5.3.0 中加入的，並不包含在 `E_ALL` 中，但是在 5.4.0 開始，就被包含進 `E_ALL` 裡。這是什麼意思？
這就表示如果要在 PHP 5.3 中顯示所有的錯誤訊息，你必須將參數設定為 `-1` 或 `E_ALL | E_STRICT` 。

**各個 PHP 版本中顯示所有錯誤的設定**

* &lt; 5.3 `-1` 或 `E_ALL`
* &nbsp; 5.3 `-1` 或 `E_ALL | E_STRICT`
* &gt; 5.3 `-1` 或 `E_ALL`

### 線上環境

如果要在<strong>線上環境</strong>隱藏錯誤訊息，你需要在 `php.ini` 中進行以下設定：

    display_errors = Off
    display_startup_errors = Off
    error_reporting = E_ALL
    log_errors = On

在線上環境進行這個設定後，所有的錯誤訊息會紀錄至 Web 伺服器的錯誤日誌，但不會顯示至使用者畫面。欲了解更多的錯誤設定相關資訊，請參考 PHP 手冊：

* [錯誤報告](http://php.net/manual/errorfunc.configuration.php#ini.error-reporting)
* [顯示錯誤訊息](http://php.net/manual/errorfunc.configuration.php#ini.display-errors)
* [顯示啟動錯誤訊息](http://php.net/manual/errorfunc.configuration.php#ini.display-startup-errors)
* [錯誤日誌](http://php.net/manual/errorfunc.configuration.php#ini.log-errors)
