[HOME](Home)
# RMCCore SDK Token interface #
Token class is based on following Restful API from RMS  
[Token service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Token%20REST%20API)  

## Token Interface class definition ##
```
#!c++

namespace RMCCORE {
    class RMToken : public RestfulBase
    {
    public:
        RMToken();
        RMToken(std::string duid, std::string key, unsigned int ml);
        RMToken(JsonObject *value);
        ~RMToken();
        
        RMToken & operator = (const RMToken & rhs);
    public:
        const bool IsInitialized();
        const std::string GetDUID();
        const std::string GetKey();
        const unsigned int GetMaintainLevel();
    public:
        RetValue ImportFromRMSResponse(std::string jsonstr);
   };
 
    class RMTokenPool : public RestfulBase
    {
    public:
        RMTokenPool();
        ~RMTokenPool();
        
    public:
        const size_t size();
	const RMToken pop();
    public:
        RetValue ImportFromString(std::string jsonstr);
        RetValue ImportFromJson(JsonObject * value);
        
        RetValue ImportFromRMSResponse(JsonObject * root);
        RetValue ImportFromRMSResponse(std::string jsonstr);
        
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);
    };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##

## RMToken Interface Functions ##
```
#!c++
	RMToken();/// constructor
	/**
	* @parameter
        *     None. the class will be created as un-initialized.
	*/
```

```
#!c++
	RMToken(std::string duid, std::string key, unsigned int ml)/// constructor with encryption id, key and maintenance level
	/**
	* @param
	*    duid id string to identify encryption key
        *    key  encryption key string
        *    ml   maintenance level return from RMS for encryption key
	*/
```

```
#!C++
	RMToken(JsonObject *value);/// construction with Json object
	/**
	* @param 
	*    value Json Object generated from ExportToJson function
        *    this constructor function is similar with function ImportFromJson inherited from RestfulBase class
	*/
```

```
#!c++
	const bool IsInitialized();/// if the class is initialized
	/**
	* @parameter
        *     None. 
	*/
Note: need call this function to validate the data before use it.
```

```
#!c++
	const std::string GetDUID();/// id for encryption key
	/**
	* @return
	*    string of id for encryption key
	*/
```

```
#!c++
	const std::string GetKey();/// encryption key
	/**
	* @return
	*   string of encryption key
	*/
```

```
#!c++
	const unsigned int GetMaintainLevel();/// maintainance level of encryption key
	/**
	* @return
        *    the value of maintainance value of encryption key
	*/
```

```
#!c++
	RetValue ImportFromRMSResponse(std::string jsonstr);///Import token value return from RMS retrieve token API
	/**
	* @param
        *    jsonstr  Json string returned from RMS Token Interface
	* @return
	*    0 if import successfully.
	*/
Note: ImportFromRMSResponse function only fill in the token key 
```

	
	
## RMTokenPool Interface Functions ##
```
#!c++
	const size_t size();/// Get size of token pool
	/**
	* @return
	*    number of available tokens
	*/
```

```
#!C++
	const RMToken pop();/// retrieve one token from pool
	/**
	* @return 
	*    Token class
	*/
```

```
#!c++
	RetValue ImportFromRMSResponse(JsonObject * root);/// Import tokens from RMS response
	/**
	* @param
        *    root  Json object returned by RMS Token Interface
	*/
```