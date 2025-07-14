# useReadContract
Hook for calling a `read-only` function on a contract，and returning the response

A `read-only` function on a Solidity contract is denoted by a `pure` or `view` keyword. They can only read the state of the contract,any cannot make any changes to it. Since read-only methods do not change the state of contract，they do not require any gas to be executed,and can be called by any use without the need to pay for gas.

## parameters

### abi
`Abi | undefined`'  
The contract's Abi 
### account
`Address | undefined`  
Account to use when calling the contract(msg.sender)
### address
`Address | undefined`  
That contract's address
### args
`readonly unknown[] | undefined`
+ Arguments to pass when calling the contract 
+ inferrd from `abi` and  `functionName`
### functionName
`string | undefined`
### blockNumber

### blockHash

### chainId

### ScopeKey





