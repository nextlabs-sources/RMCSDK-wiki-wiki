[HOME](Home)
# RMCCore SDK Membership interface #
Membership class is based on following Restful API from RMS  
[Login flow for RMC/RMC mobile/Web client](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Login%20REST%20API#markdown-header-basic-login)  
[Membership service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Membership%20REST%20API)

## Membership Interface class definition ##
```
#!c++

namespace RMSDK {
    class RMMembership : public RestfulBase
    {
    public:
        RMMembership();
        ~RMMembership();
        
    public:
        const std::string GetID();
        const std::string GetTenantID();
        unsigned int GetIdpType();
        unsigned int GetProjectID();
        
        RMMembership& operator = (const RMMembership& rhs);
        
    public:
        RetValue ImportFromString(std::string jsonstr);
        RetValue ImportFromJson(JsonObject * value);
        
        RetValue ImportFromRMSResponse(JsonObject * obj);
        RetValue ImportFromRMSResponse(std::string jsonstr);
        
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);
    public:
        RMCertificate   m_certificate; //certificate class to communicate with RMS
    };
}


```
## [RestfulBase class definition](RestfulBase_Interface) ##

## Membership Interface Functions ##
```
#!c++
	RMMembership();;/// constructor 
	/**
	* @param
	*    None. Membership can be only initialized by function ImportFromRMSResponse
	*/
```

```
#!C++
	const std::string GetID();/// Get membership ID string
	/**
	* @return 
	*    string of membership ID 
        *    If empty, not valid membership
	*/
```

```
#!c++
	const std::string GetTenantID();/// Get membership Tenant ID string
	/**
	* @return
        *    string of tenant ID of current membership
        *    If empty, not valid membership
	*/
```

```
#!c++
	unsigned int GetIdpType();/// Login IDP type of current membership
	/**
	* @return
	*    IDP login type returned from RMS
	*/
```

```
#!c++
	unsigned int GetProjectID();/// Project ID that the membership belongs to
	/**
	* @return
	*    Project ID
	*/
```

```
#!c++
	RetValue ImportFromRMSResponse(JsonObject * obj)/// Import login user membership information
	/**
	* @param
        *    Json object which point to membership array.
	*/
Note: Developer doesnot need to call this function to import login user information.  
    this function will be called implicit when import RMS response at User interface
```

```
#!c++
	RetValue ImportFromRMSResponse(std::string jsonstr)/// Import login user membership information
	/**
	* @param
        *    String which point to membership array.
	*/
Note: Developer doesnot need to call this function to import login user information.  
    this function will be called implicit when import RMS response at User interface
```