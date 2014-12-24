---
isChild: true
title: 密碼雜湊
anchor: password_hashing
---

## 密碼雜湊 {#password_hashing_title}

每個人在建構 PHP 應用程式時終究會加入使用者登入的功能。使用者的帳號及密碼都會被儲存在資料庫，並在登入時使用該資料來驗證使用者。

在寫入資料前正確的 [_雜湊_][3] 他們的密碼是相當重要的一件事。使用單向雜湊函式處理密碼可以產生不可逆的密碼雜湊，而該雜湊會是一段固定長度的字串且無法逆向演算出密碼。這就代表你可以雜湊另一組密碼，並比較兩者是否來自於同一組密碼，而且你無法得知原始的密碼。如果你不將密碼雜湊，那麼當未經授權的第三者進入你的資料庫時，所有使用者的帳號資料將會一覽無遺。有些使用者可能（很不幸的）在別的服務也使用相同的密碼，所以務必要重視資訊安全的問題。

**使用 `password_hash` 來雜湊密碼**

`password_hash` 已經在 PHP 5.5 時加入。現在你可以使用目前 PHP 所支援的演算法中最強大的 BCrypt 。當然，未來支援更多的演算法時他就不見得會是最強的。 `password_compat` 函式庫的出現是為了提供 PHP >= 5.3.7 對舊版本的支援性。

在下面例子中，我們雜湊一組字串，然後和新的雜湊值做比對。因為我們使用的兩組字串是不同的（ 'secret-password' 與 'bad-password' ），所以理所當然的就登入失敗了。

{% highlight php %}
<?php
                      
require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    // Correct Password
} else {
    // Wrong password
}
{% endhighlight %}  



* [了解 `password_hash`] [1]
* [PHP >= 5.3.7 && < 5.5 的 `password_compat`] [2]
* [了解密碼學中的雜湊] [3]
* [PHP `password_hash` RFC] [4]

[1]: http://us2.php.net/manual/en/function.password-hash.php
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
