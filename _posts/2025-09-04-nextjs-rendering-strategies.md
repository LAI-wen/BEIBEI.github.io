---
title: "告別『空白頁面恐懼症』：Next.js 如何用多種渲染策略拯救你的 SEO？"
date: 2024-01-03
categories:
  - 前端二三事
  - Next.js 深入
  - 網頁渲染與效能
tags:
  - Next.js
  - SSR
  - SSG
  - CSR
  - Hydration
excerpt: "從客戶端渲染到伺服器端渲染，再到靜態網站生成，Next.js 提供多種策略以應對不同的效能與 SEO 挑戰。本文將深入剖析這些渲染魔法的運作原理。"
---

# 
• 內容重點：
    ◦ 為什麼需要多種渲染策略： 解決 CSR 帶來的 SEO、link preview、效能和使用者體驗問題。
    ◦ 客戶端渲染 (Client-side Rendering, CSR)：
        ▪ 伺服器回傳空 HTML 容器，瀏覽器執行 JavaScript 動態生成內容。
        ▪ 缺點：首次渲染費時，不利於 SEO。
    ◦ 伺服器端渲染 (Server-side Rendering, SSR)：
        ▪ 定義： 伺服器在每次收到請求時，建立好完整的 HTML 內容並發送給客戶端。
        ▪ 優點： 解決 SEO 問題，提升首次載入速度和使用者體驗。
        ▪ 水合 (Hydration)： SSR 輸出的 HTML 頁面就像被「脫水」過，客戶端載入 JavaScript 後會將事件處理器附加到已存在的 DOM 元素上，使頁面「活起來」，變得可互動。
        ▪ Next.js 中的 SSR： 每次請求都產生 HTML，可用 getServerSideProps() 獲取資料。適用於需要經常更新數據的頁面。
    ◦ 靜態網站生成 (Static Site Generation, SSG)：
        ▪ 在網頁打包 (build time) 時，由伺服器產生所有 HTML 內容。
        ▪ 優點：HTML 內容不變可搭配快取機制，速度極快，非常適合資料變動小的頁面 (如部落格)。
        ▪ Next.js 中的 SSG：可用 getStaticProps() 獲取資料。
    ◦ 增量式網站渲染 (Incremental Site Rendering, ISR)：
        ▪ 結合 SSG 和 SSR 的方式。可設定條件保存上次渲染結果，靜態檔案過期後觸發伺服器重新生成 HTML 檔案。
    ◦ 渲染策略比較： 分析不同策略的優缺點、適用場景和 Next.js 提供的函式
