

你可以通过 `<script>` 标签直接在 HTML 中使用 Vue。

### 1. 两种主要的引入方式

根据你的需求，主要有以下两种方式：

#### 方法 A：全局变量方式（Global Build）
这是最传统的方式。Vue 会作为一个全局对象 `Vue` 暴露在 `window` 上。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Vue 3 CDN Demo</title>
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
  <div id="app">{{ message }}</div>

  <script>
    const { createApp, ref } = Vue; // 从全局对象中解构所需方法

    createApp({
      setup() {
        const message = ref('你好，Vue 3!');
        return { message };
      }
    }).mount('#app');
  </script>
</body>
</html>
```

#### 方法 B：原生 ES 模块方式（ESM Build）
这种方式更现代，语法更接近于 Vue CLI 或 Vite 的开发体验，不需要全局变量。

```html
<!DOCTYPE html>
<html>
<body>
  <div id="app">{{ count }}</div>

  <script type="module">
    // 直接从 CDN 导入 ES 模块
    import { createApp, ref } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js';

    createApp({
      setup() {
        const count = ref(0);
        return { count };
      }
    }).mount('#app');
  </script>
</body>
</html>
```

---

### 2. 常用 CDN 地址推荐

你可以根据网络情况选择不同的 CDN 服务商：

* **UNPKG**: `https://unpkg.com/vue@3/dist/vue.global.js`
* **jsDelivr**: `https://cdn.jsdelivr.net/npm/vue@3/dist/vue.global.js`
* **字节跳动静态资源库 (国内推荐)**: `https://lf3-cdn-tos.bytecdntp.com/cdn/expire-1-M/vue/3.2.31/vue.global.min.js`

---

### 3. 使用 CDN 的优缺点

| 优点 | 缺点 |
| :--- | :--- |
| **无需安装**: 不用配置 Node.js、npm 或 Webpack/Vite。 | **无组件工程化**: 无法直接使用 `.vue` 单文件组件 (SFC)。 |
| **极速上手**: 写一个 HTML 文件就能运行。 | **性能瓶颈**: 大型项目缺乏按需引入和构建优化（如 Tree-shaking）。 |
| **适合小项目**: 比如在现有的 jQuery 网页中局部嵌入 Vue。 | **生态受限**: 部分第三方 Vue 插件可能需要复杂的配置才能在非构建环境运行。 |

### 💡 进阶建议
如果你在 CDN 环境下也想用类似 `.vue` 文件的开发体验（将 HTML/CSS/JS 写在一起），可以了解一下 [petite-vue](https://github.com/vuejs/petite-vue) 或者使用 [Vue3-sfc-loader](https://github.com/FranckFreiburger/vue3-sfc-loader)，它们能让你在浏览器中直接加载 `.vue` 文件。

