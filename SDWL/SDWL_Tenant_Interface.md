[HOME](Home)

# SDWL Tenant Interface for tenant Information#

```C++
 SDWLResult GetCurrentTenant(ISDRmTenant ** ptenant);
```

## Tenant Interface ##

```
#!c++
	std::wstring GetTenant(void);/// Get Tenant ID string for RMS
	/**
	* @return
	*    Result: tenant string. If no tenant is set, default tenant id will be returned
	*/
```

```
#!c++

	const std::wstring GetRouterURL(void);	/// Get Router URL string for RMS 
	/**
	* @return
	*    Result: Router URL string. if no router url is set, default router url will be returned
	*/
```



```
#!C++

	const std::wstring GetRMSURL(void);/// Get RMS Restful URL associated with Tenant ID and Router URL 
	/**
	* @return 
	*    Result: RMS URL string. empty string if the information is not available
	*/
```