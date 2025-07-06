# useAccount
 
### parameters
#### config 
`Config | undefined`  
In most case,this parameter does not need to be configured
### returnType

#### address 
`Address | undefined`  
Connected addresses from connector   
Defaults to first address in addresses 
#### addresses 
`readlony Address[] | undefined`  
Connected addresses from connector 
#### chain
`Chain | undefined`  
Connected chain from connector.If chain is not configured by config，it will be  **undefined**

#### chainId
`number | undefined`  
Connected chain id from connector 

#### connector
`Connector | undefined`  
Connected connector

#### isConnecting/isReconnecting/isConnected/isDisconnected
`boolen`  
Boolen variables derived from status

#### status
`'connecting'|'reconnecting'|'connected'|'disconnected'`  
 + connected 已经连接
 + connecting 正在连接
 + reconnecting: attempting to re-establish connection to one or more connectors
 + disconnected: no connection to any connector


### Usage

``` tsx
 import { useAccount } from 'wagmi'

 function App(){
    const { address, addresses,status} = useAccount()

    console.log(address)   // 0x14dC79964da2C08b23698B3D3cc7Ca32193d9955
    console.log(addresses)  // [0x14dC79964da2C08b23698B3D3cc7Ca32193d9955]
    console.log(status) // 'connecting'|'reconnecting'|'connected'|'disconnected'
    
    return null
 }

```







