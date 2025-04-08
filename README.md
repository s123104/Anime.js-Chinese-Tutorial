# Anime.js 使用指南 [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[![繁體中文](https://img.shields.io/badge/繁體中文-點擊查看-orange)](README.md)
[![简体中文](https://img.shields.io/badge/简体中文-点击查看-orange)](README-zh.md)

這是一個針對 Anime.js 的全面使用指南，Anime.js 是一個輕量級的 JavaScript 動畫庫，適用於動畫 CSS 屬性、SVG、DOM 屬性和 JavaScript 物件。本指南涵蓋安裝、核心概念、動畫類型、高級功能及實用資源，幫助您快速上手並創建流暢的動畫效果。

- [什麼是 Anime.js？](#什麼是-animejs)
- [安裝](#安裝)
- [快速入門](#快速入門)
- [核心概念](#核心概念)
- [動畫類型](#動畫類型)
- [高級功能](#高級功能)
- [控制動畫](#控制動畫)
- [緩動函數](#緩動函數)
- [SVG 動畫](#svg-動畫)
- [性能考慮](#性能考慮)
- [故障排除](#故障排除)
- [資源](#資源)

## 什麼是 Anime.js？

Anime.js 是一個快速、輕量級的 JavaScript 動畫庫，專為創建流暢的網頁動畫而設計。它支援動畫 CSS 屬性、SVG、DOM 屬性和 JavaScript 物件，提供簡單而強大的 API，讓您輕鬆實現複雜的動畫效果。無論是初學者還是專業開發者，Anime.js 都能滿足您的需求。

## 安裝

### CDN

將以下 `<script>` 標籤添加到您的 HTML 文件中，即可通過 CDN 導入 Anime.js：

```html
<script src="https://cdn.jsdelivr.net/npm/animejs@latest/lib/anime.min.js"></script>
```

### npm

使用 npm 安裝 Anime.js：

```bash
npm install animejs
```

然後在 JavaScript 文件中導入：

```javascript
import anime from "animejs/lib/anime.es.js";
```

## 快速入門

以下是一個簡單範例，展示如何使用 Anime.js 移動一個 div 元素：

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

此範例將 `.box` 元素向右移動 250 像素，動畫持續 1 秒，使用 `easeInOutQuad` 緩動函數。

## 核心概念

### 目標

動畫的目標可以是：

- **CSS 選擇器**：如 `'.class'`、`'#id'`
- **DOM 元素**：如 `document.querySelector('.class')`
- **JavaScript 物件**：如 `{ prop: 0 }`
- **陣列**：如 `[element1, element2]`

### 屬性

可動畫的屬性包括：

- **CSS 屬性**：如 `translateX`、`scale`、`opacity`
- **SVG 屬性**：如 `points`、`path`
- **DOM 屬性**：如 `scrollTop`、`value`
- **JavaScript 物件屬性**：如 `obj.prop`

### 選項

常見動畫選項：

- `duration`：持續時間（毫秒）
- `delay`：延遲（毫秒）
- `easing`：緩動函數（如 `'linear'`、`'easeInOutQuad'`）
- `loop`：是否循環（`true` 或次數）
- `direction`：方向（`'normal'`、`'reverse'`、`'alternate'`）

## 動畫類型

### CSS 屬性動畫

動畫 CSS 屬性：

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

動畫 SVG 屬性：

```javascript
anime({
  targets: "#mySVG path",
  d: "M10 10 H 90 V 90 H 10 Z",
  easing: "easeInOutQuad",
  duration: 2000,
});
```

### DOM 屬性動畫

動畫 DOM 屬性：

```javascript
anime({
  targets: document.documentElement,
  scrollTop: 1000,
  duration: 2000,
  easing: "easeInOutQuad",
});
```

### JavaScript 物件動畫

動畫 JavaScript 物件：

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

使用時間軸創建序列或並行動畫：

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

沿 SVG 路徑動畫元素：

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

## 控制動畫

控制動畫播放：

```javascript
const animation = anime({
  targets: ".box",
  translateX: 250,
  autoplay: false,
});

animation.play(); // 播放
animation.pause(); // 暫停
animation.seek(500); // 尋找至 500ms
animation.restart(); // 重新開始
animation.reverse(); // 反轉
```

## 緩動函數

支援多種緩動函數，或自定義：

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

動畫 SVG 元素：

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
- 避免複雜 DOM 操作。
- 大量動畫時，考慮分批處理或使用 Web Workers。

## 故障排除

- **動畫不運行**：檢查目標和屬性是否正確。
- **動畫閃爍**：調整緩動函數或持續時間。
- **性能問題**：減少同時運行的動畫數量。

## 資源

- [官方文檔](https://animejs.com/documentation/)
- [GitHub 倉庫](https://github.com/juliangarnier/anime)
- [社區論壇](https://github.com/juliangarnier/anime/discussions)
