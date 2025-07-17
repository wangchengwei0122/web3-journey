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
```
 async function getChainId() {
  const chainId = await window.ethereum.request({
    method: 'eth_chainId',
  })
  console.log('当前链 ID:', parseInt(chainId, 16))
}
```
4. `eth_getBalance`
```
async function getBalance() {
  const accounts = await window.ethereum.request({ method: 'eth_accounts' })
  const balance = await window.ethereum.request({
    method: 'eth_getBalance',
    params: [accounts[0], 'latest'],
  })
  console.log('余额（Wei）:', BigInt(balance))
}
```
5. `eth_call`
```
async function callContractRead() {
  const contractAddress = '0xYourContractAddress'
  const userAddress = '0xUserAddress'
  const functionSelector = '0x70a08231' // balanceOf(address) 的函数选择器

  const data = functionSelector + userAddress.slice(2).padStart(64, '0')

  const result = await window.ethereum.request({
    method: 'eth_call',
    params: [
      {
        to: contractAddress,
        data: data,
      },
      'latest',
    ],
  })

  console.log('代币余额:', BigInt(result))
}
```
6. `eth_sendTransaction`
```
async function sendTransaction() {
  const accounts = await window.ethereum.request({ method: 'eth_accounts' })
  const txHash = await window.ethereum.request({
    method: 'eth_sendTransaction',
    params: [
      {
        from: accounts[0],
        to: '0xReceiverAddress',
        value: '0x2386F26FC10000', // 0.01 ETH = 10^16 Wei
      },
    ],
  })

  console.log('交易已发送，哈希：', txHash)
}
```
7. `eth_blockNumber`
```
async function getBlockNumber() {
  const blockNumberHex = await window.ethereum.request({
    method: 'eth_blockNumber',
  })
  console.log('最新区块号:', parseInt(blockNumberHex, 16))
}
```
