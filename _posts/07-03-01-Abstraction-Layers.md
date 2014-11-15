---
isChild: true
title: 抽象層
anchor: databases_abstraction_layers
---

## 抽象層 {#databases_abstraction_layers_title}

許多的framework提供他們自己的抽象層，有些會建立在PDO的上層，這些抽象層常常會藉由將你的資料庫請求包裝起來，以模擬一些非你正在使用的資料庫所擁有的特色，提供你一個真正的資料庫抽象，而不是僅僅是PDO所提供的連線抽象。這些抽象層當然地會造成一些小小的效能負擔，但是你如果你正在建立一個應用程式需要與MySQL, PostgreSQL和SQLite的時候，這些代價來交換程式碼的乾淨是值得的。

有些抽象層是建立在 [PSR-0][psr0] 或 [PSR-4][psr4] 的命名空間標準，所以可以被安裝在任何你喜歡的應用程式裡。

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]

[1]: http://www.php.net/manual/en/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/index.html#zend-db
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/

[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
