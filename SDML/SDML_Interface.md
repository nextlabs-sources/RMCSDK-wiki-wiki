[HOME](Home.md)
# SDML Library Interface #


## Interfaces ##
>Description: 	This function returns the version number of the framework.
>
>Returns: 	The format of version is *major.minor*.

```Swift
func getVersion() -> String
```
>Description: 	This function creates an instance of session.
>
>Parameters:	mark	Use  to distinguish different sessions.
>
>Returns:		If success, get instance, else catch error. 
>
>**Note: *deleteInstancemust* be called to delete this instance !!! Otherwise, it will cause memory leak.**

```swift
func createInstance(mark: String? = nil) -> SDMLResult<SDMLSessionInterface>
```
>Description: 	Use to delete session instance.
>Parameters: 	Session instance.

```swift
func deleteInstance(session: inout SDLSessionInterface?)
```

