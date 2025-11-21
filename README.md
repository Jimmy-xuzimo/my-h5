# 写在你的十八岁

一个温情的数字信件展示页面，使用现代网络技术打造沉浸式阅读体验。

## 🌟 项目简介

这是一个为前女友十八岁生日制作的电子信件项目。页面采用优雅的中文排版设计，融合了现代化的交互动画效果，为读者创造了一个温暖而庄严的阅读环境。

## ✨ 核心特性

### 🎨 设计与视觉
- **双主题系统**：内置亮色和深色主题，完美适配不同光线环境
  - 亮色模式：温暖的米色系调色板（`#fcf9f4`）
  - 深色模式：舒适的暖黑色系（`#1a1815`）
- **高级排版**：使用宋体、楷体等中文字体，提供专业的信件外观
- **响应式布局**：完美适配桌面、平板和手机设备
- **精细的视觉层次**：通过阴影、透明度和间距营造深度感

### 🎬 交互与动画
- **View Transitions API**：现代浏览器上的圆形扩展过渡效果
  - 从主题按钮位置放射状扩展，覆盖整个屏幕
  - 使用 CSS `clip-path` 实现平滑的圆形动画
  - 持续时间：420ms，采用 `cubic-bezier(0.2,0.9,0.3,1)` 缓动曲线
- **Polyfill 后备方案**：对不支持 View Transitions 的浏览器提供优雅降级
- **加载动画**：三个闪烁的星形元素，暗示内容正在展开
- **进入动画**：
  - 标题淡入效果（延迟 0.3s）
  - 每个段落按顺序向上淡入（从 0.5s 开始，每段递增）
  - 签名部分在底部出现（延迟 2.6s）

### ♿ 可访问性
- **ARIA 标签**：主题按钮包含 `aria-pressed` 属性
- **键盘支持**：
  - 主题切换：回车键或空格键激活
  - 打印快捷键：`Ctrl + P` 打开打印对话框
- **双击功能**：双击页面可平滑滚回顶部
- **运动偏好**：尊重用户的 `prefers-reduced-motion` 设置，禁用所有动画

### 📱 跨设备优化
- **断点设置**：
  - 768px 及以下：平板视图（调整内边距和字体大小）
  - 480px 及以下：手机视图（进一步缩小布局）
- **Meta 视口标签**：防止缩放，确保最佳移动体验
- **打印样式**：隐藏交互元素，保留纯白背景用于打印

## 🚀 技术栈

- **HTML5**：语义化标记
- **CSS3**：
  - CSS 变量（`--primary-color`, `--bg-gradient` 等）
  - Grid 和 Flexbox 布局
  - `@media` 查询（响应式设计和打印样式）
  - `::view-transition-old/new` 伪元素
- **JavaScript**：
  - View Transitions API
  - LocalStorage（主题持久化）
  - requestAnimationFrame（性能优化）
  - Window 事件监听

## 🎯 使用方法

### 基本使用
1. 在浏览器中打开 `index.html` 文件
2. 页面将显示加载动画，然后平滑展开信件内容
3. 使用右上角的 🌙/☀️ 按钮切换主题

### 键盘快捷键
| 快捷键 | 功能 |
|--------|------|
| 空格/回车 | 切换主题（焦点在按钮上时） |
| Ctrl + P | 打开打印对话框 |
| 双击 | 平滑滚动回页面顶部 |

### 主题系统
- **自动保存**：用户选择的主题会自动保存到本地存储
- **初始化**：页面加载时恢复之前的主题选择
- **系统偏好**：如果本地没有保存，默认使用浅色主题

## 🛠️ 代码结构

### HTML 结构
```html
<body>
  <div class="loading-screen">        <!-- 加载动画 -->
  <button class="theme-toggle">       <!-- 主题切换 -->
  <div class="container">
    <header class="letter-header">    <!-- 信件标题区 -->
    <main class="letter-content">     <!-- 信件正文 -->
```

### CSS 变量系统
```css
:root {
  --primary-color: #b08d5f;      /* 主色调 */
  --accent-color: #d4b98a;       /* 辅助色 */
  --text-primary: #3a3028;       /* 正文字色 */
  --text-secondary: #6d5d4b;     /* 次要字色 */
  --bg-color: #fcf9f4;           /* 背景色 */
  --bg-gradient: linear-gradient(...);
  --shadow: 0 4px 20px rgba(...);
}

[data-theme="dark"] {
  /* 深色模式的变量定义 */
}
```

### JavaScript 关键函数
- `applyTheme(theme)`：应用主题并持久化
- `getTriggerPoint(e, el)`：获取动画起点坐标
- `prefersReducedMotion()`：检测用户偏好
- `polyfillExpand(x, y, bgColor)`：提供过渡动画的回退方案
- `toggleTheme(e)`：处理主题切换的完整流程

## 🎨 自定义指南

### 修改主题颜色
编辑 CSS 中的颜色变量：
```css
:root {
  --primary-color: 你的颜色;
  --accent-color: 你的颜色;
  /* ... */
}
```

### 修改信件内容
编辑 HTML 中的内容区域：
```html
<header class="letter-header">
  <h1 class="title">你的标题</h1>
  <div class="date">日期</div>
  <p class="subtitle">敬礼人</p>
</header>

<main class="letter-content">
  <p class="paragraph">段落内容...</p>
  <!-- 更多段落 -->
</main>
```

### 修改动画时长
- 加载动画：搜索 `animation: starBlink 1s`
- 淡入效果：搜索 `animation: fadeIn 1.5s`
- 主题切换：搜索 `duration: 420`

## 🌐 浏览器兼容性

| 功能 | Chrome | Firefox | Safari | Edge |
|------|--------|---------|--------|------|
| View Transitions API | ✅ 111+ | ✅ 119+ | ❌ | ✅ 111+ |
| CSS 变量 | ✅ 49+ | ✅ 31+ | ✅ 9.1+ | ✅ 15+ |
| Grid/Flexbox | ✅ | ✅ | ✅ | ✅ |
| Polyfill 降级 | ✅ | ✅ | ✅ | ✅ |

## 📄 页面元素说明

| 元素 | 描述 |
|------|------|
| `.loading-screen` | 加载屏幕，显示三个闪烁的星形 |
| `.theme-toggle` | 右上角的主题切换按钮 |
| `.letter-header` | 信件头部（标题、日期、敬礼） |
| `.letter-content` | 信件正文区域 |
| `.paragraph` | 独立的段落，有缩进和序列动画 |
| `.highlight` | 高亮文本，用主色调突出 |
| `.signature` | 签名区域，带顶部边框分隔 |
| `.theme-fill` | Polyfill 过渡层（如需要） |

## 💡 性能优化

- **CSS contain 属性**：提升渲染性能
- **will-change**：预告浏览器即将变化的属性
- **requestAnimationFrame**：同步浏览器重绘周期
- **动画偏好检测**：尊重用户偏好，减少不必要的动画

## 📝 许可证

个人项目，请根据需要自由使用和修改。

---

**创建时间**：2025年12月31日  
**开发者**：徐子墨
