## Whta's the Wallet

钱包是用于管理私钥和签名交易的工具，它有两个核心功能
+ 身份认证： 证明你拥有某个地址的私钥
+ 交易签名与发送： 构造交易、签名、并且通过RPC发送给区块链网络

## What's the `window.ethereum`
When you install the `MateMask`，the page will inject an object
```
window.ethereum
```
we can use `window.ethereum` interact with blockchain by `JSON-RPC`

1. `eth_requestAccounts` connect wallet  
```
async function connectWallet() {
const accounts = await window.ethereum.request({
    method: 'eth_requestAccounts',
})
console.log(accounts[0]) // 
}
``` 
2. `eth_accounts` get currently address 
```
async function getAccounts() {
  const accounts = await window.ethereum.request({
    method: 'eth_accounts',
  })
  console.log('当前地址:', accounts[0])
}
``` 
3. `eth_chainId`