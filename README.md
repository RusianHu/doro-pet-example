# Doro 网站宠物示例

这是一个简单的 HTML 示例，演示了如何创建一个跟随鼠标移动并在鼠标按下时播放动画的网站宠物。

## 文件结构

```
doro-pet-example/
├── index.html   # 主要的 HTML 文件，包含 CSS 和 JavaScript 代码
├── doro.gif     # 鼠标宠物的 GIF 图片
└── README.md    # 本说明文件
```

## 如何运行

直接在你的网页浏览器中打开 `index.html` 文件即可查看效果。

## 实现原理

1.  **HTML (`index.html`)**:
    *   包含一个 `<img>` 元素，ID 设置为 `mouse-pet`，`src` 指向 `doro.gif`。这个图片就是我们的“宠物”。

2.  **CSS (`<style>` 标签内)**:
    *   `#mouse-pet` 样式：
        *   `position: fixed;`: 使图片相对于浏览器窗口定位，这样它就不会随着页面滚动而移动。
        *   `width`, `height`: 设置图片大小。
        *   `pointer-events: none;`: 允许鼠标事件（如点击、悬停）“穿透”图片，作用于图片下方的元素。这很重要，否则图片会挡住链接或按钮。
        *   `z-index: 9999;`: 确保图片显示在页面其他所有元素的最上层。
        *   `transition: top 0.05s linear, left 0.05s linear;`: 添加平滑过渡效果，让图片移动看起来更流畅。
        *   `user-select: none;`: 防止用户意外选中图片。

3.  **JavaScript (`<script>` 标签内)**:
    *   获取 `mouse-pet` 元素。
    *   **鼠标移动 (`mousemove`)**: 监听整个文档的鼠标移动事件。当鼠标移动时，获取鼠标的客户端坐标 (`e.clientX`, `e.clientY`)，并更新宠物的 `style.left` 和 `style.top` 属性，使其位置跟随鼠标（加上一点偏移量 `offsetX`, `offsetY`，避免鼠标指针完全覆盖图片）。使用 `requestAnimationFrame` 来优化移动的性能。
    *   **鼠标按下 (`mousedown`)**: 监听鼠标按下事件。当检测到左键或右键按下时，通过在图片 `src` 后面附加一个当前时间戳 (`?t=...`) 来强制浏览器重新加载 GIF。这会使 GIF 动画从头开始播放。
    *   **鼠标松开 (`mouseup`)**: 监听鼠标松开事件。将图片的 `src` 恢复为原始的 `doro.gif` 路径（不带时间戳）。浏览器通常会停止播放 GIF 或显示其第一帧。
    *   **鼠标移出 (`mouseleave`)**: 当鼠标移出浏览器窗口时，也停止动画。
    *   **阻止右键菜单 (`contextmenu`)**: 阻止宠物图片本身的右键菜单弹出，因为右键也被用来触发动画。

## 定制

*   **更换图片**: 将 `doro.gif` 替换为你自己的 GIF 图片，并相应地更新 `index.html` 中的 `src` 属性。
*   **调整大小**: 修改 CSS 中 `#mouse-pet` 的 `width` 和 `height`。
*   **调整偏移**: 修改 JavaScript 中的 `offsetX` 和 `offsetY` 值，改变图片相对于鼠标指针的位置。
*   **移动速度/平滑度**: 修改 CSS 中 `#mouse-pet` 的 `transition` 属性值。
