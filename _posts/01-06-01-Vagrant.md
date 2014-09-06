---
isChild: true
anchor: vagrant
---

## Vagrant {#vagrant_title}

如果你在開發應用與發布應用時使用不同的環境，那麼在正式上線時，可能會發生一些奇怪的錯誤。
在與一群團隊的開發者共同開發時，要保持每個環境同步，且所有的函式庫皆在同版本上，是最棘手的一件事情。

如果你是在 Windows 上開發，部署到 Linux（或非 Windows 平台），或者是團隊裡工作，你應該考慮使用虛擬機器。聽起來很麻煩，但使用 [Vagrant][vagrant] 你僅需幾個步驟就能設置好一個簡單的虛擬機器。再來需要手動設定基礎環境，或者你可以使用 “部署軟體” 如 [Puppet][puppet] 或 [Chef][chef] 來幫你完成這些事情。部署基礎環境是很好的做法保證大家的開發環境以相同的方式建立。並且省去你維護那些複雜的”安裝指令”。你也可以輕易地毀掉現有的基礎環境後再重新建立一個新的，這樣你就可以有一個全新的環境。

Vagrant 會建立共享資料夾，讓你可以在你的主機與虛擬機之間共享程式碼，也就是你可以在你的主機上創建與編輯檔案，然後在你的虛擬機器上面執行。


### 小助手

如果你想要取得一些 Vagrant 上的使用幫助的話，可以參考下面三個服務：

- [Rove][rove]: 提供你預先建立的 Vagrant 類型，其中包含 PHP 選項。使用 Chef 來部署。
- [Puphpet][puphpet]: 簡單的圖形化介面來設置虛擬機裡的 PHP 開發環境。**專注於 PHP 開發**，除了本地端虛擬機外，還可以部署到雲端服務上。部署工具使用 Puppet。
- [Protobox][protobox]: 構建在 Vagrant 上的服務層，提供網頁圖形介面去設置虛擬機器。通過單一 YAML 檔案去控制虛擬機的所有設定。
- [Phansible][phansible]: 為 PHP 專案提供一個簡單易用的介面，協助你產生 Ansible Playbooks。

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
[phansible]: http://phansible.com/
