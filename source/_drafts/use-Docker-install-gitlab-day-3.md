---
title: 為企業導入私有gitlab-鐵人賽Day 3
tags:
  - Docker
  - gitlab
  - 鐵人賽
---
## 開始安裝囉

我的環境為windows 10 專業版 所以先記錄著win10的操作方式，造著以下步驟走，應該不會有什麼大問題才是

並且，安裝的環境為不會關機的電腦，關機之後必須重新run container

附帶一提 windows 10 家用版是沒辦法安裝的 去升級吧

首先打開 控制台\所有控制台項目\程式和功能 開啟或關閉windows功能 將Hyper-V及容器打開

![docker-02](/images/docker-install-gitlab/docker-02.jpg)  

[下載 docker for windows ce 版本](https://docs.docker.com/docker-for-windows/install/)

使用windows的搜尋功能 尋找 power shell,並用系統管理員打開

或著你可以下載 cmdr 一個也挺方便的 cmd 工具 打開 poweshell 的 admin 模式

![docker-03](/images/docker-install-gitlab/docker-03.jpg)  

現在我們的docker已經架好 我們可以開始時做一些基本觀念了