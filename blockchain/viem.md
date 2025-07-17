# Viem 

## encodeFunctionData
自动生成`data`字段，处理函数选择器和参数编码

```
import { ecodeFunctionData } from 'viem'
import  { erc20Abi } from 'viem'

const data = ecodeFunctionData({
    abi: erc20Abi,
    functionName:'balanceOf',
    args: ['0xc0ffee254729296a45a3885639AC7E10F9d54979']
})
console.log(data)
```


## decodeFunctionResult
解码合约返回值,(通常用于eth_call的结果)

```
import { decodeFunctionResult } from 'viem'
import  { erc20Abi } from 'viem'


const result = decodeFunctionResult({
    abi: erc20Abi,
    functionName:'balanceOf',
    data: '0x00000000000000000000000000000000000000000000000000000000000003e8'
})
console.log(result)
// => [1000n]

```


## decodeFunctionData

```
import { decodeFunctionData } from 'viem'

const callData = '0x70a08231000000000000000000000000c0ffee254729296a45a3885639ac7e10f9d54979'

const decoded = decodeFunctionData({
  abi,
  data: callData,
})

console.log(decoded)
/*
{
  functionName: 'balanceOf',
  args: ['0xc0ffee254729296a45a3885639ac7e10f9d54979']
}
*/

```

## parseEther
把人类可读的ETH转换为wei(BigInt)
```
parseEther('0.1')
// 100000000000000000n

```
## formatEther
把`wei`(`BigInt`)转换为ETH(字符串)
```
formatEther(100000000000000000n)
// '0.1'
```

## parseUnits
通用转换，按任意小数位转换为`BigInt`
```
parseUnits('1.5',6)
// 1500000n
```

## formatUnits
通用格式化，按任意小数位转换为字符串
```
formatUnits(1500000n,6)
// 1.5
```

