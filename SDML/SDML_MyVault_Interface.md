[HOME](Home.md)
# MyVault Interface #


## Interfaces ##
>Description: 	Get file name.
>
>Parameter completion: Return usage and quota.
>
```Swift
func getStorage(completion: @escaping (SDMLResult<(usage: UInt, quota: UInt)>) -> ())
```
