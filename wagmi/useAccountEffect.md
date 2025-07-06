# useAccountEffect
Hook for listening to account lifecycle events

## Usage
```  tsx
import { useAccountEffect } from 'wagmi'
 function APP(){
    useAccountEffect({
        onConntec(data){
            console.log('Connected!', data)
        }，
        onDisconnect(){
            console.log('onDisconnect')
        }
    })
 }

```

