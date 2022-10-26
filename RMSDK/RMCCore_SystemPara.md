[HOME](Home)
# RMCCore SDK System Parameters interface #
SystemPara class is based on following Restful API from RMS
[Common Parameters for REST API](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Common%20Parameters%20for%20REST%20API)


## System Parameters Interface class definition ##
The System Parameters class is device base which saves system related information.
It is expected to be only created once at each device then caller serialized data by calling export/import functions 

```
#!c++
namespace RMSDK {
    class RMSystemPara : public RestfulBase
    {
    public:
	RMSystemPara();
        ~RMSystemPara();
    public:
        const std::string GetClientID(void);
        const std::string GetDeviceID(void);
        const RMPlatformID GetPlatformID(void);
        const std::string GetAppName(void);
        const std::string GetAppPath(void);
        const std::string GetAppPublisherName(void);
    public:
        void SetPlatformID(RMPlatformID id);
        void SetDeviceID(const std::string deviceid);
        void SetAppInfo(const std::string& name, const std::string& path, const std::string& publisher);
        
	RMSystemPara& operator = (const RMSystemPara& rhs);
    };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##

## System Parameters Interface Functions ##
```
#!c++
	RMSystemPara(); /// constructor
	/**
	* @param
	*    None
	*/
Note: the constructor will generate client ID automatically. For other parameters, like device name, caller should call the related functions to set it.
```

```
#!c++
	const std::string GetDeviceID(void);/// Get Device ID string for current system
	/**
	* @return
	*    device Id string.
	*/
```

```
#!c++
	const RMPlatformID GetPlatformID(void);/// Get Platform ID value for current system
	/**
	* @return
	*    enum value of platform for current system
	*/
```
Note: see wiki page [Predefined Platform](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMD/platform.md) for the detail pre-defined platform value

```
#!c++
	const std::string GetAppName(void);/// Get Application Name
	/**
	* @return
	*    the name of application which is using SDK
	*/
```
```
#!c++
	const std::string GetAppPath(void);/// Get Application Path
	/**
	* @return
	*    the full path of application which is using SDK
	*/
```
```
#!c++
	const std::string GetAppPublisherName(void);/// Get Application publisher Name
	/**
	* @return
	*    the name of publisher who release the application using SDK
	*/
```
```
#!c++
	void SetPlatformID(RMPlatformID id);/// Update current platform ID
	/**
	* @return
	*    None. function won't validate the value passed in. 
        *    the value will be sent to RMS for validation and error handle
	*/
```

```
#!c++
	void SetDeviceID(const std::string deviceid);/// set Device ID string
	/**
	* @return
        *    None. If string is empty, the value won't be set.
	*/
```
```
#!c++
	void SetAppInfo(const std::string& name, const std::string& path, const std::string& publisher);
        /// set Application information
	/**
	* @param
        *    name    the name of application
        *    path    the installation path of application
        *    publish the publisher name of application
	* @return
        *    None
	*/
```