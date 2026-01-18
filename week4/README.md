# 🍼 baby-dev - Week 4 学习任务

> 承接 Week3 对 Uniswap V2 机制的系统学习，本周正式进入 **实战实现阶段**。
> 要求 **完全基于自己的理解手写一个基础版 Uniswap V2（Core 为主）**，并在完成后 **逐项对齐官方实现与设计选择**，理解「为什么官方要这么写」。

---

## 🎯 本周目标

1. **手写一个基础版 Uniswap V2 AMM**

   * 覆盖 Factory + Pair（Core 级别）
   * 支持基础功能：建池、加/减流动性、swap
2. **严格理解并实现核心不变量**

   * `x * y = k`
   * 手续费模型（0.3%）
   * 储备同步与状态更新
3. **与官方代码逐项对齐**

   * 对照 `UniswapV2Pair.sol`
   * 理解每个关键设计点存在的原因，而不是“照抄”
4. **输出对齐分析文档**

   * 清楚写出：你 vs 官方 的差异、取舍与理解

---

## 📘 必做任务

### 1️⃣ 手写基础版 Uniswap V2（核心任务）

> ⚠️ **禁止直接复制官方实现**
> 你必须先写“自己的版本”，再做对齐分析。

#### 必须实现的合约

* `Factory`

  * `createPair(tokenA, tokenB)`
  * pair 地址管理（mapping）
* `Pair`

  * 状态变量：

    * `token0 / token1`
    * `reserve0 / reserve1`
    * `totalSupply / balanceOf`（LP Token）
  * 核心函数：

    * `mint()`（add liquidity）
    * `burn()`（remove liquidity）
    * `swap()`
    * `_update()`（reserve 更新）
  * 事件：

    * `Mint / Burn / Swap / Sync`

> Router **不是强制要求**，但如果你有余力可以实现一个最小 Router

---

### 2️⃣ 关键实现要求

#### ✅ 常数乘积不变量

* swap 前后需满足：

  ```
  (reserve0 * reserve1) <= (balance0 * balance1)
  ```
* 需要考虑手续费后的输入输出关系

#### ✅ 手续费机制

* 实现 0.3% swap fee（如 `amountIn * 997 / 1000`）
* 明确手续费是如何“隐式累积给 LP 的”

#### ✅ LP 份额计算

* 初始流动性：

  ```
  liquidity = sqrt(amount0 * amount1)
  ```
* 后续流动性：

  ```
  min(
    amount0 * totalSupply / reserve0,
    amount1 * totalSupply / reserve1
  )
  ```

#### ✅ 状态安全

* 防止非法 swap（0 输出、储备不足）
* reserve / balance 不一致问题
* 最基础的 reentrancy 防护意识（不要求完整实现）

---

### 3️⃣ 与官方代码对齐分析（**强制提交文档**）

在实现完成后，你需要 **逐条对齐官方 Uniswap V2 Core 实现**。

#### 对齐范围

* `UniswapV2Pair.sol`

  * `mint / burn / swap / _update`
  * `getReserves`
  * fee 处理逻辑
* Factory 的 pair 创建逻辑

#### 文档中必须回答的问题

* 哪些地方你和官方实现 **完全一致**
* 哪些地方你：

  * 简化了？
  * 理解不完整？
  * 选择了不同实现？
* 官方实现中你认为：

  * **“如果不这么写会出 bug”** 的地方
  * **“为 Gas / 安全性服务”** 的地方
* 至少列出 **3 个你在对齐过程中“恍然大悟”的点**

---

## 🧪 提交规范

### 📁 目录结构建议

```
week4/<your_name>/
├── contracts/
│   ├── Factory.sol
│   ├── Pair.sol
│   └── (optional) Router.sol
├── README.md
```

### 📄 README.md 内容建议

* 本周实现范围说明
* 已支持的功能 / 未支持的功能
* 如何运行或测试（如有）
* 本周最大收获（简要）
* 自己的实现简介
* 与官方实现的逐点对齐分析
* 差异表 or 分段说明
* 对 AMM / Uniswap V2 的理解变化

---

## ✅ 验收清单（必须全部满足）

* [ ] 手写 Factory + Pair（不可直接抄官方）
* [ ] swap / mint / burn 可正常推演逻辑
* [ ] 正确实现 `x*y=k` 与手续费
* [ ] 完成 **官方代码对齐分析文档**
* [ ] README 清楚说明实现边界

---

## 📎 参考资料（对齐阶段使用）

* Uniswap V2 Core：
  [https://github.com/Uniswap/v2-core](https://github.com/Uniswap/v2-core)
* 官方文档：
  [https://docs.uniswap.org/contracts/v2](https://docs.uniswap.org/contracts/v2)
* 数学辅助：
  * Babylonian sqrt
  * 流动性份额推导

---

> **Week4 是整个 baby-dev AMM 学习路线的“分水岭”**
> 能否完整写出 + 对齐 Uniswap V2，基本决定了你是否真正理解了 DeFi 协议工程。
> 不追求代码多，而追求：**每一行你都知道为什么存在。**
