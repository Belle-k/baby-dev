# 🍼 baby-dev - Week 5 学习任务

> 承接 Week4 对 Uniswap V2 Core 的手写实现与源码对齐，本周进入 **协议落地阶段**。
> 要求 **将你自己实现的 Uniswap V2 部署到测试网，并提供一个可访问的前端进行真实交互**，完成从「协议实现」到「用户可用」的闭环。

---

## 🎯 本周目标

1. **将手写的 Uniswap V2 合约部署到测试网**
   * 使用 Remix 完成部署
   * 能在区块浏览器中查看状态与事件
2. **实现最小可用前端（原生）**
   * 能连接钱包
   * 能读取合约状态
   * 能发起真实交易
3. **跑通完整链路**
   * 钱包 → 前端 → 合约 → 状态变化
4. **输出清晰的部署与使用文档**

---

## 📘 必做任务

### 1️⃣ 使用 Remix 部署 Uniswap V2 合约（核心任务）

> ⚠️ **本周部署工具统一要求使用 Remix**
> 目标是降低工具复杂度，聚焦协议与交互本身。

#### 部署环境

* Remix IDE：[https://remix.ethereum.org](https://remix.ethereum.org)
* 钱包：MetaMask
* 网络：测试网（Sepolia / Holesky 任选）

#### 必须部署的合约

* `Factory`
* 通过 `Factory.createPair()` 创建的 `Pair`
* （如 Week4 已实现）最小 Router（非强制）

#### 推荐部署顺序

1. 在 Remix 中编译并部署 `Factory`
2. 调用 `createPair(tokenA, tokenB)`
3. 记录返回的 Pair 地址
4. 在 Remix 中直接调用 Pair：

   * `mint()`（add liquidity）
   * `swap()`
   * `burn()`（如已实现）

---

### 2️⃣ Remix 自测要求（必须完成）

在 Remix 中，你需要 **手动验证以下行为**：

* addLiquidity 是否正确铸造 LP
* swap 后 reserve 是否更新
* swap 前后是否满足 `x * y = k`（近似）
* 是否触发以下事件：

  * `Mint`
  * `Swap`
  * `Sync`
* 非法操作是否被 revert（如 0 输出、储备不足）

---

### 3️⃣ 原生前端交互（重点-可借助大模型简单实现）

> 本周前端的目标不是“好看”，而是 **真实可用**

#### 技术要求

* 技术栈：

  * 原生 HTML + JavaScript
  * `ethers.js` 或 `viem`
* 不使用前端框架（React / Vue 等）

#### 前端最低功能要求

* 连接钱包（MetaMask）
* 读取链上数据：

  * `reserve0 / reserve1`
  * `totalSupply`（如需要）
* 发起交易：

  * addLiquidity
  * swap（最简单路径）

> ⚠️ 前端 **必须使用你通过 Remix 部署的真实合约地址**

---

## 🧪 提交规范

### 📁 目录结构建议

```
week5/<your_name>/
├── frontend/
│   ├── index.html
│   ├── main.js
│   └── README.md
├── deployment.md
└── README.md
```

---

### 📄 README.md 内容建议

* 本周目标与完成情况
* 测试网名称
* 合约地址：

  * Factory
  * Pair
* 前端访问地址（Vercel）
* 已支持的功能 / 未支持的功能
* 本周最大问题 & 收获

---

### 📄 deployment.md（强制）

必须清楚记录：

* 使用的测试网
* Factory 合约地址
* Pair 合约地址
* `createPair` 交易 hash
* 至少一次：

  * addLiquidity 交易 hash
  * swap 交易 hash
* 部署 & 调用过程中遇到的问题（简要）

---

## ✅ 验收清单（必须全部满足）

* [ ] 使用 Remix 成功部署 Factory
* [ ] 使用 Remix 成功创建 Pair
* [ ] Remix 中完成 addLiquidity
* [ ] Remix 中完成 swap
* [ ] 前端可读取 reserve 数据
* [ ] 前端可发起交易
* [ ] README + deployment.md 完整

---

## 📎 参考资料

* Remix 官方文档：[https://remix-ide.readthedocs.io](https://remix-ide.readthedocs.io)
* ethers.js：[https://docs.ethers.org](https://docs.ethers.org)
* Vercel：[https://vercel.com/docs](https://vercel.com/docs)
* Uniswap Interface（仅参考交互方式）

---

> **Week5 的完成标志不是“代码更多”，而是：**
> > **“你写的 AMM，已经可以被任何人通过浏览器真实使用。”**
> 从这一周开始，你已经具备了一个 **可展示、可讲解、可验证** 的完整 Web3 项目。

