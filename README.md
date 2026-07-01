# 教學老師薪資管理系統

純靜態 HTML + Firebase Realtime Database，部署於 GitHub Pages。

---

## 檔案說明

```
salary-system/
├── index.html            ← 主程式（UI + 邏輯 + Firebase config 已內嵌）
├── database.rules.json   ← Realtime Database 安全規則
└── README.md
```

> `firebase-config.js` 已不需要，config 直接內嵌在 index.html。

---

## 第一步：設定 Realtime Database 安全規則

1. 前往 [https://console.firebase.google.com](https://console.firebase.google.com)
2. 選擇專案 **otto2-2026**
3. 左側選單 → **Realtime Database** → **規則** 頁籤
4. 將以下內容貼入並點「發布」：

```json
{
  "rules": {
    "salarySystem": {
      ".read": true,
      ".write": true
    }
  }
}
```

> 這樣只有 `salarySystem/` 路徑可讀寫，不影響你其他系統（如 `seat3/`、`salaryData/` 等）。

---

## 第二步：上傳到 GitHub

```bash
cd salary-system
git init
git add .
git commit -m "薪資系統初始版"
git remote add origin https://github.com/你的帳號/salary-system.git
git branch -M main
git push -u origin main
```

---

## 第三步：開啟 GitHub Pages

1. GitHub repository → **Settings** → **Pages**
2. Source：**Deploy from a branch** → Branch：**main** → **/ (root)** → Save
3. 等約 1 分鐘，取得網址：
   `https://你的帳號.github.io/salary-system/`
4. 分享給同事，所有人共用同一份 Firebase 資料

---

## 日後更新程式

```bash
git add .
git commit -m "說明修改內容"
git push
```

GitHub Pages 約 1 分鐘後自動更新。

---

## 資料結構（供參考）

資料存在 Firebase Realtime Database 的以下路徑：

```
salarySystem/
├── staff/          ← 人員設定（正職＋兼職）
└── months/         ← 每月統計＋超時時數
    ├── 2026-06/
    │   ├── data/   ← 從 xlsx 解析的教學人次
    │   └── overtime/ ← 各正職的教學時數
    └── 2026-07/
        └── ...
```

與你現有的 `seat3/`、`salaryData/` 路徑完全獨立，不會互相影響。
