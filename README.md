# Anime.js 使用指南

**繁體中文** | **简体中文**

Anime.js 是一個輕量級的 JavaScript 動畫庫，適用於動畫 CSS 屬性、SVG、DOM 屬性和 JavaScript 物件。它提供了一個簡單而強大的 API，讓您可以輕鬆創建流暢的動畫效果，適合初學者和專業開發者。  
Anime.js 是一个轻量级的 JavaScript 动画库，适用于动画 CSS 属性、SVG、DOM 属性和 JavaScript 对象。它提供了一个简单而强大的 API，让您可以轻松创建流畅的动画效果，适合初学者和专业开发者。

## 目錄 | 目录

- [簡介 | 简介](#簡介--简介)
- [安裝 | 安装](#安裝--安装)
  - [CDN](#cdn)
  - [npm](#npm)
- [快速入門 | 快速入门](#快速入門--快速入门)
- [核心概念 | 核心概念](#核心概念)
  - [目標 | 目标](#目標--目标)
  - [屬性 | 属性](#屬性--属性)
  - [選項 | 选项](#選項--选项)
- [動畫類型 | 动画类型](#動畫類型--动画类型)
  - [CSS 屬性動畫 | CSS 属性动画](#css-屬性動畫--css-属性动画)
  - [SVG 動畫 | SVG 动画](#svg-動畫--svg-动画)
  - [DOM 屬性動畫 | DOM 属性动画](#dom-屬性動畫--dom-属性动画)
  - [JavaScript 物件動畫 | JavaScript 对象动画](#javascript-物件動畫--javascript-对象动画)
- [高級功能 | 高级功能](#高級功能--高级功能)
  - [時間軸 | 时间轴](#時間軸--时间轴)
  - [交錯動畫 | 交错动画](#交錯動畫--交错动画)
  - [路徑動畫 | 路径动画](#路徑動畫--路径动画)
- [回調和事件 | 回调和事件](#回調和事件--回调和事件)
- [控制動畫 | 控制动画](#控制動畫--控制动画)
- [緩動函數 | 缓动函数](#緩動函數--缓动函数)
- [SVG 動畫 | SVG 动画](#svg-動畫--svg-动画-1)
- [性能考慮 | 性能考虑](#性能考慮--性能考虑)
- [故障排除 | 故障排除](#故障排除--故障排除)
- [資源 | 资源](#資源--资源)

## 簡介 | 简介

**繁體中文**:  
Anime.js 是一個快速、輕量級的 JavaScript 動畫庫，專為創建流暢的網頁動畫而設計。它支援動畫 CSS 屬性、SVG、DOM 屬性和 JavaScript 物件，提供了一個簡單而強大的 API，讓您能夠輕鬆實現複雜的動畫效果。

**简体中文**:  
Anime.js 是一个快速、轻量级的 JavaScript 动画库，专为创建流畅的网页动画而设计。它支持动画 CSS 属性、SVG、DOM 属性和 JavaScript 对象，提供了一个简单而强大的 API，让您能够轻松实现复杂的动画效果。

## 安裝 | 安装

### CDN

**繁體中文**:  
您可以通過 CDN 直接在 HTML 文件中導入 Anime.js。將以下 `<script>` 標籤添加到您的 HTML 文件：  
**简体中文**:  
您可以通过 CDN 直接在 HTML 文件中导入 Anime.js。将以下 `<script>` 标签添加到您的 HTML 文件：

```html
<script src="https://cdn.jsdelivr.net/npm/animejs@latest/lib/anime.min.js"></script>
```

### npm

**繁體中文**:  
如果您使用 npm，可以通過以下命令安裝 Anime.js：  
**简体中文**:  
如果您使用 npm，可以通过以下命令安装 Anime.js：

```bash
npm install animejs
```

**繁體中文**:  
然後在您的 JavaScript 文件中導入：  
**简体中文**:  
然后在您的 JavaScript 文件中导入：

```javascript
import anime from "animejs/lib/anime.es.js";
```

## 快速入門 | 快速入门

**繁體中文**:  
以下是一個簡單的動畫範例，展示如何使用 Anime.js 移動一個 div 元素：  
**简体中文**:  
以下是一个简单的动画范例，展示如何使用 Anime.js 移动一个 div 元素：

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

**繁體中文**:  
這個範例將 `.box` 元素向右移動 250 像素，動畫持續 1 秒，並使用 `easeInOutQuad` 緩動函數。  
**简体中文**:  
这个范例将 `.box` 元素向右移动 250 像素，动画持续 1 秒，并使用 `easeInOutQuad` 缓动函数。

## 核心概念 | 核心概念

### 目標 | 目标

**繁體中文**:  
動畫的目標可以是以下之一：

- **CSS 選擇器**：例如 `'.class'`、`'#id'`
- **DOM 元素**：例如 `document.querySelector('.class')`
- **JavaScript 物件**：例如 `{ prop: 0 }`
- **陣列**：例如 `[element1, element2]`

**简体中文**:  
动画的目标可以是以下之一：

- **CSS 选择器**：例如 `'.class'`、`'#id'`
- **DOM 元素**：例如 `document.querySelector('.class')`
- **JavaScript 对象**：例如 `{ prop: 0 }`
- **数组**：例如 `[element1, element2]`

### 屬性 | 属性

**繁體中文**:  
您可以動畫多種屬性，包括：

- **CSS 屬性**：如 `translateX`、`scale`、`opacity`
- **SVG 屬性**：如 `points`、`path`
- **DOM 屬性**：如 `scrollTop`、`value`
- **JavaScript 物件屬性**：如 `obj.prop`

**简体中文**:  
您可以动画多种属性，包括：

- **CSS 属性**：如 `translateX`、`scale`、`opacity`
- **SVG 属性**：如 `points`、`path`
- **DOM 属性**：如 `scrollTop`、`value`
- **JavaScript 对象属性**：如 `obj.prop`

### 選項 | 选项

**繁體中文**:  
動畫選項用於配置動畫行為，常見選項包括：

- `duration`：動畫持續時間（毫秒）
- `delay`：動畫延遲（毫秒）
- `easing`：緩動函數（如 `'linear'`、`'easeInOutQuad'`）
- `loop`：是否循環動畫（`true` 或次數）
- `direction`：動畫方向（`'normal'`、`'reverse'`、`'alternate'`）

**简体中文**:  
动画选项用于配置动画行为，常见选项包括：

- `duration`：动画持续时间（毫秒）
- `delay`：动画延迟（毫秒）
- `easing`：缓动函数（如 `'linear'`、`'easeInOutQuad'`）
- `loop`：是否循环动画（`true` 或次数）
- `direction`：动画方向（`'normal'`、`'reverse'`、`'alternate'`）

## 動畫類型 | 动画类型

### CSS 屬性動畫 | CSS 属性动画

**繁體中文**:  
動畫 CSS 屬性，如 `transform`、`opacity` 等：  
**简体中文**:  
动画 CSS 属性，如 `transform`、`opacity` 等：

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

### SVG 動畫 | SVG 动画

**繁體中文**:  
動畫 SVG 屬性，如 `points`、`path`：  
**简体中文**:  
动画 SVG 属性，如 `points`、`path`：

```javascript
anime({
  targets: "#mySVG path",
  d: "M10 10 H 90 V 90 H 10 Z",
  easing: "easeInOutQuad",
  duration: 2000,
});
```

### DOM 屬性動畫 | DOM 属性动画

**繁體中文**:  
動畫 DOM 屬性，如 `scrollTop`：  
**简体中文**:  
动画 DOM 属性，如 `scrollTop`：

```javascript
anime({
  targets: document.documentElement,
  scrollTop: 1000,
  duration: 2000,
  easing: "easeInOutQuad",
});
```

### JavaScript 物件動畫 | JavaScript 对象动画

**繁體中文**:  
動畫 JavaScript 物件的屬性：  
**简体中文**:  
动画 JavaScript 对象的属性：

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

## 高級功能 | 高级功能

### 時間軸 | 时间轴

**繁體中文**:  
使用時間軸創建動畫序列或並行動畫：  
**简体中文**:  
使用时间轴创建动画序列或并行动画：

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
); // 與上一個動畫重疊 500ms | 与上一个动画重叠 500ms
```

### 交錯動畫 | 交错动画

**繁體中文**:  
為多個目標創建延遲動畫：  
**简体中文**:  
为多个目标创建延迟动画：

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

### 路徑動畫 | 路径动画

**繁體中文**:  
沿著 SVG 路徑動畫元素：  
**简体中文**:  
沿着 SVG 路径动画元素：

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

## 回調和事件 | 回调和事件

**繁體中文**:  
Anime.js 提供多種回調函數：

- `begin`：動畫開始時調用
- `update`：動畫更新時調用
- `complete`：動畫完成時調用

**简体中文**:  
Anime.js 提供多种回调函数：

- `begin`：动画开始时调用
- `update`：动画更新时调用
- `complete`：动画完成时调用

**範例 | 示例**：

```javascript
anime({
  targets: ".box",
  translateX: 250,
  begin: function (anim) {
    console.log("動畫開始 | 动画开始");
  },
  update: function (anim) {
    console.log("動畫更新 | 动画更新");
  },
  complete: function (anim) {
    console.log("動畫完成 | 动画完成");
  },
});
```

## 控制動畫 | 控制动画

**繁體中文**:  
您可以控制動畫的播放、暫停等：  
**简体中文**:  
您可以控制动画的播放、暂停等：

```javascript
const animation = anime({
  targets: ".box",
  translateX: 250,
  autoplay: false, // 不自動播放 | 不自动播放
});

// 播放動畫 | 播放动画
animation.play();

// 暫停動畫 | 暂停动画
animation.pause();

// 尋找動畫的特定時間 | 寻找动画的特定时间
animation.seek(500); // 尋找到 500ms | 寻找到 500ms

// 重新開始動畫 | 重新开始动画
animation.restart();

// 反轉動畫 | 反转动画
animation.reverse();
```

## 緩動函數 | 缓动函数

**繁體中文**:  
Anime.js 支援多種內置緩動函數，如 `'linear'`、`'easeInQuad'` 等。您也可以自定義緩動函數：  
**简体中文**:  
Anime.js 支持多种内置缓动函数，如 `'linear'`、`'easeInQuad'` 等。您也可以自定义缓动函数：

```javascript
anime({
  targets: ".box",
  translateX: 250,
  easing: function (el, i, total) {
    return function (t) {
      return Math.pow(t, 2); // 自定義二次方緩動 | 自定义二次方缓动
    };
  },
});
```

## SVG 動畫 | SVG 动画

**繁體中文**:  
Anime.js 特別適合動畫 SVG 元素，例如動畫屬性、路徑和形狀：  
**简体中文**:  
Anime.js 特别适合动画 SVG 元素，例如动画属性、路径和形状：

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

## 性能考慮 | 性能考虑

**繁體中文**:

- 使用 `requestAnimationFrame` 確保動畫平滑。
- 避免在動畫中進行複雜的 DOM 操作。
- 對於大量動畫，考慮分批處理或使用 Web Workers。

**简体中文**:

- 使用 `requestAnimationFrame` 确保动画平滑。
- 避免在动画中进行复杂的 DOM 操作。
- 对于大量动画，考虑分批处理或使用 Web Workers。

## 故障排除 | 故障排除

**繁體中文**:

- **動畫不運行**：檢查目標是否正確、屬性是否支援動畫。
- **動畫閃爍**：確保使用適當的緩動函數和持續時間。
- **性能問題**：減少同時運行的動畫數量，優化代碼。

**简体中文**:

- **动画不运行**：检查目标是否正确、属性是否支持动画。
- **动画闪烁**：确保使用适当的缓动函数和持续时间。
- **性能问题**：减少同时运行的动画数量，优化代码。

## 資源 | 资源

**繁體中文**:

- [官方文檔 | 官方文档](https://animejs.com/documentation/)
- [GitHub 倉庫 | GitHub 仓库](https://github.com/juliangarnier/anime)
- [社區論壇 | 社区论坛](https://github.com/juliangarnier/anime/discussions)

**简体中文**:

- [官方文档](https://animejs.com/documentation/)
- [GitHub 仓库](https://github.com/juliangarnier/anime)
- [社区论坛](https://github.com/juliangarnier/anime/discussions)

---

### 補充說明

這個雙語說明文件提供了 Anime.js 的全面介紹和使用指南，涵蓋所有主要功能，並以繁體中文和簡體中文並列呈現，方便兩種語言的使用者閱讀。每個部分都附有清晰的代碼範例，無論您是初學者還是進階使用者，都能快速上手並創建出色的動畫效果。
