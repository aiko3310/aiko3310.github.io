---
title: bootstrap4 modal 遇上 swiper
date: 2019-01-11 15:03:49
tags: other
---

小小的紀錄一下，有在 bootstrap4 的 modal 裡要放置任何的 slider 方法如下，這邊用 swiper 來做紀錄

```
const swiper = new Swiper('.swiper-container', {
    // Optional parameters
    loop: true,
    autoHeight: true,
    spaceBetween: 50,
    // Navigation arrows
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
  });
// bs4需要在他執行完的時候 slider 需製作一次
$('#your-modal').on('shown.bs.modal', function(){
  swiper.update();
})
```
