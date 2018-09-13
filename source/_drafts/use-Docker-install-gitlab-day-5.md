---
title: 為企業導入私有gitlab-鐵人賽Day 5
tags:
  - Docker
  - gitlab
  - 鐵人賽
---

今天我們要開始認識一些 Docker 的基本指令，那我們開始吧！

首先，請確認你的 Docker 已經裝好

我們這裡使用docker -v

![docker-04](/images/docker-install-gitlab/docker-04.jpg)  

確認後，我們要先找我們要來操作的軟體，也就是 Docker image

前面已經介紹我們有用到 docker hub 這個網站 

我們在上面搜尋 nginx 

![docker-05](/images/docker-install-gitlab/docker-05.jpg) 

可以看到很多搜尋結果

![docker-06](/images/docker-install-gitlab/docker-06.jpg) 

每一筆都是一個 image 

然後我們可以看到，藍色的為 image 的名稱

底下可以看到介紹 official 為官方版本

public 屬於自己做的

再來我們看右邊這三欄

左邊第一個為多少人按星星 (像 github 給星星一樣)

第二個為有多少人下載

第三個點進去之後可以看到該 image 的介紹文檔

那我們就把它下載下來

![docker-07](/images/docker-install-gitlab/docker-07.jpg) 

雖然前面有講過了，但如果你遇到這種問題該怎麼辦

![docker-08](/images/docker-install-gitlab/docker-08.jpg) 

這個就是這裡沒有打開

![docker-09](/images/docker-install-gitlab/docker-09.jpg) 

下載好之後，我們透過 docker images 指令來打開

![docker-10](/images/docker-install-gitlab/docker-10.jpg) 

就可以看到關於你所有 image 的資料了

再來，我們開始啟動我們的第一個 container 

使用的是 docker run 這個指令來去做操作

一些簡單的操作，因為我們用的是 nginx 我們可以介紹 

docker run -p [ 對外的port ] : [ 預設的port ] -d < image 名稱 >

-p 就是 port ( 埠號 ) 的意思 

-d 就是 detach ( 背後執行 ) 的意思

![docker-11](/images/docker-install-gitlab/docker-11.jpg) 

然後打開 localhost:8080，就可以看到歡迎畫面了，是不是很神速

![docker-12](/images/docker-install-gitlab/docker-12.jpg) 

然後我們透過 docker ps 或 docker ps -a (全部的意思) 來列出正在跑的 container

可以看到他的 container id 跟其他​有用的資訊

那我們現在把它停止掉

使用 docker stop < container 名稱 >，就把第一個 container id 給複製起來

![docker-13](/images/docker-install-gitlab/docker-13.jpg) 

這樣就 "停" 掉了，不過為什麼會有這個亂數呢 ?

因為 container 如果你沒有特別命名，系統會自董幫你取一個亂數名稱，雖然是省去命名的困擾，

不過在觀看上就很困難了，所以我們盡量都還是會去命名他

至於命名的方法，下一篇我們會開始講到