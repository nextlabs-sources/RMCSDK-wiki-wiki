[HOME](Home.md)
# Session Interface #

## Interfaces ##

> Description: Use router and tenant to get rms address.
> 
> Parameter router: Router url.
> 
> Parameter tenant: Tenant url.
> 
> Parameter completion: Handler for async network result.

```swift
func initTenant(router: String, tenant: String, completion: @escaping (SDMLResult<Any?>) -> Void)
```
> Description: 	Get login url request.
>
> Returns: Request and cookie to insert.

```swift
func getLoginURLRequest() -> SDMLResult<(cookie: String, urlRequest: URLRequest)>
```

> Description: Get register url request and cookie.
> 
> Returns: Request and cookie to insert.

```swift
func getRegisterURLRequest() -> SDMLResult<(cookie: String, urlRequest: URLRequest)>
```

> Description: Set login result.
>
> Parameter cookies: Cookies return from server.
>
> Parameter response: Server returns for login.

```swift
func setLoginResult(cookies: [HTTPCookie], response: String) -> SDMLResult<Any?>
```

> Description: Get tenant instance from cache. Call 'fetchRMS' to create tenant if value is nil.
>
> Returns: Tenant instance.

```swift
func getCurrentTenant() -> SDMLResult<SDMLTenantInterface>
```

> Description: Get user instance from cache. Call 'setLoginResult' to create user if value is nil.
>
> Returns: User instance.

```swift
func getCurrentUser() -> SDMLResult<SDMLUserInterface>
```

> Description: Get protect manager.
> 
> Returns: Protect manager.

```swift
func getProtectManager() -> SDMLResult<SDMLProtectManagerInterface>
```
> Description: Get cache manager.
> 
> Returns: Cache Manager instance.

```swift
func getCacheManager() -> SDMLResult<SDMLCacheManagerInterface>
```
> Description: Get upload manager.
> 
> Returns: Upload manager instance.

```swift
func getUploadManager() -> SDMLResult<SDMLUploadManagerInterface>
```

> Description: Logout current user.
> 
> Parameter completion: nil or error.

```swift
func logout(completion: @escaping (SDMLResult<Any?>) -> ())
```

> Description: Get heartbeat infor.
> 
> Parameter completion: Heartbeat instance.

```swift
func getHeartbeatInfo(completion: @escaping (SDMLResult<SDMLHeartbeatInterface>) -> ())
```

> Description: Get myvalut service.
> 
> Returns: myvault instance.

```swift
func getMyVaultService() -> SDMLResult<SDMLMyVaultInterface>
```

> Description: Get log manager.
> 
> Returns: Log manager instance.

```swift
func getLogManager() -> SDMLResult<SDMLLogManagerInterface>
```