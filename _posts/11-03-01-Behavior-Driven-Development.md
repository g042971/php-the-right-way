---
isChild: true
anchor: behavior_driven_development
---

## 行為驅動開發 {#behavior_driven_development_title}

有兩種不同的行為驅動開發 (BDD)： SpecBDD 和 StoryBDD。 SpecBDD 專注於程式碼技術上的行為，而 StoryBDD 專注於商業或功能的行為和互動。 這兩種 BDD 都有 PHP 的框架。

採用 StoryBDD 時，你撰寫人可以閱讀的故事來描述應用程式的行為。 接著這些故事
可以作為應用程式的實際測試案例運行。 使用在 PHP 應用程式的 StoryBDD 框架
是 Behat，它受到 Ruby 的 [Cucumber](http://cukes.info/) 專案啟發並實作了 Gherkin DSL
來描述功能的行為。

採用 SpecBDD 時，你撰寫規格來描述實際的程式碼應該有什麼行為。 描述函式或方法應該有什麼行為，而不是測試函式或方法。 PHP 提供 PHPSpec 框架來達到這個目的。 這個框架受到 Ruby 的 [RSpec 專案](http://rspec.info/) 啟發。

### BDD 連結

* [Behat](http://behat.org/)，PHP 的 StoryBDD 框架，受到 Ruby 的 [Cucumber](http://cukes.info/) 專案啟發。
* [PHPSpec](http://www.phpspec.net/)，PHP 的 SpecBDD 框架，受到 Ruby 的 [RSpec](http://rspec.info/) 專案啟發。
* [Codeception](http://www.codeception.com) 是個使用 BDD 原則的全端測試框架。
