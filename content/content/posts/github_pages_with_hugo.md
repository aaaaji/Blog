---
title: "用Hugo、Github、Github Pages建立靜態網站"
draft: true
date: "2020-03-22"
tags: ["hugo","github"]
categories: ["技術"]
---

雖然在 Hugo 的[官方文件](https://gohugo.io/hosting-and-deployment/hosting-on-github/)有寫用 Github 作為 Host 應該怎麼把 Hugo 佈署上去，但實際執行時還是遇到了一點問題，為了避免忘記來做一下紀錄～

- Github Pages 提供了3種不同型態的頁面 User / Organization / Project Site ，雖然就目前看ㄧ

  - 用 User / Organization 為主頁一個帳號只能有**一個**

    顯示網址為 ```https://<user/organization>.github.io```

  - Project 頁面則能有數個，不過設定較為麻煩

    顯示網址為 ```https://<user>.github.io/<project-name>```

https://kaichu.io/2015/07/12/my-first-post/