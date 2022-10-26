[HOME](Home.md)
# FileService Interface #


## Interfaces ##
>Description: 	Decrypt file to folder.
>
>Parameter:
>
>path: Local path.
>
>toFolder: The folder to store decrypt file.
>
>isOverwrite: Overwrite file or not.
>
>completion: Decrypt path or error.

```Swift
func decryptFile(path: String, toFolder: String, isOverwrite: Bool, completion: @escaping (SDMLResult<String>) -> ())
```

>Description: 	Share recipients.
>
>Parameter:
>
>path: Local path.
>
>newRecipients: New recipients.
>
>completion: Success or fail.

```Swift
func reshare(path: String, newRecipients: [String], completion: @escaping (SDMLResult<Any?>) -> ())
```

>Description: 	Check rights.
>
>Parameter:
>
>path: Local path.
>
>completion: If success, return isOwner and file rights.

```Swift
func checkRight(path: String, completion: @escaping (SDMLResult<(isOwner: Bool, rights: [SDMLFileRight])>) -> ())
```

>Description: 	Get meta data.
>
>Parameter:
>
>path: Local path.
>
>completion: Get file info.

```Swift
func getMetadata(path: String, completion: @escaping (SDMLResult<SDMLNXLFileInterface>) -> ())
```
