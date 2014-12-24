---
isChild: true
title: 物件快取
anchor: object_caching
---

## 物件快取 {#object_caching_title}

快取程式碼裡面的物件常常是很有助益的，像是取得時很耗資源的資料，或是資料庫裡不太會變動的資料。你可以使用物件快取系統來保存這些資料以供日後快速取用。如果你在取出這些資料後可以儲存它們，那麼在往後的請求裡就可以直接使用這些資料，從而獲得效能的提升並減少資料庫的負擔。

有很多流行的 bytecode 快取同時也可以讓你儲存自定義資料，所以這或許是一個更好的理由去使用他們。 PCu ， XCache ， 和 WinCache 都有 APIs 可以將資料從 PHP 程式碼存到記憶體。

最常用的記憶體資料快取系統是 APCu 和 memcached 。 APCu 是儲存資料很好的選擇之一，他有很簡單的 API 讓你把資料加到記憶體快取，並且非常容易設置和使用。但是 APCu 的一個限制是只能用在其安裝的伺服器上。 另一方面， Memcached 可以作為獨立的服務，可以從網路存取，意味著你可以將資料可以存在 hyper-fast 資料儲存中心以及很多不同可以取得資料的系統。

注意如果在伺服器跑的是 PHP (Fast-)CGI ，每個 PHP 行程會有自己的快取，也就是說， APCu 的資料不會在工作行程（ worker processes ）間共享，因為它不會綁定到 PHP 的行程。

在單一網路環境內， APCu 的存取速度通常會表現的比 memcached 好，但是 memcached 可以很快速的進行擴展。如果你不打算用多伺服器架設你的應用程式，或是不需要 memcached 特有的功能， APCu 或許是快取資料的最好選擇。

APCu 的使用範例：

{% highlight php %}
<?php
// 卻認是否有稱作 'expensive_data' 的資料存在快取裡
$data = apc_fetch('expensive_data');
if ($data === false) {
    // 如果資料沒有被快取，把耗費昂貴成本取得的資料存起來供往後使用
    apc_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

注意在 PHP 5.5 之前， APC 同時提供了資料快取和 bytecode 快取。 APCu 是用在 PHP 5.5+ 資料快取的 APC 分支，因為 PHP 已經有內建的bytecode 快取了。

更多流行的資料快取系統：

* [APCu](https://github.com/krakjoe/apcu)
* [APC Functions](http://php.net/manual/en/ref.apc.php)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [WinCache Functions](http://www.php.net/manual/en/ref.wincache.php)
