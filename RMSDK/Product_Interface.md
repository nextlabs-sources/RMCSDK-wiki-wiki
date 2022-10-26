[HOME](Home)
# RMCCore Library product interface #
Product class is designed to register current running application.
The application can use following Restful API from RMS for upgrading purpose.
[Check Upgrade REST API](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Check%20Upgrade%20REST%20API)

## Product Interface class definition ##
```
#!c++
namespace RMSDK {
    class RMProduct : public RestfulBase
    {
    public:
        RMProduct(const std::string & productname, uint32_t major_ver, uint32_t minor_ver, uint32_t build_no);
        ~RMProduct(){};
    public:
        void SetAppInfo(const std::string& path, const std::string& publisher);
        RMProduct& operator = (const RMProduct& rhs);
    public:
        const std::string GetVersionString(void) const;
     
        const std::string GetName(void) const;
        const std::string GetPath(void) const;
        const std::string GetPublisherName(void) const;
	public: //API after import RMS response.
        const bool IsNewVersionAvailable(void) const ;
        const std::string GetNewVersionString(void) const ;
        const std::string GetDownloadURL(void) const;
        const std::string GetDownloadChecksum(void) const;	
    public:
        RetValue ImportFromRMSResponse(std::string jsonstr);        
    };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##

## Product Interface Functions ##
```
#!c++
RMProduct(const std::string & productname, uint32_t major_ver, uint32_t minor_ver, uint32_t build_no);  
	/// constructor with product information
/**
* @param
*    productname  string of product name
*    major_ver    product major version information
*    minor_ver    product minor version information
*    build_no     product build number information
*/
Note: the version string format(major.minor.build) is used to send version information to RMS Check Upgrade API
```

```
#!c++
 void SetAppInfo(const std::string& path, const std::string& publisher);/// Set product application information
/**
* @param
*    path  		the installation path of product
*    publisher	publisher string of product
* @return
*    None
*/
Note: this function is optional
```

```
#!c++
const std::string GetVersionString(void) const;	/// Get product version string 
/**
* @return
*    Result: version string based on major, minor and build number 
*/
```

```
#!C++
const std::string GetName(void) const;/// Get Product Name string
/**
* @return 
*    Product Name string initialized from constructor or Import by RestfulBase functions.
*/

```

```
#!c++
const std::string GetPath(void) const;/// Get Application installation path
/**
* @return
*    Application path if set by function SetAppInfo.
*/
```

```
#!c++
const std::string GetPublisherName(void) const;/// Get Application publisher information
/**
* @return
*    Application publisher information if set by function SetAppInfo
*/
```

```
#!c++
RetValue ImportFromRMSResponse(std::string jsonstr)/// Import Check Update REST API return from RMS response
/**
* @param
*    String of json string receive from RMS.
*/
Note: Call function GetProductUpdateQuery() in RMTenant class to get HTTP Request for Check Update REST API
```

```
#!c++
const bool IsNewVersionAvailable(void) const ;/// If there is new version available 
/**
* @return
*    true if there is new version available from RMS. Call following functions to get more information
*/
```

```
#!C++
const std::string GetNewVersionString(void) const ;/// Get New version string
/**
* @return 
*    New version string of package available on server
*/
Note: the information only available after ImportFromRMSResponse is called.
```
```
#!C++
const std::string GetDownloadURL(void) const; //Get download URL string
/**
* @return 
*    New version package URL on server
*/
Note: the information only available after ImportFromRMSResponse is called.
```

```
#!C++
const std::string GetDownloadChecksum(void) const;/// Get new package SHA1 checksum string
/**
* @return 
*    The SHA1 checksum string of new package for verification after download. 
*    return empty string if information is not available
*/
Note: the information may not available for all packages. 
```
