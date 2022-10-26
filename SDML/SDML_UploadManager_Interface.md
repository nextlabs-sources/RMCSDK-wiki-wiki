[HOME](Home.md)
# Upload Manager Interface #


## Interfaces ##
>Description: 	Upload File.
>
>parameter file: [nxl file interface](SDML_NXLFile_Interface.md).
>
>parameter progress: upload progress.
>
>parameter completion: finish or error.
>
>Returns: uuid for cancel.

```Swift
func upload(file: SDMLNXLFileInterface, progress: @escaping (Double) -> (), completion: @escaping (SDMLResult<Any?>) -> ()) -> String
```
>description: Cancel upload.
>
>parameter id: upload id.
>
>Returns: success or fail.

```Swift
func cancel(id: String) -> Bool
```
