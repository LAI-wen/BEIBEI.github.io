---
title: "前端的「煉金術」：JSX 如何將 HTML 變為 JavaScript 的黃金？"
date: 2024-01-01
categories:
  - 前端二三事
  - React 基礎
tags:
  - React
  - JSX
  - Component
  - State
  - Props
excerpt: "深入探討 React 的核心：從 JSX 如何將 HTML 轉化為可互動的 JavaScript 元素，到元件如何利用狀態 (State) 來管理自身數據。"
---

# 前言 

我竟然要寫系列文..


* **內容重點：**

* **React 的本質：** 作為建構使用者介面的 JavaScript 函式庫。

* **元件 (Component)：** UI 的最小單位，具備自身邏輯和外觀，可巢狀使用。React 元件是回傳 markup 的 JavaScript 函式。元件名稱必須以大寫字母開頭。

* **JSX 語法：** 寫 markup 的語法，是 HTML/XML 與 JavaScript 的結合。JSX 允許將 HTML 語法轉換為 JavaScript 函式以建立 React 元素。

* **嚴格性：** 標籤必須閉合 (如 `<br />`)，元件不能返回多個 JSX 標籤，需包裹在共享父元素中 (如 `<div>` 或 `<>`)。

* **嵌入 JavaScript：** 使用大括號 `{}` 將 JavaScript 變數或表達式嵌入到 JSX 中，包括屬性值。

* **自動轉義 (Automatic Escaping)：** JSX 能預防注入攻擊 (Injection Attacks)，提供轉義功能。但需注意 `<a>` 標籤中用戶輸入的內容可能導致 XSS 攻擊，建議使用 `encodeURIComponent()` 預防。

* **樣式 (Adding Styles)：** 使用 `className` 指定 CSS 類別。

* **顯示資料 (Displaying Data)：** 使用 `{}` 嵌入 JavaScript 變數以顯示資料。

* **條件渲染 (Conditional Rendering)：** 使用 JavaScript 的 `if` 語句、三元運算符 `? :` 或邏輯 `&&` 運算符。

* **渲染列表 (Rendering Lists)：** 使用陣列的 `map()` 函式將資料轉換為列表項目，每個項目應有獨特的 `key` 屬性。

* **響應事件 (Responding to Events)：** 在元件內部宣告事件處理函式，並將其作為 prop 傳遞給 JSX 元素 (例如 `onClick={handleClick}`)。

* **更新畫面與狀態 (Updating the Screen with State)：**

* 元件透過 **`useState` Hook** 「記住」資訊並顯示。

* `useState` 返回當前狀態 (`count`) 和更新狀態的函式 (`setCount`)。

* 每個元件實例擁有獨立的狀態。

* **Props 與 State 的不同：** 兩者皆為 JavaScript 物件，改變時會觸發畫面重新渲染。

* **State：** 在元件內部管理，只有該元件能透過 `setState` 變更。

* **Props：** 從外部傳入元件，類似函式參數，由父層單向傳遞給子層，子層不能直接修改。`children` 也是一種 props。

* **共享資料 (Sharing Data)：** 透過「提升狀態 (Lifting State Up)」將狀態從子元件移到共同的父元件，並將狀態和更新函式作為 props 傳遞下去。




* **[從 React 到 Next.js：為何需要一個框架？ &raquo;](/2024/01/02/nextjs-why-framework/)**
