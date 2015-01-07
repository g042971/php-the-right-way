---
isChild: true
title: 虛擬或自架伺服器
anchor: virtual_or_dedicated_servers
---

## 虛擬或自架伺服器 {#virtual_or_dedicated_servers_title}

如果你傾向自己管理系統，或是有興趣學習，虛擬或自己的伺服器環境可以讓你自己控制應用程式的上線環境。

### nginx 和 PHP-FPM

PHP 透過內建的 FastCGI Process Manager（ FPM ），可以和 [nginx](http://nginx.org) 搭配的很好（ nginx 是個輕量，高效能的伺服器）。它比 Apache 消耗更少的記憶體，且可以處理更多並行請求。這在沒有太多記憶體空間可用虛擬機器裡尤其重要。

* [更多關於 nginx](http://nginx.org)
* [更多關於 PHP-FPM](http://php.net/manual/en/install.fpm.php)
* [關於安全設定 nginx 和 PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache 和 PHP

PHP 和 Apache 的搭配使用已經蠻久了， Apache 可以進行高度客製並且有很多[模組](http://httpd.apache.org/docs/2.4/mod/) 可以擴展功能。對於共用伺服器，或想簡單設定 PHP 框架，以及使用開源程式像 WordPress，它是個流行的選擇。不幸的是， Apache 先天上要比 nginx 耗費更多資源並且無法同時應付更多的使用者。

Apache 有很多設定方式可以執行 PHP 。最普遍且最簡單的設定方式是使用 [prefork MPM](http://httpd.apache.org/docs/2.4/mod/prefork.html) 加上 mod_php5 。雖然它不是對記憶體最高效的方式，但它是最簡單使用的方式。如果你不想在伺服器系統管理方面太過深入，這可能是最好的選擇。注意如果你使用 mod_php5 ，你也必須使用 prefork MPM。

另外，如果你想讓 Apache 有更好的效能和更多的穩定性，那麼可以使用像是 nginx FPM 的 [worker MPM](http://httpd.apache.org/docs/2.4/mod/worker.html) 或是 [event MPM](http://httpd.apache.org/docs/2.4/mod/event.html) 搭配 mod_fastcgi 或 mod_fcgid 。兩者在設定上對於記憶體使用更為高效並且更快，但是設定上需要花更多功夫。

* [更多關於 Apache](http://httpd.apache.org/)
* [更多關於 Multi-Processing Modules](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [更多關於 mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [更多關於 mod_fcgid](http://httpd.apache.org/mod_fcgid/)
