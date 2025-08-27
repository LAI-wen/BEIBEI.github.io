# 關於專案的資料夾結構

寫 react 的時候為了分資料夾糾結很久...

### Level 1：依「檔案類型」分組（適合小型專案）

```plaintext
src/
├── assets/         # 圖片、樣式等靜態資源
├── components/     # 所有元件
├── hooks/          # 自訂 Hook
├── services/       # API 呼叫
├── utils/          # 工具函式
├── App.tsx
└── index.tsx
```

✅ 優點：簡單明瞭  
⚠️ 缺點：功能邏輯分散，維護困難

---

###  Level 2：依「檔案類型 + 功能模組」分組（適合中型專案）

```plaintext
src/
├── components/
│   ├── auth/
│   ├── payment/
│   └── common/
├── hooks/
│   ├── auth/
│   ├── payment/
│   └── common/
├── services/
│   ├── authService.ts
│   └── paymentService.ts
├── utils/
│   └── formatDate.ts
```

✅ 優點：功能模組化，維護更容易  
⚠️ 缺點：仍有邏輯分散問題

---

### Level 3：依「功能模組」分組（適合大型專案）

```plaintext
src/
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── utils/
│   ├── payment/
│   └── dashboard/
├── shared/         # 共用元件、hook、工具
├── layouts/        # 頁面佈局
├── pages/          # 路由頁面
├── App.tsx
└── index.tsx
```

✅ 優點：高模組化、易於擴展與重構  
⚠️ 缺點：初期設定較複雜

---

可以參考這篇文章深入了解各層級的差異與實作方式：[Folder Structures in React Projects - DEV Community](https://dev.to/itswillt/folder-structures-in-react-projects-3dp8)  
或是看看這個 GitHub 範例：[Optimized React Folder Structure (2025)](https://github.com/meghint/optimized-react-folder-structure-2025)


