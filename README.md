# Anime.js

Anime.js 是一個輕量級的 JavaScript 動畫庫，適用於動畫 CSS 屬性、SVG、DOM 屬性和 JavaScript 物件。它提供了一個簡單而強大的 API，讓您可以輕鬆創建流暢的動畫效果，適合初學者和專業開發者。

## 目錄

- [簡介](#簡介)
- [安裝](#安裝)
  - [CDN](#cdn)
  - [npm](#npm)
- [快速入門](#快速入門)
- [核心概念](#核心概念)
  - [目標](#目標)
  - [屬性](#屬性)
  - [選項](#選項)
- [動畫類型](#動畫類型)
  - [CSS 屬性動畫](#css-屬性動畫)
  - [SVG 動畫](#svg-動畫)
  - [DOM 屬性動畫](#dom-屬性動畫)
  - [JavaScript 物件動畫](#javascript-物件動畫)
- [高級功能](#高級功能)
  - [時間軸](#時間軸)
  - [交錯動畫](#交錯動畫)
  - [路徑動畫](#路徑動畫)
- [回調和事件](#回調和事件)
- [控制動畫](#控制動畫)
- [緩動函數](#緩動函數)
- [SVG 動畫](#svg-動畫-1)
- [性能考慮](#性能考慮)
- [故障排除](#故障排除)
- [資源](#資源)

## 簡介

Anime.js 是一個快速、輕量級的 JavaScript 動畫庫，專為創建流暢的網頁動畫而設計。它支援動畫 CSS 屬性、SVG、DOM 屬性和 JavaScript 物件，提供了一個簡單而強大的 API，讓您能夠輕鬆實現複雜的動畫效果。

## 安裝

### CDN

您可以通過 CDN 直接在 HTML 文件中導入 Anime.js。將以下 `<script>` 標籤添加到您的 HTML 文件：

```html
<script src="https://cdn.jsdelivr.net/npm/animejs@latest/lib/anime.min.js"></script>
```

### npm

如果您使用 npm，可以通過以下命令安裝 Anime.js：

```bash
npm install animejs
```

然後在您的 JavaScript 文件中導入：

```javascript
import anime from "animejs/lib/anime.es.js";
```

## 快速入門

以下是一個簡單的動畫範例，展示如何使用 Anime.js 移動一個 div 元素：

```html
<div class="box" style="width: 100px; height: 100px; background: red;"></div>

<script>
  anime({
    targets: ".box",
    translateX: 250,
    duration: 1000,
    easing: "easeInOutQuad",
  });
</script>
```

這個範例將 `.box` 元素向右移動 250 像素，動畫持續 1 秒，並使用 `easeInOutQuad` 緩動函數。

## 核心概念

### 目標

動畫的目標可以是以下之一：

- **CSS 選擇器**：例如 `'.class'`、`'#id'`
- **DOM 元素**：例如 `document.querySelector('.class')`
- **JavaScript 物件**：例如 `{ prop: 0 }`
- **陣列**：例如 `[element1, element2]`

### 屬性

您可以動畫多種屬性，包括：

- **CSS 屬性**：如 `translateX`、`scale`、`opacity`
- **SVG 屬性**：如 `points`、`path`
- **DOM 屬性**：如 `scrollTop`、`value`
- **JavaScript 物件屬性**：如 `obj.prop`

### 選項

動畫選項用於配置動畫行為，常見選項包括：

- `duration`：動畫持續時間（毫秒）
- `delay`：動畫延遲（毫秒）
- `easing`：緩動函數（如 `'linear'`、`'easeInOutQuad'`）
- `loop`：是否循環動畫（`true` 或次數）
- `direction`：動畫方向（`'normal'`、`'reverse'`、`'alternate'`）

## 動畫類型

### CSS 屬性動畫

動畫 CSS 屬性，如 `transform`、`opacity` 等：

```javascript
anime({
  targets: ".box",
  translateX: 250,
  rotate: "1turn",
  scale: 1.5,
  opacity: 0.5,
  duration: 1000,
});
```

### SVG 動畫

動畫 SVG 屬性，如 `points`、`path`：

```javascript
anime({
  targets: "#mySVG path",
  d: "M10 10 H 90 V 90 H 10 Z",
  easing: "easeInOutQuad",
  duration: 2000,
});
```

### DOM 屬性動畫

動畫 DOM 屬性，如 `scrollTop`：

```javascript
anime({
  targets: document.documentElement,
  scrollTop: 1000,
  duration: 2000,
  easing: "easeInOutQuad",
});
```

### JavaScript 物件動畫

動畫 JavaScript 物件的屬性：

```javascript
const obj = { prop: 0 };
anime({
  targets: obj,
  prop: 100,
  easing: "linear",
  update: function () {
    console.log(obj.prop);
  },
});
```

## 高級功能

### 時間軸

使用時間軸創建動畫序列或並行動畫：

```javascript
const tl = anime.timeline({
  easing: "easeOutExpo",
  duration: 750,
});

tl.add({
  targets: ".box1",
  translateX: 250,
}).add(
  {
    targets: ".box2",
    translateX: 250,
  },
  "-=500"
); // 與上一個動畫重疊 500ms
```

### 交錯動畫

為多個目標創建延遲動畫：

```javascript
anime({
  targets: ".staggering-grid div",
  scale: [
    { value: 0.1, easing: "easeOutSine", duration: 500 },
    { value: 1, easing: "easeInOutQuad", duration: 1200 },
  ],
  delay: anime.stagger(200, { grid: [14, 5], from: "center" }),
});
```

### 路徑動畫

沿著 SVG 路徑動畫元素：

```javascript
const path = anime.path("#motionPath path");

anime({
  targets: ".box",
  translateX: path("x"),
  translateY: path("y"),
  rotate: path("angle"),
  easing: "linear",
  duration: 2000,
  loop: true,
});
```

## 回調和事件

Anime.js 提供多種回調函數：

- `begin`：動畫開始時調用
- `update`：動畫更新時調用
- `complete`：動畫完成時調用

範例：

```javascript
anime({
  targets: ".box",
  translateX: 250,
  begin: function (anim) {
    console.log("動畫開始");
  },
  update: function (anim) {
    console.log("動畫更新");
  },
  complete: function (anim) {
    console.log("動畫完成");
  },
});
```

## 控制動畫

您可以控制動畫的播放、暫停等：

```javascript
const animation = anime({
  targets: ".box",
  translateX: 250,
  autoplay: false, // 不自動播放
});

// 播放動畫
animation.play();

// 暫停動畫
animation.pause();

// 尋找動畫的特定時間
animation.seek(500); // 尋找到 500ms

// 重新開始動畫
animation.restart();

// 反轉動畫
animation.reverse();
```

## 緩動函數

Anime.js 支援多種內置緩動函數，如 `'linear'`、`'easeInQuad'` 等。您也可以自定義緩動函數：

```javascript
anime({
  targets: ".box",
  translateX: 250,
  easing: function (el, i, total) {
    return function (t) {
      return Math.pow(t, 2); // 自定義二次方緩動
    };
  },
});
```

## SVG 動畫

Anime.js 特別適合動畫 SVG 元素，例如動畫屬性、路徑和形狀：

```javascript
anime({
  targets: "#mySVG",
  points: [
    { value: "0,0 100,0 100,100 0,100" },
    { value: "50,50 150,50 150,150 50,150" },
  ],
  easing: "easeInOutQuad",
  duration: 2000,
  loop: true,
});
```

## 性能考慮

- 使用 `requestAnimationFrame` 確保動畫平滑。
- 避免在動畫中進行複雜的 DOM 操作。
- 對於大量動畫，考慮分批處理或使用 Web Workers。

## 故障排除

- **動畫不運行**：檢查目標是否正確、屬性是否支援動畫。
- **動畫閃爍**：確保使用適當的緩動函數和持續時間。
- **性能問題**：減少同時運行的動畫數量，優化代碼。

## 資源

- [官方文檔](https://animejs.com/documentation/)
- [GitHub 倉庫](https://github.com/juliangarnier/anime)
- [社區論壇](https://github.com/juliangarnier/anime/discussions)

---

這個 README.md 文件提供了 Anime.js 的全面介紹和使用說明，涵蓋所有主要功能，並附有清晰的代碼範例。無論您是初學者還是進階使用者，都可以通過此文件快速上手並創建出色的動畫效果！
