# Anime.js 使用指南 [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[![繁體中文](https://img.shields.io/badge/繁體中文-點擊查看-orange)](README.md)
[![简体中文](https://img.shields.io/badge/简体中文-点击查看-orange)](README-zh.md)

这是一个针对 Anime.js 的全面使用指南，Anime.js 是一个轻量级的 JavaScript 动画库，适用于动画 CSS 属性、SVG、DOM 属性和 JavaScript 对象。本指南涵盖安装、核心概念、动画类型、高级功能及实用资源，帮助您快速上手并创建流畅的动画效果。

- [什么是 Anime.js？](#什么是-animejs)
- [安装](#安装)
- [快速入门](#快速入门)
- [核心概念](#核心概念)
- [动画类型](#动画类型)
- [高级功能](#高级功能)
- [控制动画](#控制动画)
- [缓动函数](#缓动函数)
- [SVG 动画](#svg-动画)
- [性能考虑](#性能考虑)
- [故障排除](#故障排除)
- [资源](#资源)

## 什么是 Anime.js？

Anime.js 是一个快速、轻量级的 JavaScript 动画库，专为创建流畅的网页动画而设计。它支持动画 CSS 属性、SVG、DOM 属性和 JavaScript 对象，提供简单而强大的 API，让您轻松实现复杂的动画效果。无论是初学者还是专业开发者，Anime.js 都能满足您的需求。

## 安装

### CDN

将以下 `<script>` 标签添加到您的 HTML 文件中，即可通过 CDN 导入 Anime.js：

```html
<script src="https://cdn.jsdelivr.net/npm/animejs@latest/lib/anime.min.js"></script>
```

### npm

使用 npm 安装 Anime.js：

```bash
npm install animejs
```

然后在 JavaScript 文件中导入：

```javascript
import anime from "animejs/lib/anime.es.js";
```

## 快速入门

以下是一个简单范例，展示如何使用 Anime.js 移动一个 div 元素：

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

此范例将 `.box` 元素向右移动 250 像素，动画持续 1 秒，使用 `easeInOutQuad` 缓动函数。

## 核心概念

### 目标

动画的目标可以是：

- **CSS 选择器**：如 `'.class'`、`'#id'`
- **DOM 元素**：如 `document.querySelector('.class')`
- **JavaScript 对象**：如 `{ prop: 0 }`
- **数组**：如 `[element1, element2]`

### 属性

可动画的属性包括：

- **CSS 属性**：如 `translateX`、`scale`、`opacity`
- **SVG 属性**：如 `points`、`path`
- **DOM 属性**：如 `scrollTop`、`value`
- **JavaScript 对象属性**：如 `obj.prop`

### 选项

常见动画选项：

- `duration`：持续时间（毫秒）
- `delay`：延迟（毫秒）
- `easing`：缓动函数（如 `'linear'`、`'easeInOutQuad'`）
- `loop`：是否循环（`true` 或次数）
- `direction`：方向（`'normal'`、`'reverse'`、`'alternate'`）

## 动画类型

### CSS 属性动画

动画 CSS 属性：

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

### SVG 动画

动画 SVG 属性：

```javascript
anime({
  targets: "#mySVG path",
  d: "M10 10 H 90 V 90 H 10 Z",
  easing: "easeInOutQuad",
  duration: 2000,
});
```

### DOM 属性动画

动画 DOM 属性：

```javascript
anime({
  targets: document.documentElement,
  scrollTop: 1000,
  duration: 2000,
  easing: "easeInOutQuad",
});
```

### JavaScript 对象动画

动画 JavaScript 对象：

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

## 高级功能

### 时间轴

使用时间轴创建序列或并行动画：

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
); // 与上一个动画重叠 500ms
```

### 交错动画

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

### 路径动画

沿 SVG 路径动画元素：

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

## 控制动画

控制动画播放：

```javascript
const animation = anime({
  targets: ".box",
  translateX: 250,
  autoplay: false,
});

animation.play(); // 播放
animation.pause(); // 暂停
animation.seek(500); // 寻找至 500ms
animation.restart(); // 重新开始
animation.reverse(); // 反转
```

## 缓动函数

支持多种缓动函数，或自定义：

```javascript
anime({
  targets: ".box",
  translateX: 250,
  easing: function (el, i, total) {
    return function (t) {
      return Math.pow(t, 2); // 自定义二次方缓动
    };
  },
});
```

## SVG 动画

动画 SVG 元素：

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

## 性能考虑

- 使用 `requestAnimationFrame` 确保动画平滑。
- 避免复杂 DOM 操作。
- 大量动画时，考虑分批处理或使用 Web Workers。

## 故障排除

- **动画不运行**：检查目标和属性是否正确。
- **动画闪烁**：调整缓动函数或持续时间。
- **性能问题**：减少同时运行的动画数量。

## 资源

- [官方文档](https://animejs.com/documentation/)
- [GitHub 仓库](https://github.com/juliangarnier/anime)
- [社区论坛](https://github.com/juliangarnier/anime/discussions)
