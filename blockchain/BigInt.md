# Web3 前端开发中的 BigInt 与 Decimals 精度转换与显示

> 本文适用于使用 **Viem** + **Wagmi** + **Next.js** 的前端开发者，讲解如何正确处理链上数字单位 `BigInt` 与小数位 `decimals`，实现 **金额的正确转换与显示**。

---

## 📚 目录

- [Web3 前端开发中的 BigInt 与 Decimals 精度转换与显示](#web3-前端开发中的-bigint-与-decimals-精度转换与显示)
  - [📚 目录](#-目录)
  - [🧠 背景知识](#-背景知识)
  - [💡 为什么链上必须使用 BigInt](#-为什么链上必须使用-bigint)
  - [🔢 什么是 decimals（精度）](#-什么是-decimals精度)
  - [🧰 常用转换工具函数](#-常用转换工具函数)
  - [✍️ 前端输入 ➜ 链上单位：`parseUnits`](#️-前端输入--链上单位parseunits)
  - [✍️ 前端输入 ➜ 转链上：必须转为 BigInt](#️-前端输入--转链上必须转为-bigint)
  - [📤 链上值 ➜ UI 显示：`formatUnits`](#-链上值--ui-显示formatunits)
  - [📌 从合约读取的 BigInt 数值应使用 formatUnits 格式化后再展示到 UI。](#-从合约读取的-bigint-数值应使用-formatunits-格式化后再展示到-ui)

---

## 🧠 背景知识

以太坊链上所有代币数值 **只能以整数存储和传输**，小数的概念是通过 `decimals` 精度来模拟的。

**示例：**
- ETH 精度为 `18`，1 ETH = `10^18` wei
- USDC 精度为 `6`，1 USDC = `10^6` 最小单位

---

## 💡 为什么链上必须使用 BigInt

JavaScript 的普通数字类型 `Number` 最大安全值是 `2^53 - 1 ≈ 9 * 10^15`，但链上常见的单位（如 1 ETH = 10^18 wei）**远远超出这个范围**，所以我们必须使用：

```ts
1234567890123456789n // ✅ BigInt 类型（注意后缀 `n`）
```
## 🔢 什么是 decimals（精度）

代币合约中定义的 `decimals` 决定了这个 Token 有多少位小数。

| Token | decimals | 示例 |
|-------|----------|------|
| ETH   | 18       | 1 ETH = 1e18 wei |
| USDC  | 6        | 1 USDC = 1e6 单位 |
| DAI   | 18       | 1 DAI = 1e18 单位 |

---

## 🧰 常用转换工具函数

Viem 中提供了以下 4 个转换函数：

| 函数名                 | 用途                        | 示例 |
|------------------------|-----------------------------|------|
| `parseEther`           | `"1.23"` ETH ➜ wei（18位） | `parseEther('1.23')` |
| `formatEther`          | wei ➜ `"1.23"` ETH         | `formatEther(1230000000000000000n)` |
| `parseUnits(value, decimals)` | 任意小数单位 ➜ BigInt     | `parseUnits('10.5', 6)` → `10500000n` |
| `formatUnits(value, decimals)` | BigInt ➜ 人类可读字符串 | `formatUnits(10500000n, 6)` → `'10.5'` |

---

## ✍️ 前端输入 ➜ 链上单位：`parseUnits`

```ts
import { parseUnits } from 'viem'

const amount = parseUnits('10.5', 6)
// => 10500000n
```
## ✍️ 前端输入 ➜ 转链上：必须转为 BigInt

在传入合约之前，**必须将用户输入的金额（如 "10.5"）转换成链上识别的整数 BigInt 类型**。

---

## 📤 链上值 ➜ UI 显示：`formatUnits`

```ts
import { formatUnits } from 'viem'

const balance = 10500000n
const display = formatUnits(balance, 6)
// => '10.5'
```

## 📌 从合约读取的 BigInt 数值应使用 formatUnits 格式化后再展示到 UI。

🔁 完整示例（ERC20 转账）
```ts
import { parseUnits } from 'viem'
import { useAccount, useWriteContract, erc20Abi } from 'wagmi'

const { address } = useAccount()
const { writeContractAsync } = useWriteContract()

async function transferUSDC() {
  const amount = parseUnits('10.5', 6) // 用户输入 "10.5"

  await writeContractAsync({
    address: '0xUSDC_CONTRACT_ADDRESS',
    abi: erc20Abi,
    functionName: 'transfer',
    args: ['0xRecipient', amount],
    account: address,
  })
}
```
