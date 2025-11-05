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
series: frontend
series_index: 1
---

**系列導覽：**

* « 本篇為系列首篇文章
* 下一篇：[不只 React，更勝 React：為什麼你的下一個專案應該考慮 Next.js？ »](/nextjs-why-framework)

---

### **前言：告別手動操作 DOM！**

前端開發經歷了多次典範轉移，而 **React** 無疑是其中最重要的推手。它帶領我們從一個需要一步步手動操作 DOM 的「命令式」時代 (想想 jQuery)，進入了一個「宣告式」、由狀態驅動的新世界。

過去，你得寫下詳細的指令去「修改」UI；有了 React，你只需要「描述」在特定狀態下，UI「應該長什麼樣子」。當資料改變時，React 會自動且高效率地去更新畫面。

而 **JSX** 語法正是這場「煉金術」的核心，它讓開發者能以直觀的 HTML 形式撰寫 UI，卻保有 JavaScript 的靈活性與強大功能。這篇文章，就是要帶你搞懂這一切魔法背後的核心觀念。

---

### **1. React 的本質：一個專注於「畫面」的函式庫**

React 的官方定義是「一個用來建構使用者介面的 JavaScript **函式庫 (Library)**」。它只專注處理 MVC 架構中的「V (View)」這一層。其核心解決思路非常直接：「**當狀態改變時，就重新渲染整個畫面**」。

你可能會想，這樣不會很慢嗎？為了解決這個瓶頸，React 引入了 **Virtual DOM (虛擬 DOM)** 的概念。這個機制大幅減少了對真實 DOM 的直接操作：

1.  **建立快照**：當元件的狀態改變時，React 會在記憶體中建立一個新的 Virtual DOM，這是一個輕量的 JavaScript 物件，描述了 UI 應該有的結構。
2.  **進行比對**：接著，React 會使用一種稱為 "Diff" 的演算法，去比對「新的」和「舊的」Virtual DOM 樹，精準找出真正改變的地方。
3.  **批次更新**：最後，React 會計算出最有效率的更新方式，只針對那些「有變動」的部分去更新真實的瀏覽器 DOM。

這個流程避免了整個頁面不必要的重繪，從而提升了應用的整體效能。

---

### **2. 萬物皆元件 (Component)：UI 的樂高積木**

React 應用是由一個個**元件 (Components)** 組成的。你可以把它想像成獨立的樂高積木，每個元件都封裝了自己的邏輯和外觀，一個完整的應用程式，就是由這些元件組合、巢狀堆疊而成。

> **💡 一個關鍵規則**
>
> React 元件的名稱**必須以大寫字母開頭** (例如 `MyButton`)，而標準的 HTML 標籤則必須是小寫 (例如 `button`)。這不只是個命名習慣，而是 JSX 區分「你的自訂元件」和「原生 HTML 元素」的核心機制。

---

### **3. JSX：讓你在 JavaScript 中寫 HTML 的橋樑**

**JSX (JavaScript XML)** 是一種語法擴充，它允許我們在 `.js` 檔案中直接撰寫類似 HTML 的標籤。你可以把 JSX 想像成一個內建了語法檢查器的 HTML，強迫你寫出乾淨、可預測的程式碼。

#### **JSX 的基本規則**

JSX 比原生 HTML 更嚴格，有幾個規則必須遵守：

* **所有標籤都必須閉合**：像是 `<br>` 這種單標籤，必須寫成自我閉合的形式 `<br />`。
* **只能回傳單一根元素**：如果要回傳多個元素，必須用一個父層元素（如 `<div>`）或用一個不產生額外 DOM 節點的 Fragment (`<>...</>`) 包起來。

#### **在 JSX 中嵌入 JavaScript**

想在 JSX 標籤中嵌入變數或執行 JavaScript 邏輯，只要用**大括號 `{}`** 包起來即可。這個語法讓我們能從 HTML 的世界「跳回」JavaScript。

```jsx
const user = {
  name: 'Hedy Lamarr',
  imageUrl: '[https://i.imgur.com/yXOvdOSs.jpg](https://i.imgur.com/yXOvdOSs.jpg)',
};

function Profile() {
  return (
    <>
      <h1>{user.name}</h1> {/* 顯示變數內容 */}
      <img
        className="avatar"
        src={user.imageUrl} // 屬性值來自 JavaScript 變數
        alt={'Photo of ' + user.name} // 屬性值可以包含複雜表達式
      />
    </>
  );
}
````

#### **內建安全機制**

React DOM 預設會對 JSX 中嵌入的所有內容進行**跳脫 (Escape)** 處理。這意味著所有 `{}` 裡的內容都會被自動淨化，能有效防止跨網站指令碼（XSS）攻擊。

> **⚠️ 注意安全**
>
> 在 `<a>` 連結標籤中直接放入使用者輸入的內容時，如果惡意使用者輸入 `javascript:alert()`，點擊連結仍可能觸發 XSS 攻擊。建議使用 `encodeURIComponent()` 語法將使用者輸入的 URL 轉換為轉義格式。

-----

### **4. 賦予元件生命：資料與邏輯的展現**

#### **設定樣式**

有兩種主要方式可以為 JSX 元素加上樣式：

  * **CSS Classes**：使用 `className` 屬性，它的作用就跟 HTML 的 `class` 一樣。
  * **Inline Styles**：使用 `style` 屬性，但它接收的不是字串，而是一個 JavaScript **物件**，且屬性名稱要用駝峰式命名 (camelCase)。

<!-- end list -->

```jsx
{% raw %}
// 使用 CSS class
<div className="card">...</div>

