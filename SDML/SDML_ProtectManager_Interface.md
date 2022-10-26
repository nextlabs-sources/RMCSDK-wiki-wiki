[HOME](Home.md)
# Protect Manager Interface #


## Interfaces ##
>Description: 	Protect origin file to server.
>
>parameter path: Origin file path.
>
>parameter rights: e.g 'view'...
>
>parameter completion: [nxl file interface](SDML_NXLFile_Interface.md) or error.

```Swift
func protectOriginFile(path: String, rights: [SDMLFileRight], completion: @escaping (SDMLResult<SDMLNXLFileInterface>) -> ())
```
>description: Share origin file to server.
>
>parameters:
>
>path: Origin file path.
>
>recipients: 'xxx'
>
>rights: e.g 'view'...
>
>watermark: Watermark.
>
>expiredTime: When to expired.
>
>comment: Comment word.
>
>completion: Cache file struct or error.

```Swift
func shareOriginFile(path: String, recipients: [String], rights: [SDMLFileRight], watermark: String, expiredTime: Date, comment: String, completion: @escaping (SDMLResult<SDMLNXLFileInterface>) -> ())
```
