[HOME](Home)
# RMCCore SDK MyDrive interface #
Tenant class is based on following Restful API from RMS
[RMS MyDrive REST API](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/MyDrive%20REST%20API#markdown-header-get-storage-used)

## MyDrive Interface class definition ##
```
#!c++

namespace RMSDK {
class RMMyDrive : public RestfulBase
{
public:
RMMyDrive();
~RMMyDrive();

public:
uint64_t GetUsage(void);
uint64_t GetQuota(void);

public: //function inherit from RestfulBase
RetValue ImportFromRMSResponse(std::string jsonstr);
public://MyDrive API
const HTTPRequest &GetStorageQuery(void);
};
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##
## [HTTPRequest class definition](HttpRequest_Interface) ##

## MyDrive Interface Functions ##
Note: MyDrive class instance can be only obtained from RMUser class. 
```
#!c++
RMMyDrive(); /// constructor 
/**
* @param
*    NULL
*/
```

```
#!c++
uint64_t GetUsage(void);/// Get My Drive Usage
/**
* @return
*    the bytes used at MyDrive
*/
```

```
#!C++

uint64_t GetQuota(void);/// Get My Drive Total Quota
/**
* @return 
*    total storage size for My Drive
*/
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
RetValue ImportFromRMSResponse(std::string jsonstr)/// Import query storage return from RMS response
/**
* @param
*    String of json string receive from RMS.
*/
Note: Mydrive storage and quota data only be availabe after import RMS response.
```

```
#!c++
const HTTPRequest &GetStorageQuery(void);/// Get HTTP Request to query MyDrive storage
/**
* @return
*    HTTPRequest class 
*/
```
