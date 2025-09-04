---
title: "時間旅行者指南：回溯 SSR 的演變，從 PHP 到 React Server Components 的前端簡史"
date: 2024-01-04
categories:
  - 前端二三事
  - 前端歷史
tags:
  - SSR
  - Isomorphic
  - React
  - Next.js
excerpt: "伺服器端渲染的定義隨著時代不斷演變。本文將帶你回顧從傳統 PHP 渲染，到現代 React Server Components 的前端渲染技術發展歷程。"
---
### **📚 系列導覽：**

* **&laquo; 上一篇：[前端的『煉金術』：JSX 如何將 HTML 變為 JavaScript 的黃金？](/2024/01/01/frontend-alchemy-react/)**
#

內容重點：
    ◦ SSR 定義的演變與分歧： 討論「SSR」一詞在不同語境下的理解，以及為何傳統 PHP 渲染不常被稱為「SSR」。
    ◦ SPA 的興起： JavaScript (XMLHttpRequest/Ajax) 的成熟，以及 Backbone.js、AngularJS 等早期框架對 SPA 的推動。
    ◦ 早期 SPA 的 SSR 解決方案：
        ▪ 針對搜尋引擎渲染不同模板： 伺服器偵測 bot 時輸出專門的 HTML。優點是簡單，缺點是使用者與 bot 看到頁面不一致，可能影響 SEO 分數 (cloaking)。
        ▪ Pre-render (預渲染)： 伺服器使用 headless browser 執行 SPA 頁面並保存為 HTML，提供給搜尋引擎。使用者與 bot 看到的頁面更相似，但一般使用者仍經歷「空白頁面恐懼症」。
        ▪ 在伺服器渲染客戶端應用 (Server Render Client App)： 最理想的 SSR，首次渲染在伺服器，後續交由客戶端，客戶端與伺服器共用程式碼。解決 SEO 和使用者體驗問題，但實作較複雜，例如資料獲取。
    ◦ Isomorphic / Universal JavaScript： 「同一行程式碼既可以跑在客戶端又可以跑在伺服器」的概念，早期解決方案如 Airbnb 的 Rendr。
    ◦ 靜態生成 (Build-time Render)： 在建置時就預先渲染頁面，適用於內容不變的頁面 (例如 Next.js 的 SSG)。
    ◦ 現代與未來的前端渲染：
        ▪ Progressive Hydration (漸進式水合)： 分區塊進行水合，優先處理重要區塊。
        ▪ Selective Hydration (選擇性水合)： 提前渲染不需要互動的靜態區塊，避免不必要的水合。


### **📚 系列下一篇：**

* **[告別『空白頁面恐懼症』：Next.js 如何用多種渲染策略拯救你的 SEO？ &raquo;](/2024/01/03/nextjs-rendering-strategies/)**
        ▪ Islands Architecture (島嶼架構)： 將網頁視為不同小島組成，靜態頁面中只有需要互動的部分是獨立的小島。
        ▪ React Server Components： React 往此方向發展，區分伺服器與客戶端元件，將不需要狀態的元件直接在伺服器渲染
