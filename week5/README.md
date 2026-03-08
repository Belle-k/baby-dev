# 🍼 baby-dev - Week 5 学习任务

> 在前几周中，你已经开始接触 **AMM 与 Uniswap 的核心原理**。
> 但真实的 DeFi 协议除了智能合约，还需要一个 **用户界面（Frontend）** 才能被普通用户使用。
>
> 本周我们将开始学习 **Web 前端的基础能力**，并完成一个小项目：
>
> **实现一个 Swap UI（仅前端界面）。**

本周重点不是 UI 设计，而是：

> **理解 Web 页面是如何构建和交互的。**

---

# 🎯 本周目标

1. 理解 Web 前端三大 **基础技术**

```
HTML
CSS
JavaScript
```

2. 能够写出一个简单网页

3. 完成一个 **Swap UI 页面**

4. 将网页 **部署到互联网上访问**

---

# 📎 推荐学习平台

### MDN（最权威的前端文档）

内容覆盖所有前端知识，推荐长期使用。
学习过程中注意 **逐步学习和整理知识结构**。

[https://developer.mozilla.org/en-US/](https://developer.mozilla.org/en-US/)

---

### 菜鸟教程

适合初学者的教程，特点：

* 简单易懂
* 入门友好

但需要注意：

* 内容深度相对较浅

[https://www.runoob.com/](https://www.runoob.com/)

---

### bilibili

如果阅读文档比较困难，可以通过视频学习。

建议：**尽量选择可以跟着敲代码的教程，而不是只讲概念的课程。**

---

# 📘 本周学习内容

浏览器中的网页通常由三部分组成：

```
HTML → 页面结构
CSS → 页面样式
JavaScript → 页面逻辑
```

可以简单理解为：

```
HTML = 骨架
CSS = 外观
JavaScript = 行为
```

---

# 1️⃣ HTML：构建页面结构

HTML 用来描述网页的 **结构和内容**。

例如：

```html
<h1>Mini Swap</h1>

<input placeholder="Token A Amount">

<input placeholder="Token B Amount">

<button>Swap</button>
```

浏览器会渲染为：

```
标题
两个输入框
一个按钮
```

---

## 本周需要掌握的标签

```
div
span
h1
p
input
button
```

建议理解以下概念：

```
id
class
元素嵌套
```

简单示例：

```html
<div class="container">
  <h1>Mini Swap</h1>
  <input placeholder="Token A Amount">
  <button>Swap</button>
</div>
```

---

# 2️⃣ CSS：控制页面样式

CSS 用来控制网页的 **视觉效果**。

例如：

```
颜色
布局
间距
字体
```

示例：

```css
.container {
  width: 400px;
  margin: auto;
}

button {
  background: black;
  color: white;
}
```

---

## 本周需要理解

```
class
margin
padding
border
flex
```

建议重点了解：

```
flex 布局
```

因为现代前端布局 **大多依赖 flex 或 grid**。

简单示例：

```css
.container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
```

---

# 3️⃣ JavaScript：实现交互

JavaScript 让网页可以 **响应用户操作**。

例如：

```
点击按钮
读取输入框
修改页面内容
```

示例：

```javascript
const button = document.querySelector("#swap")

button.onclick = () => {
  console.log("Swap clicked")
}
```

---

## 本周需要理解

```
变量
函数
DOM 操作
事件监听
```

例如：

```javascript
const input = document.querySelector("#tokenA")
const output = document.querySelector("#tokenB")

input.oninput = () => {
  const value = input.value
  output.value = value * 100
}
```

---

# 🧪 本周项目：实现 Swap UI

你需要实现一个 **简单的 Swap 页面**。

---

# 📌 参考示例（可选）

为了帮助大家理解 Swap UI 的基本结构，仓库中提供了一个 **简单示例页面**。

你可以通过示例理解：

```
HTML 页面结构
CSS 页面布局
JavaScript 交互逻辑
```

示例中包含的功能：

```
输入 Token 数量
简单的汇率计算
Swap 方向切换
基础样式布局
```

⚠️ **注意**

* 示例代码 **仅供参考学习**
* 不要求完全复制示例 UI
* 可以根据自己的理解 **自由设计界面**

本周重点是：

> **理解 HTML + CSS + JavaScript 如何协同构建一个网页应用**

只要实现以下核心功能即可：

```
输入 Token A
自动计算 Token B
Swap 方向切换
基本 UI 样式
```

---

## 如何运行示例项目

1. 打开 `example` 文件夹
2. 在 VSCode 中打开 `index.html`
3. 右键点击文件
4. 选择：

```
Open with Live Server
```

浏览器会自动打开示例页面。

---

# 必须实现的功能

## 1️⃣ 输入 Token A 数量

用户可以输入：

```
1
2
10
```

---

## 2️⃣ 自动计算 Token B

使用一个简单公式：

```
tokenB = tokenA * 100
```

示例：

```
输入 1
输出 100
```

目的是练习：

```
读取输入框
更新另一个输入框
```

---

## 3️⃣ Swap 方向按钮

增加一个按钮：

```
⇅
```

点击后交换：

```
Token A
Token B
```

例如：

```
ETH → USDC
```

变成：

```
USDC → ETH
```

---

# 📁 目录结构

```
week5/<your_name>/
├── index.html
├── style.css
├── main.js
└── README.md
```

---

# 📄 README.md 内容

需要说明：

* 项目介绍
* 页面截图
* Swap UI 实现逻辑
* 使用的技术
* 部署地址

---

# ✅ 验收清单

必须全部满足：

* [ ] 完成 Swap UI 页面
* [ ] Token A 输入可以更新 Token B
* [ ] 实现 Swap 方向切换
* [ ] 页面样式基本可用
* [ ] 成功部署网页
* [ ] README 完整

---

# 📌 进阶学习内容（可选）

如果你对前端感兴趣，可以进一步学习：

```
React
```

React 是目前最主流的前端框架之一。

很多 Web3 项目（例如 Uniswap）都使用 React 构建前端。

但本课程 **不会强制要求学习 React**。

---

# 🧠 本周真正的目标

本周不是让你成为前端工程师。

而是：

> **当你需要为区块链项目写一个前端界面时，你可以自己完成。**

在接下来的几周中，你将会把这个 UI **升级为真正的 Web3 DApp**。

届时你将实现：

```
钱包连接
读取链上数据
发起交易
```

最终完成一个 **完整可用的 DeFi 前端应用**。

**在 Week6 中，我们将开始让这个 UI 连接真实的区块链。**
