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


如果你有用 React 開發過專案，你大概也遇過這些問題：花了很多時間把酷炫的介面做出來了，但網站丟到 Google 就是搜尋不到；或是使用者抱怨第一次打開網頁怎麼那麼慢。

React 是一個超棒的 UI 函式庫，這點無庸置疑。但單獨用它來打造一個完整的「產品級」網站，就像是給你一顆超強引擎，卻要你自已找輪胎、底盤和外殼。

這篇文章，我們就來聊聊 Next.js 這個框架，看看它怎麼幫我們把「剩下的部分」都準備好，釋放 React 的真正潛力。

## 在開始之前，先搞懂：React 是「函式庫」，不是「框架」

要理解 Next.js 的好，得先釐清一件事：React 官方給自己的定位是「一個用來建立使用者介面的 JavaScript **函式庫** (Library)」。

「函式庫 (Library)」和「框架 (Framework)」差在哪？
講白話就是，函式庫只專心做好一件事。React 的專長就是專注於「View」層，提供強大的 UI 元件渲染能力

但一個完整的網站，光有畫面還不夠啊！我們還需要：

  * **路由 (Routing)**：怎麼切換頁面？
  * **資料處理與擷取 (Data Fetching)**：怎麼跟後端 API 拿資料？
  * **伺服器端邏輯 (Server-side Logic)**：有些事不能在使用者瀏覽器上做。
  * **應用程式狀態管理 (State Management)**
  * **打包工具**：Webpack、Babel 那些複雜的設定誰來弄？

![image](https://hackmd.io/_uploads/Hk8HSnn6xx.png)



只用 React，上面這些東西都得由開發者自己一個個找工具、自己設定、自己維護。雖然彈性，但真的很花時間，也很容易踩坑。

## 「純 React」開發的痛：SPA 模式下的三大硬傷

用 React 開發，最常見的模式就是 **「單頁式應用程式 (Single Page Application, SPA)」**。這種模式提供了類似桌面應用的流暢體驗，但其對 **「客戶端渲染 (Client-Side Rendering, CSR)」** 的依賴，天生就帶了幾個讓開發者很頭痛的問題：

1.  **SEO 幾乎是場災難**
    當 Google 爬蟲來看你的網站時，SPA 吐給它的是一個幾乎全空的 HTML。所有內容都要等 JavaScript 下載、執行完才會出現。很多爬蟲沒耐心等，結果就是你的網站內容 Google 根本看不到，搜尋排名自然上不去。
    ![image](https://hackmd.io/_uploads/r1tKShnaxe.png)


2.  **使用者等到天荒地老**
    使用者第一次進站時，瀏覽器得先下載一個超大的 JavaScript 包 (bundle)。下載完、執行完，畫面才姍姍來遲。這個「首次渲染延遲」對使用者體驗非常傷，也是 Google Core Web Vitals 很在意的指標。

3.  **社群分享連結超醜**
    你有沒有試過把 SPA 網站的連結貼到 Facebook 或 Slack？因為它們的爬蟲也不會等 JavaScript，所以抓不到你精心設定的標題、描述和預覽圖，最後只會顯示一個沒人想點的通用連結。

## Next.js 登場：那個幫你把車組好的「框架」


為了解決這些痛點，Next.js 應運而生。由 Vercel 團隊打造，它是一個全端 React **框架**，你可以把它想像成一個「原廠幫你改到好的 React」。它把 React 強大的 UI 引擎包起來，然後把路由、渲染、效能優化這些你原本要自己煩惱的事，全部都用最佳實踐幫你內建好了。

而且這不只是個人推薦——React 官方文件已明確表示："We recommend using a full-stack React framework like Next.js or Remix." 意味著它是打造嚴謹應用的首選途徑。

## Next.js 到底做了什麼來解決問題？

Next.js 透過幾個關鍵功能，直接命中 SPA 的要害。

### 一：預先渲染 (Pre-rendering)，讓 SEO 和效能起死回生

這是 Next.js 最核心的功能。它不再讓使用者的瀏覽器自己從零開始畫頁面，而是在伺服器端就先產生好完整的 HTML。這樣一來，不管是搜尋引擎還是使用者，收到的都是一個內容完整的 HTML 頁面，立即解決了 SEO 和首次載入緩慢的問題。

它主要有兩種模式：

  * **靜態網站生成 (Static Site Generation, SSG)：**：在專案**打包時**就把每個頁面的 HTML 做好。速度快到像飛一樣，最適合部落格、行銷網站這種內容不太變動的頁面。
  * **伺服器端渲染 (Server-Side Rendering, SSR)**：在**每一次請求**時，伺服器才即時產生 HTML。適合需要顯示最新資料或個人化內容的頁面，像是電商的會員中心。

![image](https://hackmd.io/_uploads/Hyy6B2npex.png)


### 二：內建各種自動優化，你什麼都不用做

Next.js 知道開發者懶得手動調校，所以內建了很多優化：

  * **圖片優化**：自動壓縮圖片、轉換成 WebP 格式，再也不用擔心上傳一張超大圖拖垮網站。
  * **字型與腳本優化：程式碼分割 (Code Splitting)**：自動把程式碼切成小塊，每個頁面只載入它需要的 JavaScript，大幅縮減首次載入的檔案大小。

### 三：開發體驗 (DX) 超級好

除了效能，Next.js 也讓開發過程變得很舒服：

  * **檔案就是路由**：想新增一個 `/about` 頁面？只要在 `pages` 或 `app` 資料夾裡新增一個 `about.js` 檔案就好。不用再裝 `react-router` 然後設定半天。
  * **API 路由**：你可以直接在 Next.js 專案裡寫後端 API！這讓開發全端應用變得異常簡單。
  * **快速刷新 (Fast Refresh)**：你改完程式碼存檔的瞬間，瀏覽器上的畫面就更新了，而且還不會洗掉你目前的狀態。
  * **整合工具鏈** ：內建對 CSS、Sass 和 CSS-in-JS 的支援。它在底層處理了 Babel 和 Webpack 等複雜的編譯與打包工具，讓你專注於撰寫應用程式邏輯。

## 那什麼時候該用 Next.js？

簡單來說，當你的專案**非常重視 SEO 和載入速度**時，選 Next.js 就對了。例如：

  * 公司的官方網站、產品介紹頁
  * 電子商務網站
  * 部落格、新聞媒體網站

## 上手 Next.js 有多簡單？

以前我們要設定 Webpack 和 Babel 可能要搞一整個下午，但 Next.js 只需要一行指令：

```bash
npx create-next-app@latest
```

就這樣，一個設定好所有開發工具、可以直接跑起來的專案就完成了。你馬上就能開始專心寫你的功能，而不是在搞環境設定。
![image](https://hackmd.io/_uploads/SJi0S22plx.png)

### 小結

React 是一顆頂級的引擎 (UI 函式庫)，但光有引擎沒辦法上路。Next.js 就是那台幫你把引擎、底盤、輪胎、方向盤都完美組裝好的跑車 (框架)。

它解決了純 React 在 SEO 和效能上的先天不足，同時又提供了極佳的開發體驗。別再自己拼裝車子了，直接開上這台為你打造好的 React 跑車，開始高效地打造你的下一個專案吧！



