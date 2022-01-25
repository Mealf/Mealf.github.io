---
title: "vCenter 取消密碼到期"
date: 2022-01-14T23:36:48+08:00
draft: false

tags: [vCenter, configuration]
categories: [網路管理]
---

在登入vCenter後，上排常常出現密碼將要到期的提示，而且改完後過一段時間又再跳出來了，因此這次想要一勞永逸，不要讓他在強制我們修改密碼，順便做個紀錄。

- vCenter 版本: 6.7.0

## 介面位置
選擇上方的功能表 -> 系統管理 -> Single Sign On -> 組態

![](https://i.imgur.com/UsN2ovJ.png)

## 到期時間設定
可以看到原本密碼90天內需要更變一次，我們可以點選右上方的編輯

![](https://i.imgur.com/EDSQ4tB.png)

---

將存留時間上限的欄位填0，表示密碼不會到期

![](https://i.imgur.com/78B3x5V.png)

---

如此一來就不會再看到惱人的到期提醒了

## 參考資料
https://docs.vmware.com/tw/VMware-vSphere/6.7/com.vmware.psc.doc/GUID-B9C4409A-B053-40C3-96DE-232BB99AAA35.html

