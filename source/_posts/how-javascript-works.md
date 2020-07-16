---
title: javascript 運作原理
date: 2018-09-14 
tags: 
  - javascript
  - javascript 運作原理
---

今天要來聊到究竟 js 在瀏覽器裡面是怎麼運作的，做一個粗淺的介紹

首先我們知道瀏覽器的引擎會轉成二進制( 010110101 之類的機碼 ) 存起來做為內存

在瀏覽器裡，引擎提供了 16 進制的方法給 js，執行之前就先把這個 16 進制的文件編譯成 2 進制文件來讓瀏覽器最為內存使用

而這個 16 進制的文件就可以撰寫非常多東西，如 UTF-8

那我們知道說，js 有三種資料結構，heap ( 堆 )、stack ( 棧 )、queue ( 佇列 )

heap 就是一個樹狀結構圖，概念上有點像 key & value 的感覺

快速地看過

<blockquote class="imgur-embed-pub" lang="en" data-id="a/uFnXVCZ"><a href="//imgur.com/uFnXVCZ"></a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

如果有興趣，可以參考[這篇](http://notepad.yehyeh.net/Content/Algorithm/Sort/Heap/Heap.php)

stack 你就把他想像成放乒乓球的盒子

![stack](/images/how-javascript-work/how-js-01.jpg)

我們從編號 1 開始放乒乓球，順序就如圖，然後取出的時候就是從 5 開始取出，順序就是 54321

實際上怎麼運作，我們等等會談

queue 就是像排隊點餐一樣

先來的先做，照順序做

再來，實際上瀏覽器只提供 heap 給 js 做使用，stack 與 queue 為 js 自行模擬而來

這也是為什麼說在 js 裡面，一切都為物件 ( object ) 的原因

簡單的介紹這三種資料結構後，我們開始講一段 function 是怎麼運作的

我們來看個簡單的 function 

```
function a(){
  var b = 5
  var c = 'Hi'
  var d = { e: 5 }
}
a()
```

## EC 階段


首先，js 會先創造全域執行環境 ( Global Execution Context )，以下簡稱 GEC

![how-js-02](/images/how-javascript-work/how-js-02.jpg)

再來，引擎看到 function a 被呼叫，ok 好，創造一個執行環境給他

![how-js-03](/images/how-javascript-work/how-js-03.jpg)

## VO 階段

這個 Fn EC 裡面建造了一些東西，這個階段我們稱為 VO ( 變數物件 Variable Object )

![how-js-04](/images/how-javascript-work/how-js-04.jpg)

這時候的內存是長這樣的 

![how-js-05](/images/how-javascript-work/how-js-05.jpg)

在 VO 階段，做了以下事情 ( 這邊我就直接照抄 [這篇，有興趣也可以更詳細的去讀](https://www.jianshu.com/p/edb2be5866eb) )

- 初始化作用域鏈

- 創建變數函數

- 創建參數物件 ( arguments object，傳進來的參數 )，檢查上下文，初始化其名字和值，以及建立引用物件的拷貝

- 掃描上下文中的函數聲明

- 為每一個掃描到的函數聲明在 VO 中創建一個屬性，命名為函數的名字，指向了存儲空間中的對應函數

- 如果函數名稱已經存在了，這個引用指針將被重寫為新的這一個

- 掃描上下文中的變數聲明

- 為每一個掃描到的變數聲明在 VO 中創建一個屬性，命名為變數的名字，初始化值為 undefined

- 如果變數名在記憶體中已經存在了，就跳過

- 決定上下文中 this 的指向

就我們現在可以看到的，我們知道我們的變數聲明已經建立並賦予 undefined 這個值，並且已經確定了 this

特別說一下，大家都知道 var 有提升 ( hosting ) 特性，原因就是在這裡，因為 var 為使用 function 做切割

## AO 階段

AO ( Activation Object ) 這時候做了以下事情

- 執行/解釋上下文中的 function ，為變數賦值

- code 按行執行

![how-js-06](/images/how-javascript-work/how-js-06.jpg)

這時候的內存是長這樣的 

![how-js-07](/images/how-javascript-work/how-js-07.jpg)

ok，我們可以了解到，其實 d 只是做一個指向 e 的地址

他並不是真的有一個 e:5

這個後面幾篇會講到這個會造成什麼影響。

再來，我們看再多一點 function 的

```

function a(){
  var aa = 5
  var bb = 'hi'
}
function b(){
  var ee = true
}
a()
b()

```

這時候就會 GEC => a EC => a VO => a AO => a Ec 離開 => b VO => b AO => b Ec 離開

![how-js-08](/images/how-javascript-work/how-js-08.jpg)

很公平的道理，對吧

### 來看看閉包

簡單的了解一下之後我們來看看閉包是怎麼回事

```

function a(){
  var n = 99
  function b(){
    n += 1
    console.log(n)
  }
  return b
}

var k = a();

k()

```

我們就一個一個寫

首先

var k 呼叫了 a()

a() 被呼叫，創造 a EC

執行 a VO

第一個先把大家都找出來

b : fn

n : undefined

this : window

下一個 a AO 階段，我們說按行執行

n : 99

b : 還是 fn

這時候，return b

b 被 k() 呼叫了 

好，他在 a EC 裡面又建立了 b EC

![how-js-09](/images/how-javascript-work/how-js-09.jpg)

b VO 開始

n : 99

this: window

b AO 開始

n += 1 => n = 100

console.log(n)

這樣子是不是比較好理解一點 ? 

js 沒有施展任何特別的魔法，

所有 js 的過程就是 GEC => EC => VO => AO => EC => VO => AO 不斷循環下去而已

要做練習建議多畫幾次，然後比對一下對不對

再來，回頭講記憶體，我們來看一個經典例子

```
let a = { g: 0 }

const b = a

a.n = { x: 3 }

a = { c: 8 }

console.log(a)
console.log(b)

```

請問 a 跟 b　分別是什麼

我們逐行來看，

首先 a 並不是真的等於 { g:0 }

也就是 a = 0X00fec3e 之類的

{ g:0 } 有自己的地址，然後 a 指向他而已

![how-js-10](/images/how-javascript-work/how-js-10.jpg)

const b = a 他是長這樣

![how-js-11](/images/how-javascript-work/how-js-11.jpg)

a.g = { x:3 }

通過 Dot 這個運算子去找到 g 改變 g 裡面的內容

![how-js-12](/images/how-javascript-work/how-js-12.jpg)

最後 a = { c: 8 }

指向一個新的記憶體 0X001cc3e 之類的，跟原本的地址斷開一切的牽連

![how-js-13](/images/how-javascript-work/how-js-13.jpg)

如此一來 a 跟 b 是什麼就很好懂了吧