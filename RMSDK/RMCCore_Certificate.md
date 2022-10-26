[HOME](Home)
# RMCCore SDK Certificate interface #
Certificate class is based on following Restful API from RMS   
[Membership service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Membership%20REST%20API)

## Certificate Interface class definition ##
```
#!c++

namespace RMSDK {
    typedef std::vector<uint8_t> RMAgreement;
    
    class RMCertificate : public RestfulBase
    {
    public:
        RMCertificate();
        ~RMCertificate();
        
    public:
        RMCertificate& operator = (const RMCertificate& rhs);
        
        const RMAgreement GetAgreement0();
        const RMAgreement GetAgreement1();
        
    public:
        RetValue ImportFromRMSResponse(JsonObject * root);
        RetValue ImportFromRMSResponse(std::string jsonstr);

    public:
        RetValue ImportFromString(std::string jsonstr);
        RetValue ImportFromJson(JsonObject * value);
        
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);
    };
```
## [RestfulBase class definition](RestfulBase_Interface) ##

## Certificate Interface Functions ##
```
#!c++
	RMCertificate()/// constructor 
	/**
	* @param
	*    None. Certificate class can be only initialized by function ImportFromRMSResponse
	*/
```

```
#!C++
	const RMAgreement GetAgreement0()/// Get first agreement
	/**
	* @return 
	*    agreement which used to communicate with RMS in future.
        *    If vector size is zero, not valid certificate
	*/
```

```
#!C++
	const RMAgreement GetAgreement1()/// Get second agreement
	/**
	* @return 
	*    agreement which used to communicate with RMS in future.
        *    If vector size is zero, not valid certificate
	*/
```

```
#!c++
	RetValue ImportFromRMSResponse(JsonObject * root)/// Import certificate information
	/**
	* @param
	*    Json return from RMS Membership API
	*/
Note: Developer need call this function to finished the initialize of Membership class

```