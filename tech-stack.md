# tech-stack.md - Pixel Bay 技术栈推荐

**项目:** Pixel Bay (像素海湾)
**目标:** 打造“最简单但最健壮”的像素风海洋生态缸原型
**适用阶段:** 原型开发 (Prototype) -> 早期产品 (MVP)

---

## 1. 核心技术栈 (The Core Stack)

我们采用 **"Modern Vanilla Web"** 架构，不引入复杂的框架（如 React/Vue），直接通过高性能渲染引擎驱动画面。

| 组件 | 选型 | 理由 (Why?) |
| :--- | :--- | :--- |
| **构建工具** (Build Tool) | **Vite** | **最简单。** 目前最快的对前端构建工具，零配置启动，支持热更新（修改代码浏览器秒变），处理图片资源极其方便。 |
| **编程语言** (Language) | **JavaScript (ES6+)** | **最通用。** 原型阶段直接使用原生 JS，避免 TypeScript 的配置复杂度，足以应付单页面逻辑。 |
| **渲染引擎** (Rendering) | **Pixi.js** (v8) | **最健壮。** Web 界 2D 渲染的“工业标准”。<br>1. **原生支持像素风:** 拥有 `Nearest Neighbor` 缩放模式，保证像素画放大后边缘锐利，不模糊。<br>2. **高性能:** 基于 WebGL，同屏几百条鱼游动也不会卡顿。<br>3. **交互强:** 内置了鼠标悬停/点击检测功能，无需自己算坐标。 |
| **动画库** (Animation) | **GSAP** (可选) | 如果 Pixi 自带的动画不够用，GSAP 是做“弹性”、“缓动”效果最好的库（让鱼游得更自然）。 |

---

## 2. 为什么选择这个组合？

### ✅ 简单 (Simplicity)
* **没有“框架黑盒”:** 不需要学习 React 的生命周期或 Vue 的指令。你只需要一个 `index.html` 和一个 `main.js` 就能跑起来。
* **极简的代码结构:**
    ```javascript
    // 伪代码示例：创建一个应用只需要几行
    import { Application, Sprite } from 'pixi.js';
    
    const app = new Application();
    await app.init({ resizeTo: window, pixelArt: true }); // 开启像素模式
    document.body.appendChild(app.canvas);
    
    const fish = Sprite.from('fish.png');
    app.stage.addChild(fish);
    ```

### 🛡️ 健壮 (Robustness)
* **性能天花板高:** Pixi.js 自动调用显卡 (GPU) 加速。即使你以后想加入光影效果（Minecraft 的海晶灯光晕）或者上千个粒子泡泡，它都能轻松吃下。
* **生态成熟:** 遇到问题随便搜都有解决方案。
* **跨平台铺路:**
    * **Web:** 直接发布。
    * **Mac Desktop:** 后续通过 **Tauri** 或 **Electron** 包裹这个网页，直接变成桌面应用。
    * **Mobile Widget:** iOS 组件开发较特殊（需原生 Swift），但你可以用这个网页作为设计蓝本，或者通过 WebView 嵌入。

---

## 3. 推荐的项目文件结构 (Project Structure)

保持扁平化，方便开发者快速上手。

```text
pixel-bay/
├── index.html          # 入口文件
├── package.json        # 项目配置 (Vite)
├── src/
│   ├── main.js         # 主逻辑 (初始化场景、加载资源)
│   ├── entities/       # 实体类
│   │   ├── Fish.js     # 定义鱼的行为 (游动、转身)
│   │   └── Bubble.js   # 定义气泡粒子
│   ├── data/
│   │   └── fish-data.json # 鱼类配置数据 (ID, 名称, 属性)
│   └── utils/          # 工具函数 (随机数生成等)
└── public/             # 静态资源 (不被打包，直接访问)
    └── assets/
        ├── sprites/    # 鱼类像素图 (.png)
        ├── scene/      # 背景图、海晶灯素材
        └── ui/         # 边框、提示框素材