// 使用 Inline style
<h1 style={{ fontSize: '16px', color: 'blue' }}>Hello</h1>
{% endraw %}
```

> **為什麼是兩層大括號？**
>
> 外層的 {% raw %}`{}`{% endraw %} 是告訴 JSX「這裡要插入 JavaScript 囉！」，而內層的 {% raw %}`{}`{% endraw %} 則是 JavaScript 中建立「物件」的標準語法。

#### **條件渲染 (Conditional Rendering)**

React 沒有特殊的條件語法，而是直接使用標準的 JavaScript 來處理。常見的技巧有三種：

  * **使用 `if...else`**：最直白的方式，在 `return` 之外先用 `if` 判斷，再決定要渲染哪個元件。
  * **使用三元運算子 (`? :`)**：非常適合在 JSX 中處理簡單的 `if-else` 邏輯。
  * **使用邏輯 `&&` 運算子**：當你只想在「條件為真時才渲染某個東西」時，這是最方便的寫法。

<!-- end list -->

```jsx
{% raw %}
// 三元運算子
<div>{isLoggedIn ? <AdminPanel /> : <LoginForm />}</div>

// && 運算子
<div>{unreadMessages.length > 0 && <h2>您有 {unreadMessages.length} 則未讀訊息。</h2>}</div>
{% endraw %}
```

#### **渲染列表 (Rendering Lists)**

要根據一個陣列資料來渲染列表，我們通常使用 JavaScript 的 `array.map()` 方法。

```jsx
{% raw %}
const products = [
  { title: '高麗菜', id: 1 },
  { title: '大蒜', id: 2 },
  { title: '蘋果', id: 3 },
];

const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);
{% endraw %}
```

> **`key` 是什麼？為什麼重要？**
>
> `key` 是一個特殊的屬性，它幫助 React 識別列表中的哪些項目被更改、新增或刪除了。`key` 應該是穩定且在同層級元素中唯一的，通常我們會使用資料庫中的 ID。**為列表加上唯一的 `key` 是 React 的一項重要效能優化！**

-----

### **5. 打造互動體驗：事件與狀態 (State)**

#### **回應使用者事件**

你可以透過在元件內宣告**事件處理函式 (event handler)** 來回應點擊等使用者行為。要把處理函式綁定到元素上，只要把它當作一個 prop（例如 `onClick`）傳下去即可。

```jsx
function MyButton() {
  function handleClick() {
    alert('你點擊了我！');
  }

  return (
    <button onClick={handleClick}>
      點我
    </button>
  );
}
```

**注意**：我們是傳遞 `handleClick` 這個**函式本身**，而不是 `handleClick()` 這個**函式的執行結果**。

#### **用 State 記住資訊**

要讓元件「記住」某些資訊（例如計數器的值、表單的輸入內容），並在資訊改變時自動更新畫面，我們需要使用 **State (狀態)**。`useState` Hook 是在函式元件中加入 State 的主要方式。

1.  **引入 `useState`**：`import { useState } from 'react';`
2.  **宣告 State 變數**：在元件的頂層呼叫 `useState`。

<!-- end list -->

```jsx
{% raw %}
const [count, setCount] = useState(0);

function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1); // 呼叫更新函式
  }

  return (
    <button onClick={handleClick}>
      你點擊了 {count} 次
    </button>
  );
}
{% endraw %}
```

-----

### **6. 掌握資料流：Props vs. State**

`Props` 和 `State` 都是影響元件渲染的 JavaScript 物件，但它們的角色截然不同。

| 類別 | State (狀態) | Props (屬性) |
| :--- | :--- | :--- |
| **來源** | 在元件**內部**管理與宣告 | 從**父元件**傳遞進來 |
| **用途** | 元件內部的記憶體或資料儲存 | 像是函式的參數，用來設定元件和傳遞資料 |
| **可變性** | **可變的**。可透過 setter 函式改變 | **不可變的**。子元件不能直接修改自己的 props |
| **資料流** | 存在於元件內部，自我管理 | 單向資料流，從上 (父) 到下 (子) |

#### **共享資料：狀態提升 (Lifting State Up)**

想像一下，你有兩個元件需要同步顯示一個計數，如果 state 分別存在各自元件裡，它們就無法同步。要解決這個問題，React 的標準模式是「**狀態提升**」：

1.  找到需要共享 state 的所有元件的**最近共同父層**。
2.  將 state 和更新函式從子元件**移動到**這個父層元件中。
3.  父層現在是這個資料的「**唯一真實來源 (single source of truth)**」。
4.  透過 **props**，將 state 的值和更新函式傳遞給需要的子元件。

透過這個模式，我們就能讓多個子元件共享並同步同一個 state。

-----

### **總結：下一步**

這篇文章涵蓋了 React 的幾個重要基石：用 **Component** 打造可複用單元、用 **JSX** 撰寫宣告式 UI、用 **State** 管理內部資料，以及用 **Props** 傳遞數據。

然後你就可以開始React惹！

-----

**📚 系列下一篇：**

  * [不只 React，更勝 React：為什麼你的下一個專案應該考慮 Next.js？ »](/nextjs-why-framework)

<!-- end list -->