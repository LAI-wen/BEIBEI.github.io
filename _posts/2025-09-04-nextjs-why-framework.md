---
title: "不只 React，更勝 React：為什麼你的下一個專案應該考慮 Next.js？"
date: 2024-01-02
categories:
  - 前端二三事
  - Next.js 深入
tags:
  - React
  - Next.js
  - SPA
  - Framework
excerpt: "React 專注於 UI 構建，但當面對 SEO、效能和路由等問題時，Next.js 提供了更全面的解決方案。這篇文章將帶你了解從函式庫到框架的必要性。"
---

##...
• 內容重點：
    ◦ React 是函式庫而非框架： React 專注於 UI 構建，但單獨使用時，路由、資料處理等需求需搭配其他函式庫。
    ◦ 單頁應用程式 (SPA) 的挑戰：
        ▪ SEO 問題： 內容由 JavaScript 動態生成，搜尋引擎爬蟲可能只看到空白 HTML。
        ▪ 首次載入效能： 初次載入需下載大量 JavaScript 檔案，導致首次渲染時間較長。
        ▪ 社群平台連結預覽 (Link Preview) 問題： meta 標籤在客戶端生成無效，社群平台 bot 通常不執行 JavaScript。
    ◦ Next.js 的誕生與優勢： 作為基於 React 的全端框架，旨在解決 React 作為函式庫的不足。
        ▪ 預渲染 (Pre-rendering)： 支援兩種形式的預渲染 (SSG 和 SSR)，有助於改善 SEO 和效能。
        ▪ 內建優化： 自動優化圖片、字體、JavaScript 載入 (包括延遲載入和快取處理)。
        ▪ 便捷的開發體驗： 例如檔案系統路由、內建 CSS/Sass 支援、API 路由、快速重新整理 (Fast Refresh)。
    ◦ 何時選擇 Next.js： 適合需要優化網頁效能與 SEO 的專案，如著陸頁面或產品展示頁面。
    ◦ Next.js 環境建置： 透過 npm install react react-dom next 安裝，並使用 npm run dev 運行開發伺服器。Next.js 會自動處理 Babel 編譯和 React 引入
