[HOME](Home.md)
# Log Manager Interface #


## Interfaces ##
>Description: 	Get nxl file activity logs.
>
>parameter file: [nxl file interface](SDML_NXLFile_Interface.md).
>
>Returns: Logs or error.

```Swift
func getActivityLog(file: SDMLNXLFileInterface) -> SDMLResult<[SDMLActivityLogInterface]>
```

>Description: 	Add log.
>
>Parameter file: NXL file.(SDML_NXLFile_Interface.md).
>
>Parameter log: log to add.
>
>Parameter completion: nil or error.
>

```Swift
func addLog(file: SDMLNXLFileInterface, log: SDMLActivityLogInterface, completion: @escaping (SDMLResult<Any?>) -> ())
```
