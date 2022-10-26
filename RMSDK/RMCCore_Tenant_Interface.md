[HOME](Home)
# RMCCore Library tenant interface #
Tenant class is based on following Restful API from RMS    
[Login flow for RMC/RMC mobile/Web client](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Login%20REST%20API#markdown-header-login-flow-for-rmcrmc-mobileweb-client)    
[Check for Update Request/Response](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Check%20Upgrade%20REST%20API)

## Tenant Interface class definition ##
```
#!c++

namespace RMSDK {
    class RMTenant: public RestfulBase
    {
    public:
        RMTenant(const std::string router = "", const std::string tenant = "");
        ~RMTenant();
    public:
        const std::string GetTenant(void);
        const std::string GetRouterURL(void);
        const std::string GetRMSURL(void); 
    public:
        void SetTenant(const std::string tenant);
        void SetRouter(const std::string router);
        
        RMTenant& operator = (const RMTenant& rhs);
    public: //functions inherit from RestfulBase
        RetValue ImportFromJson(JsonObject * value);
        RetValue ImportFromString(std::string jsonstr);
        RetValue ImportFromRMSResponse(JsonObject * root);
        RetValue ImportFromRMSResponse(std::string jsonstr);
        
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);
    public: //tenant REST API
        const HTTPRequest &GetTenantQuery(void);
	public: //Check for Update REST API
        const HTTPRequest &GetProductUpdateQuery(const RMSystemPara & para);
  };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##
## [HTTPRequest class definition](HttpRequest_Interface) ##

## Tenant Interface Functions ##
```
#!c++
RMTenant(const std::string router = "", const std::string tenant = "");  
	/// constructor with router and tenant information
/**
* @param
*    router  router string. If empty, default router will be used.
	*    tenant  tenant id string. If empty, default tenant id will be used.
*/
```

```
#!c++
std::string GetTenant(void);/// Get Tenant ID string for RMS
/**
* @return
*    Result: tenant string. If no tenant is set, default tenant id will be returned
*/
```

```
#!c++
const std::string GetRouterURL(void);	/// Get Router URL string for RMS 
/**
* @return
*    Result: Router URL string. if no router url is set, default router url will be returned
*/
```



```
#!C++
const std::string GetRMSURL(void);
	/// Get RMS Restful URL associated with Tenant ID and Router URL 
/**
* @return 
*    Result: RMS URL string. empty string if the information is not available
*/
Note: RMSURL value can only be initialize by import functions
```

```
#!c++
void SetTenant(const std::string tenant);/// set Tenant ID string
/**
* @param
*    tenant  tenant id string. If empty, default tenant id will be used.
*/
```

```
#!c++
void SetRouter(const std::string router);/// set Tenant ID string
/**
* @param
*    router  router string. If empty, default router will be used.
*/
```

```
#!c++
const HTTPRequest &GetTenantQuery(void);/// Get HTTP Request for query RMS URL
/**
* @return
*    HTTPRequest class 
*/
```

```
#!c++
const HTTPRequest &GetProductUpdateQuery(const RMSystemPara & para);/// Get HTTP Request for query auto upgrade package on RMS
/**
* @param
*    para  System parameters
* @return
*    HTTPRequest class 
*/
Note: call ImportFromRMSResponse function in RMProduct class to import RMS return
```