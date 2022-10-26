[HOME](Home)
# RMCCore Heartbeat interface #
Heartbeat class is based on following Restful API from RMS
[Heartbeat REST API](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Heartbeat%20REST%20API)

## Heartbeat Interface class definition ##
```
#!c++
namespace RMSDK {
    class RMPolicyConfig : public RestfulBase
    {
    public:
        RMPolicyConfig();
        ~RMPolicyConfig(){};
    
        RMPolicyConfig& operator = (const RMPolicyConfig& rhs);
    public:
        const std::string &GetPolicyBundle();
        bool HasWatermarkPolicy();
        const Watermark &GetWatermarkConfig();
        uint64_t GetPolicyLastModify();
        uint64_t GetPolicyBundleTimeStamp();
    };

    class RMHeartbeat : public RestfulBase
    {
    public:
        RMHeartbeat();
		~RMHeartbeat() {};
    public:
        uint32_t GetFrequency(void);
        const Watermark & GetDefaultWatermarkSetting(void);
        
		size_t GetPolicyConfigCount();
		const std::string GetPolicyConfigTenantID(int index);
		bool GetPolicyConfig(const std::string & tenantid, RMPolicyConfig & config);

    public:
        RetValue ImportFromRMSResponse(std::string jsonstr);
    };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##

## Policy Configuration Interface Functions ##
PolicyConfig is part of Heartbeat configuration return from RMS
```
#!c++
	RMPolicyConfig();/// constructor 
	/**
	* @param
	*    NULL
	*/
```

```
#!c++
	const std::string &GetPolicyBundle();/// Get Policy Bundle in configuration
	/**
	* @return
	*    Policybundle string
	*/
```

```
#!c++

	bool HasWatermarkPolicy();/// if current configuration has watermark setting
	/**
	* @return
	*    true if there is watermark setting in configuration
	*/
```


```
#!C++
	const Watermark &GetWatermarkConfig();///Get Watermark setting 
	/**
	* @return 
	*    Watermark configuration 
	*/
```

```
#!c++
	uint64_t GetPolicyLastModify();///Get last modify time on policy
	/**
	* @return
	*    last modify time when the configuration is updated.
	*/
```

```
#!c++
	uint64_t GetPolicyBundleTimeStamp();///Get last update time of policy bundle
	/**
	* @return
	*    last time when the policy bundle is updated
	*/
```

## RMHeartbeat Interface Functions ##
```
#!c++
	RMHeartbeat();/// constructor 
	/**
	* @param
	*    NULL
	*/
```

```
#!c++
	uint32_t GetFrequency(void);/// Get heart beat frequency setting
	/**
	* @return
	*    the time for next heartbeat with RMS (seconds)
	*/
```

```
#!c++

	const Watermark & GetDefaultWatermarkSetting(void);/// the watermark setting for current user
	/**
	* @return
	*    watermark setting
	*/
```


```
#!C++
	size_t GetPolicyConfigCount();///Get Policy Configuration number in current setting
	/**
	* @return 
	*    number of policy configuration 
	*/
```

```
#!c++
	const std::string GetPolicyConfigTenantID(int index);///Get tenantid of PolicyConfig 
	/**
	* @param
	*    index	0 based index of PolicyConfig
	* @return
	*    TenantID string
	*/
```

```
#!c++
	bool GetPolicyConfig(const std::string & tenantid, RMPolicyConfig & config);///Get PolicyConfig class
	/**
	* @param
	*    tenantid		tenant id string
	*    config[out]	PolicyConfig class which has same tenantid	
	* @return
	*    true if tenantid is found and configuration returned. false if no PolicyConfig for specified tenantid 
	*/
```

```
#!c++
RetValue ImportFromRMSResponse(std::string jsonstr)/// Import heartbeat query return from RMS response
/**
* @param
*    String of json string receive from RMS.
*/
Note: For related HTTP helper see GetHeartBeatQuery() function in RMUser class.
```