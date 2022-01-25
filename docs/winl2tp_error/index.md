# Windows 10 L2TP 解決連線失敗


## 錯誤訊息
之前在 Windows 中都能正常的建立 L2TP 的連線，但最近要連線時就出現了以下的錯誤訊息

![](https://i.imgur.com/OxncDPO.png)

## 排錯過程
先使用 ubuntu 與 anandroid 環境建立 L2TP 連線，皆能成功連線，同時也在相同的網路環境中進行測試，排除了網路的影響，且在別的 OS 中也能連線，也排除了 Server 端的異常。
<br/><br/>
因此就針對 Windows 環境下去搜尋，在網路上看到許多修改機碼的方法，但說實話我對這些方法並不抱著多大的期待，畢竟在之前還能正常連線，在照著網路的步驟做之後，果然一點用也沒有。
<br/><br/>
最後在網路上看到一個月之內發布的[文章](https://www.reddit.com/r/sysadmin/comments/s1oqv8/kb5009543_january_11_2022_breaks_l2tp_vpn/)，裡面談到了這是因為 Windows 的更新(KB5009543) 所造成。
<br/><br/>
我就依據他更新的版本號進行搜尋，在[官方的支援文檔](https://support.microsoft.com/zh-tw/topic/2022-%E5%B9%B4-1-%E6%9C%88-11-%E6%97%A5-kb5009543-os-%E7%89%88%E6%9C%AC-19042-1466-19043-1466-%E5%92%8C-19044-1466-b763552f-73bd-435a-b220-fc3e0bc9765b)中，可以看到 "此更新中的已知問題"內，有 L2TP 相關的問題，並在 KB5010793 的更新中解決了，所以我們現在的目標就是要將我們的Windows更新到對應的版本
<br/><br/>
![](https://i.imgur.com/dJWCrC8.png)

## 解決方法
### Windows 10 更新到 KB5010793 版本

> 不想更新的話，退個版本也個是辦法。

對 Windows 進行更新，先更新到 21H2 版本

![](https://i.imgur.com/SjRqv09.png)

在更新成 21H2 後，先按一次檢查更新，他就能夠更新到 KB5010793 了

![](https://i.imgur.com/05XC1Vv.png)

在更新完成後，就能正常連線了

![](https://i.imgur.com/1nFKszB.png)

## 參考資料
- https://www.reddit.com/r/sysadmin/comments/s1oqv8/kb5009543_january_11_2022_breaks_l2tp_vpn/

- https://support.microsoft.com/zh-tw/topic/2022-%E5%B9%B4-1-%E6%9C%88-11-%E6%97%A5-kb5009543-os-%E7%89%88%E6%9C%AC-19042-1466-19043-1466-%E5%92%8C-19044-1466-b763552f-73bd-435a-b220-fc3e0bc9765b

- https://support.microsoft.com/zh-tw/topic/2022-%E5%B9%B4-1-%E6%9C%88-17-%E6%97%A5-kb5010793-os-%E7%89%88%E6%9C%AC-19042-1469-19043-1469-%E5%92%8C-19044-1469-%E5%B8%B6%E5%A4%96-f2d4f178-5b36-49cb-a6fd-4bf9857574f9

