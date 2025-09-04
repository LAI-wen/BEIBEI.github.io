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


### **前端的「煉金術」：JSX 如何將 HTML 變為 JavaScript 的黃金？**

**系列導覽：**

  * **« 系列首篇文章**
  * **下一篇：[從 React 到 Next.js：為何需要一個框架？ »](https://www.google.com/search?q=https://your-blog.com/2024/01/02/nextjs-why-framework/)**

-----

### **前言：寫下系列文的開端**
我竟然要寫系列文..
前端網頁開發經歷了多次的典範轉移，其中 **React** 扮演了舉足輕重的角色。它不只是一個函式庫，更帶來了一套全新的思考模式，將前端開發從過去直接操作 DOM 的命令式做法，轉變為更為結構化、資料驅動的**宣告式開發**。而 **JSX** 語法正是這場「煉金術」的核心，它讓開發者能以直觀的 HTML 形式撰寫 UI，卻保有 JavaScript 的靈活性與強大功能。

本文將深入探討 React 的核心概念，解密 JSX 如何將 HTML 變為可互動的 JavaScript 元素，以及元件如何透過狀態（State）和屬性（Props）來管理自身數據和實現資料流動。

-----

### **React 的本質：JavaScript 函式庫**

React 是一個用於建構使用者介面（UI）的 **JavaScript 函式庫 (Library)**。嚴格來說，它並非一個完整的框架（Framework），但透過搭配其他相關函式庫，其所構成的生態系功能可媲美框架。

React 的誕生是為了解決傳統 JavaScript MVC（Model-View-Controller）架構在應用程式規模擴大時，複雜度呈指數級增長，導致開發與維護困難的問題。React 專注於處理 MVC 中的 **View（介面）** 部分。其核心解決思路是：「**當狀態改變時，直接重新渲染畫面**」。

為此，React 引入了 **虛擬 DOM (Virtual DOM)** 的概念。當資料狀態（data state）改變時，React 會比較這個模擬的 Virtual DOM，並透過特殊的 DOM Diff 演算法計算出實際需要更新的部分，最終只修改真實 DOM 中有差異的地方，從而有效減少渲染次數，提升效能並避免資源浪費。

-----

### **元件 (Component)：UI 的最小單位**

React 應用程式是由一個個**元件 (components)** 所組成。每個元件都是 UI 的一個獨立部分，擁有自己的邏輯和外觀。這些元件可以小到像一個按鈕，也可以大到構成一個完整的頁面。

開發 React 時，一個重要的思考點在於識別頁面中重複性高或相似的元素，並將它們封裝成獨立的元件。這種**元件化 (Component-based)** 的開發方式強調 UI 元件的**封裝性、共用性及擴展性**。

> **💡 重點提示：**
> React 元件本質上是回傳標記 (markup) 的 JavaScript 函式。為了區別於標準的 HTML 標籤，**React 元件的名稱必須以大寫字母開頭**。元件可以像積木一樣相互巢狀 (nest) 使用，形成複雜的 UI 結構。

-----

### **JSX 語法：將 HTML 轉化為 JavaScript 的橋樑**

#### **簡介**

**JSX (JavaScript XML)** 是一種語法擴充，它允許開發者在 JavaScript 程式碼中撰寫類似 HTML 的標記 (markup)。雖然 JSX 並非強制使用，但大多數 React 專案都因為其便利性而採用。React 透過底層的 Babel 機制，將這些 JSX 語法轉換成 JavaScript 函式，用來建立實際的 React 元素。你可以將 JSX 簡單理解為 HTML/XML 與 JavaScript 的結合。

```jsx
// 傳統 JavaScript 中操作 DOM
// document.getElementById('root').innerHTML = '<div>Hello React!</div>';

// React 中使用 JSX
const root = createRoot(document.getElementById('root'));
root.render(<div>hello React!</div>);
```

#### **嚴格性**

相較於 HTML，JSX 有更嚴格的語法規則：

  * **所有標籤都必須閉合**，即使是單一標籤，例如 `<br />` 而不是 `<br>`。
  * 一個 React 元件不能直接回傳多個 JSX 標籤。如果需要回傳多個平級元素，必須將它們包裹在一個共享的父元素中，例如 `<div>...</div>` 或一個**空的 `<>...</>` 片段**。
  * **JSX 本身沒有直接的迴圈概念或 `if-else` 判斷式。** 但你可以透過 JavaScript 語法來實現這些邏輯。

#### **嵌入 JavaScript**

JSX 最強大的功能之一是允許你在標記中輕鬆地嵌入 JavaScript 變數或表達式。這透過使用**大括號 `{}`** 來實現，它讓你「跳脫回 JavaScript」。

例如，你可以顯示一個變數的值：

```jsx
<h1>{user.name}</h1>
```

你也可以在 JSX 屬性中嵌入 JavaScript 值，此時需要使用大括號而不是引號。

```jsx
<img className="avatar" src={user.imageUrl} />
```

在大括號內，甚至可以放置更複雜的 JavaScript 表達式，例如字串串聯。

#### **自動轉義 (Automatic Escaping)**

JSX 語法具有**自動轉義 (automatic escaping)** 的特性，有助於預防**注入攻擊 (Injection Attacks)**。這表示 React 會自動將嵌入的內容轉換為字串，防止惡意腳本的執行。

> **⚠️ 注意：**
> 在某些特定情境下仍需注意安全問題。例如，在 `<a>` 連結標籤中直接放入使用者輸入的內容，如果惡意使用者輸入 `javascript:alert()`，點擊連結仍可能觸發 XSS 攻擊。為了防範這類問題，建議**不要在 `<a>` 標籤中直接放入使用者輸入的內容**，如果必須要放入，請使用 `encodeURIComponent()` 語法將字串轉換為轉義格式。

-----

### **使用 JSX 處理資料與邏輯**

#### **樣式 (Adding Styles)**

在 React 中，你可以使用 `className` 屬性來指定 CSS 類別，其功能與 HTML 的 `class` 屬性相同。

```jsx
<img className="avatar" />
```

此外，如果樣式需要依賴 JavaScript 變數動態生成，你可以使用 `style` 屬性，其值是一個 JavaScript 物件。

#### **顯示資料 (Displaying Data)**

如前所述，JSX 允許你透過大括號 `{}` 將 JavaScript 變數或表達式嵌入到標記中，從而將資料顯示給使用者。

```jsx
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

function Profile() {
  return (
    <>
      <h1>{user.name}</h1> {/* 顯示變數內容 */}
      <img
        className="avatar"
        src={user.imageUrl} // 屬性值來自 JavaScript 變數
        alt={'Photo of ' + user.name} // 屬性值可以包含複雜表達式
        style={{ width: user.imageSize, height: user.imageSize }} // 樣式也可動態設定
      />
    </>
  );
}
```

#### **條件渲染 (Conditional Rendering)**

在 React 中，並沒有專門的條件渲染語法，而是直接使用常規的 JavaScript 程式碼來實現條件邏輯。

**1. `if` 語句**：可以使用標準的 `if` 語句來條件性地包含 JSX。

```jsx
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return <div>{content}</div>;
```

**2. 三元運算符 `? :`**：如果你喜歡更緊湊的程式碼，可以在 JSX 內部直接使用三元運算符。

```jsx
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

**3. 邏輯 `&&` 運算符**：當你不需要 `else` 分支時，可以使用更簡短的邏輯 `&&` 語法。

```jsx
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

#### **渲染列表 (Rendering Lists)**

要渲染元件列表，你會依賴 JavaScript 的陣列方法，尤其是 **`map()` 函式**。

```jsx
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];

function ShoppingList() {
  const listItems = products.map(product =>
    <li key={product.id}> {/* 每個列表項目都需要一個唯一的 `key` 屬性 */}
      {product.title}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}
```

值得注意的是，列表中的每個項目都必須包含一個 **`key` 屬性**。這個 `key` 應該是一個字串或數字，並且在同級元素中是唯一的。

-----

### **與使用者互動：事件與狀態**

#### **響應事件 (Responding to Events)**

在 React 中，你可以透過在元件內部宣告**事件處理函式 (event handler functions)** 來響應使用者互動事件。

```jsx
function MyButton() {
  function handleClick() { // 宣告事件處理函式
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}> {/* 將函式作為 prop 傳遞給 JSX 元素 */}
      Click me
    </button>
  );
}
```

**關鍵點**在於 `onClick={handleClick}` **沒有括號**。這表示你不是立即呼叫 `handleClick` 函式，而是將其作為一個函式物件傳遞下去。

#### **更新畫面與狀態 (Updating the Screen with State)**

為了讓元件能夠「記住」某些資訊並在需要時更新顯示，你需要為元件添加**狀態 (State)**。

1.  **導入 `useState` Hook**：首先，從 React 導入這個內建的 Hook。

    ```jsx
    import { useState } from 'react';
    ```

2.  **宣告狀態變數**：`useState()` 函式會回傳一個包含兩個元素的陣列：

      * **當前狀態的值** (例如 `count`)。
      * **更新狀態的函式** (例如 `setCount`)。

    <!-- end list -->

    ```jsx
    function MyButton() {
      const [count, setCount] = useState(0);
      // ...
    }
    ```

3.  **更新狀態**：當你想要改變狀態時，呼叫 `setCount()` 函式並傳入新的值。

    ```jsx
    function MyButton() {
      const [count, setCount] = useState(0);
      function handleClick() {
        setCount(count + 1);
      }
      return (
        <button onClick={handleClick}>
          Clicked {count} times
        </button>
      );
    }
    ```

    每當狀態改變，React 都會自動重新渲染頁面。

-----

### **Props 與 State 的不同**

**State 和 Props** 都是 JavaScript 物件，用於控制元件的資料，改變時都會觸發畫面重新渲染。然而，它們在來源和管理方式上有本質的區別：

| 類別 | State（狀態） | Props（屬性） |
| :--- | :--- | :--- |
| **來源** | 在元件**內部**被管理。 | 從**外部父元件**傳入。 |
| **作用** | 類似元件本身的「記憶」。 | 類似函式呼叫時傳遞的參數。 |
| **可變性** | 只有該元件能透過 `setState` 變更。 | 子元件**不能**直接修改，僅能讀取。 |
| **資料流向**| 自身管理。 | 由上往下單向傳遞。 |

#### **共享資料 (Sharing Data)：提升狀態 (Lifting State Up)**

如果多個子元件需要共享相同的資料，你需要將狀態從個別的子元件移動到包含所有這些子元件的最近的共同父元件。這個模式稱為「**提升狀態 (Lifting State Up)**」。

這樣一來，父元件就成為了共享狀態的「真相來源 (source of truth)」。父元件將這個共用的狀態和更新狀態的函式作為 props 傳遞給每一個需要這些資料的子元件。

-----

### **📚 系列下一篇：**


* **[從 React 到 Next.js：為何需要一個框架？ &raquo;](/2024/01/02/nextjs-why-framework/)**
