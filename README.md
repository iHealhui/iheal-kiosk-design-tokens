# iHeal Kiosk Design Tokens（iHeal 自助機 Design Tokens）

本 Repository 提供 **iHeal kiosk MVP** 的 Design Tokens，輸出為 **CSS Custom Properties（CSS 變數）**，並包含可直接套用的 **Typography 文字樣式 classes**（對應 Figma text styles）。

> 核心概念：`ref → sys → (component/typography)`  
> - `ref.css`：原子色票與尺寸基準（`--ref-*`）  
> - `sys.css`：語意層（`--sys-*`）全部 alias 指向 `--ref-*`  
> - `typography.css`：把 Figma 的文字 style 打包成 class（例如 `.body-base`, `.heading-strong`）

---

## 檔案結構（Files）

```
styles/
  ref.css
  sys.css
  typography.css
```

---

## 使用方式（Usage）

### 1) 引用字體（Google Fonts，MVP 版）
目前先採用引用方式（之後可視情況改為下載字體檔 self-host）。

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;600&family=Roboto:wght@400;500;600&display=swap" rel="stylesheet">
```

### 2) 引入 CSS 檔案（順序很重要）
> `sys.css` 依賴 `ref.css`，`typography.css` 依賴 `sys.css`

```html
<link rel="stylesheet" href="/styles/ref.css" />
<link rel="stylesheet" href="/styles/sys.css" />
<link rel="stylesheet" href="/styles/typography.css" />
```

---

## 前端怎麼用（How to use）

### A) 文字：直接套用 Typography classes（對應 Figma style）
```html
<h1 class="heading-strong">掛號完成</h1>
<p class="body-base">本機台不會變更或取消您的預約…</p>
<span class="label-small">請將健保卡插入讀卡機</span>
<button class="label-large-strong">確認並繼續</button>
```

### B) 元件樣式：使用 `--sys-*` tokens（顏色／圓角／spacing）
```css
.kiosk-button-primary {
  background: var(--sys-color-bg-primary-default);
  color: var(--sys-color-text-on-primary);
  border-radius: var(--sys-corner-md);
  padding: var(--sys-spacing-spacers-1rem) var(--sys-spacing-spacers-1-5rem);
}
```

---

## 設計／工程對應（Design ↔ Engineering）

### Token 層級
- **Figma Variables：ref** → CSS `--ref-*`
- **Figma Variables：sys** → CSS `--sys-*`（alias to `--ref-*`）
- **Figma Text Styles** → `typography.css` 中的 classes（`.body-base` 等）

### 命名規範
- 全部 **小寫**
- 使用 **dash `-`**
- 不含空格

---

## 注意事項（Notes）

### rem 基準
`ref.css` 內固定 `html { font-size: 16px; }`，用來固定 `1rem = 16px`，方便在 kiosk 上保持尺寸一致，也方便工程端用 rem。

### `corner-full`（全圓角）
`ref.css` 已將 `--ref-size-50pct` 設為 `999rem`（有單位），避免 CSS 判定為無效值。

---

## 版本管理建議（Versioning）

建議 tokens 有變更時打 Git tag / release，例如：
- `v0.1.0`
- `v0.1.1`

讓前端可以鎖版本、回溯差異。
