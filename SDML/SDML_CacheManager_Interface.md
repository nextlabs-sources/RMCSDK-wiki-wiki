[HOME](Home.md)
# Cache Manager Interface #


## Interfaces ##
>Description: 	Get all file under cache folder.
>
>Parameter parentPath: parentPath, if root use "/".
>
>Returns: [nxl file](SDML_NXLFile_Interface.md) or [folder](SDML_BaseFile_Interface.md).

```Swift
func getFiles(parentPath: String) -> SDMLResult<[SDMLBaseFileInterface]>
```

>Description: 	Get file from name.
>
>Parameter name: File name.
>
>Returns: Basefile or error.

```Swift
func searchFile(containName: String) -> SDMLResult<[SDMLBaseFileInterface]>
```

>Description: 	Delete file in cache.
>
>Parameter file: Cache file struct.
>
>Returns: nil or error.

```Swift
func deleteFile(file: SDMLNXLFileInterface) -> SDMLResult<Any?>
```
>Description: 	Decrypt cahce file to folder.
>
>Parameter file: File struct.
>
>Parameter toFolder: Where decrypt file store.
>
>Parameter isOverwrite: Overwrite file or not.
>
>Parameter completion: Decrypt path or error.
>

```Swift
func decryptFile(file: SDMLNXLFileInterface, toFolder: String, isOverwrite: Bool, completion: @escaping (SDMLResult<String>) -> ())
```
>Description: 	Share recipients.
>
>Parameters:
>
>file: Nxl file.
>
>newRecipients: New recipients.
>
>completion: Success or fail.

```Swift
func reshare(file: SDMLNXLFileInterface, newRecipients: [String], completion: @escaping (SDMLResult<Any?>) -> ())
```
