# Uniswap_learning
### 概念学习(部分)
x*y=k
x：交易对中 token0 的储备金（reserve0）；
y：交易对中 token1 的储备金（reserve1）；
k：恒定常数（理想状态下，Swap 过程中 k 不变，确保价格平滑变化）

实际 Swap 中(x + Δx * (1 - fee)) * (y - Δy) = k 扣除的手续费会留在储备金中，导致 k 略微上升，最终惠及 LP 持有者

LP（Liquidity Provider）代币是用户提供流动性的 “所有权凭证”：用户添加流动性时铸造 LP 代币，移除流动性时销毁 LP 代币，LP 代币的数量与用户占有的储备金比例严格对应

Swap 是用户通过输入一种代币兑换另一种代币的过程，核心是基于 x*y=k 计算输出金额，同时扣除手续费、更新储备金......

### #addLiquidity、removeLiquidity、swap 三大核心函数的 参数、顺序、限制条件

#### addLiquidity
函数参数顺序
function addLiquidity(
    address tokenA    交易对中第一种资产地址（如 USDT）
    address tokenB     交易对中第二种资产地址（如 WETH）
    uint amountADesired   期望存入的 tokenA 数量
    uint amountBDesired   期望存入的 tokenB 数量
    uint amountAMin       可接受的最小 tokenA 实际存入量
    uint amountBMin       可接受的最小 tokenB 实际存入量
    address to            接收 LP Token 的地址
    uint deadline          交易有效期（UNIX 时间戳，过期则交易失败）
) external returns (
    uint amountA          实际存入的 tokenA 数量
    uint amountB          实际存入的 tokenB 数量
    uint liquidity         获得的 LP Token 数量
);
限制条件：
授权前置;
价格比例匹配;
deadline 有效性;
首次添加流动性;
#### removeLiquidity
函数参数顺序
function removeLiquidity(
    address tokenA,       交易对中第一种资产地址
    address tokenB,       交易对中第二种资产地址
    uint liquidity        要销毁的 LP Token 数量
    uint amountAMin       可接受的最小赎回 tokenA 数量
    uint amountBMin       可接受的最小赎回 tokenB 数量
    address to            接收赎回资产的地址
    uint deadline          交易有效期（UNIX 时间戳）
) external returns (
    uint amountA          实际赎回的 tokenA 数量
    uint amountB           实际赎回的 tokenB 数量
);
限制条件：
LP Token 授权;
LP 持仓充足;
deadline 限制;
#### swap
函数参数顺序(例)
function swapExactTokensForTokens(
    uint amountIn,       
    uint amountOutMin  
    address[] calldata path
    address to            
    uint deadline      
) external returns (uint[] memory amounts);
限制条件：
输入资产授权;
路径有效性;
滑点保护;
deadline 限制;
流动性充足

#### Factory/Pair/Router
Factory 创建实体 → Pair 建立关联 → Router 转发数据;
数据流方向：发起者（用户 / 合约调用者）→ Router → Pair → Factory（仅校验）→ Pair（处理核心逻辑）→ Router → 发起者

#### 手续费计算
1. 当用户通过 Router 发起兑换，Pair 合约会在执行兑换逻辑时，先扣 0.3% 手续费，再按 x*y=k 计算兑换数量；
2. 每发生一次兑换，都会有 0.3% 的手续费注入储备池，储备池的总规模会随着手续费的注入不断增加；
3. LP 持有的 LP Token 代表 “对储备池的所有权比例”；
4. LP通过 “燃烧 LP Token 赎回资产” 时，按自己的持仓比例，一次性拿回 “本金 + 对应比例的累积手续费”；
   
### 模块拆分思路
#### 先写pair：
写出能实现添加流动性、swap、移除流动性的最小 Pair 合约，包含3 个核心逻辑：
1. x*y=k 定价规则；
2. LP 代币是流动性所有权凭证；
3. 储备金同步更新；
为了使合约更完善，准备加入几个功能:
管理员权限（只有管理员能添加初始流动性）；
交易手续费（0.3%，给 LP 分红）；
#### 再写Factory：
写出能创建任意交易对的 Factory 合约：
1. 用嵌套映射记录交易对地址；
2. CREATE2 部署；
#### 最后写Router：
写出能简化用户操作的 Router 合约，支持：
1. 自动计算添加流动性的代币比例；
2. 支持 ETH 直接交易（自动包装成 WETH）

最后再尝试拼接完整 AMM 生态（Pair+Factory+Router）
### 总结
1. 感觉这周难度前所未有的大，知识容量大，难度大，理解起来较为困难；
2. 对于一些特有的函数还需要多练习提升熟练度才能进行运用；
3. 本周依赖AI较多，主要是对于诸多概念和函数一头雾水，通过学习能理解部分概念和函数，还有很多问题没有得到解决，这里就不举例了（太多了）