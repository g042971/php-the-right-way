---
isChild: true
title: 日期與時間
anchor: date_and_time
---

## 日期與時間 {#date_and_time_title}

PHP 提供 DateTime 類別處理讀取、設定、比較和計算日期與時間。儘管 PHP 有許多日期與時間相關的函數，但是 DateTime 類別提供更佳的物件導向介面來處理常見的操作。並且能處理時區問題（礙於篇幅這裡並不多著墨）。

要使用 DateTime 類，可以使用工廠模式方法 `createFromFormat()` 來把原始的日期時間字串轉換成時間物件，或直接用 `new \DateTime` 取得當下日期時間的 DateTime 物件。可用 `format()` 方法轉換 DateTime 物件為字串作為輸出。

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = \DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('m/d/Y') . "\n";
{% endhighlight %}

DateTime 計算時間通常需要 DateInterval 類別，如 `add()` 和 `sub()` 方法，都是將時間差當作參數，而避免使用時間戳記來計算時間區間，這是因為當遇到日光節約或是時區問題都會造成錯誤。並且應該盡量使用 `diff()` 方法計算日期差，這會回傳一個新的 DateInterval 物件，非常容易作為輸出顯示使用。
{% highlight php %}
<?php
// create a copy of $start and add one month and 6 days
$end = clone $start;
$end->add(new \DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

DateTime 物件之間可以直接比較:
{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before end!\n";
}
{% endhighlight %}

最後一個範例來展示 DatePeriod 類，它用來迭代處理週期性的事件，傳入開始時間、結束時間以及時間區間，將會回傳此區間內的所有事件。
{% highlight php %}
<?php
// output all thursdays between $start and $end
$periodInterval = \DateInterval::createFromDateString('first thursday');
$periodIterator = new \DatePeriod($start, $periodInterval, $end, \DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // output each date in the period
    echo $date->format('m/d/Y') . ' ';
}
{% endhighlight %}

* [了解更多 DateTime][datetime]
* [了解更多 date formatting][dateformat] (允許的日期格式字串)

[datetime]: http://www.php.net/manual/book.datetime.php
[dateformat]: http://www.php.net/manual/function.date.php
