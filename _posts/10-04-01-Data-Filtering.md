---
isChild: true
title: 資料過濾
anchor: data_filtering
---

## 資料過濾 {#data_filtering_title}

絕對（永遠）不要在 PHP 程式相信外部輸入。每次在程式中使用外部輸入時務必要過濾及驗證。 `filter_var` 及 `filter_input` 函式可以過濾文字及驗證文字的格式（例如 Email ）。

外部輸入可以是：由表單輸入的 `$_GET` 及 `$_POST` ，還有 `$_SERVER` 超級全域變數，以及來自 `fopen('php://input', 'r')` 的 Http 請求。切記，外部輸入並不限定是使用者從表單填入的資料。上傳及下載的檔案， Session 值及 Cookie 資料，以及第三方 Web 服務提供的資料，均是外部輸入。

當外部輸入被儲存、合併，或是下次讀取，他們依然是外部輸入。每次在程式中處理、輸出、串接或是引入資料時，試著問你自己這些資料都已經過濾，而且可以被信任。

根據資料使用的方式不同，就要進行不同的_過濾_。例如當外部輸入未經過濾輸出到 HTML 頁面上時，他就可以在你的網站上執行 HTML 及 JavaScript ！這就是我們所知道的跨網站指令碼（ Cross-site scripting ， 又稱為 XSS ），這是一個相當危險的攻擊手法。避免 XSS 的其中一個方式就是使用 `strip_tags` 函式來過濾外部輸入的所有 HTML 標籤，另外也可以使用 `htmlentities` 或 `htmlspecialchars` 函式將特定字元替換成 HTML 的實體符號。

另一個例子是傳遞給終端機執行的選項，這是相當危險的一件事（而且通常是個爛主意），不過你可以使用內建的 `escapeshellarg` 函式來過濾執行終端機的參數。

最後一個例子就是根據外部輸入從檔案系統載入檔案，該動作可以透過修檔案名稱或是路徑來攻擊。你必須移除外部輸入的 "/" ， "../" ， [空字元][6] 或是其他檔案路徑的字元，這樣就可以避免載入隱密，非公開或是敏感的檔案。

* [了解資料過濾][1]
* [了解 `filter_var`][4]
* [了解 `filter_input`][5]
* [了解空字元的處理][6]

### 淨化

淨化就是刪除（或是跳脫）外部輸入不合法或是不安全的字元。

例如，在將外部輸入的字元輸出至 HTML 或是插入到SQL的查詢前淨化外部輸入。當你使用 [PDO](#databases) 綁定參數時，他會為你淨化輸入的資料。

有時需要允許外部輸入包含某些安全的 HTML 標籤，並輸出至HTML頁面上。這是很難做到的，可以試著使用其他限制較嚴格的格式，例如 Markdown 或 BBCode 。如果真的窮途末路了，可以使用 [HTML Purifier][html-purifier] 來進行淨化。

[查閱淨化過濾][2]

### 驗證

驗證可以確保外部輸入是你所期望的資料。例如，你可能需要在處理註冊帳號時驗證Email，電話號碼或年齡。

[查閱驗證過濾][3]

[1]: http://www.php.net/manual/en/book.filter.php
[2]: http://www.php.net/manual/en/filter.filters.sanitize.php
[3]: http://www.php.net/manual/en/filter.filters.validate.php
[4]: http://php.net/manual/en/function.filter-var.php
[5]: http://www.php.net/manual/en/function.filter-input.php
[6]: http://php.net/manual/en/security.filesystem.nullbytes.php
[html-purifier]: http://htmlpurifier.org/
