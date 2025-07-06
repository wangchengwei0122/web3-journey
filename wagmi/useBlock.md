# useBlock
 Obtain the block information 
## parameter
### blockHash
#### blockHash
  `0x{string}`




## return Type
### hash
`ox{string}`

### number

### parentHash

### chainId
 





## Usage
``` tsx
 improt { useBlock } from 'wagmi'
 function App(){
  const block = useBlock({
    blockNumber: 'xxx'
  })
  return null
 }
 
```


## Todo
1. 通过useBlockNumber 和 useTranscationRecipe 显示进度条
2. 



