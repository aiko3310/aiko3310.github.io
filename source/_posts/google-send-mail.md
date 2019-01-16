---
title: 使用google服務寄送網頁表單,發送郵件
date: 2019-01-11 15:48:50
tags: javascript, google
---

簡單說明如何使用google的服務進行驗證並發送網頁表單

#### 首先，準備好你的表單，前端驗證做好。

![code](/images/google-send-mail/code-01.png)

#### 然後我們去 Google 試算表建立表單

![google-send-mail](/images/google-send-mail/05.jpg)

完成之後到左上角檔案 > 發佈

![google-send-mail](/images/google-send-mail/13.jpg)


#### 選擇指令碼編輯器

![google-send-mail](/images/google-send-mail/06.jpg)

裡面會長這樣，在寫這篇文章的時間目前只有支援 ES5 的寫法，注意這邊 function 名稱要用 doGet，google 會去執行這個 function (這邊我不確定，不過我自己使用 doGet 才會過)

![google-send-mail](/images/google-send-mail/07.jpg)

為方便觀看，我會將裡面的 code 貼到別處，但這邊是在裡面做操作

![google-send-mail](/images/google-send-mail/code-03.png)

從 d/ 到 /edit 這中間就是你的id

![google-send-mail](/images/google-send-mail/08.jpg)

剩下完善 code 的部分這邊我直接用註解的方式來寫，至於為什麼是 j2 我們等等會看到

![google-send-mail](/images/google-send-mail/code-04.png)

#### 完成之後儲存，我們來發佈我們寫好的 function 吧

![google-send-mail](/images/google-send-mail/09.jpg)

##### 這兩個步驟每次更新function都要再來一次

![google-send-mail](/images/google-send-mail/10.jpg)

![google-send-mail](/images/google-send-mail/11.jpg)

接下來經過一連串的驗證之後會給你一串網址，存起來

回到我們的表單，這邊用最簡單的 jQuery 來取得，這邊就會用到我們前面命名的 j2 跟 j3，這邊可以自己去命名

![google-send-mail](/images/google-send-mail/code-05.png)

寫好就回到我們的 HTML 去輸入表單

![google-send-mail](/images/google-send-mail/12.jpg)

送出，回去表單看

![google-send-mail](/images/google-send-mail/14.jpg)

有值了，接下來回到信件裡收信

![google-send-mail](/images/google-send-mail/15.jpg)

也收到信了，那寄信加紀錄的功能就到這裡

[也可以參考此系列文章]('https://www.oxxostudio.tw/articles/201706/google-spreadsheet-1.html')

[完整Google script api]('https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet')