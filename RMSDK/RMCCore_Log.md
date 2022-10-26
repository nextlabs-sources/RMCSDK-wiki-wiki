[HOME](Home)
# RMCCore SDK Activity Log interface #
Log classes are based on following Restful API from RMS [Log service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Log%20REST%20API)  

## Activity Log Interface class definition ##
```
#!c++

namespace RMSDK {
    class RMActivityLog
    {
    public:
        RMActivityLog(const std::string& nxlduid,    const std::string& fileownerid,    const std::string& userid,  const RMActivityLogOperation operation, const RMSystemPara & param, const std::string& repoId, const std::string& fileId, const std::string& fileName,  const std::string& filePath, const RMActivityLogResult accessResult, const std::string& extraData,  uint64_t accessTime = 0, const RMActivityLogAccountType accountType = RLATPersonal);
        RMActivityLog(JsonString *value);
        ~RMActivityLog();
        
        RMActivityLog & operator = (const RMActivityLog & rhs);
    public:
        const std::string Serialize(void);
        
    public:
        JsonString * ExportToJson(void);
    };
    
    class RMLogPool : public RestfulBase
    {
    public:
        RMLogPool();
        ~RMLogPool();
        
    public:
        const size_t size();
        const std::string ExportLogStringForUpload(unsigned int num =0);

        void AddLog(RMActivityLog & log);
        void Reset(void) ;
    public:
        RetValue ImportFromString(std::string jsonstr);
        RetValue ImportFromJson(JsonObject * value);
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);

        RetValue ImportFromRMSResponse(JsonObject * root);
        RetValue ImportFromRMSResponse(std::string jsonstr);
    };
    class RMNXLFileActivity: public RestfulBase
    {
    public:
        RMNXLFileActivity();
        ~RMNXLFileActivity(){};
    
        RMNXLFileActivity & operator = (const RMNXLFileActivity & rhs);
    public:
        const std::string GetEmail(void);
        const std::string GetOperation(void);
        const std::string GetDeviceType(void);
        const std::string GetDeviceID(void);
        const std::string GetAccessResult(void);
        uint64_t GetAccessTime(void);
    };
    
    class RMNXLFileLogs : public RestfulBase
    {
    public:
        RMNXLFileLogs();
        ~RMNXLFileLogs();
        
    public:
        const size_t size() ;
        const RMNXLFileActivity * GetAt(size_t index);
        
        const std::string GetFileName();
        const std::string GetDUID();
    };
}

```
## [RestfulBase class definition](RestfulBase_Interface) ##

## RMActivityLog Interface Functions ##
```
#!c++
	RMActivityLog(const std::string& nxlduid,    const std::string& fileownerid,    const std::string& userid,  const RMActivityLogOperation operation, const RMSystemPara & param, const std::string& repoId, const std::string& fileId, const std::string& fileName,  const std::string& filePath, const RMActivityLogResult accessResult, const std::string& extraData,  uint64_t accessTime = 0, const RMActivityLogAccountType accountType = RLATPersonal);
        /// constructor
	/**
	* @parameter
        *     nxlduid     nxl file DUID string
        *     fileownerid nxl file owner id string
        *     userid      string of user id for the operation
        *     operation   operation on nxl file
        *     repoId      string of repository id of nxl file
        *     fileName    file name string
        *     filePath    file path string
        *     accessResult The result of nxl file access (deny/allow)
        *     extraData   extra data string (JSON format)
        *     accessTime  time of file operation. (0 mean current time)
        *     accountType where activity is performed  
	*/
```


```
#!C++
	RMActivityLog(JsonValue *value);/// construction with Json String value
	/**
	* @param 
	*    value Json value generated from ExportToJson function
        *    this constructor function is similar with function ImportFromJson inherited from RestfulBase class
	*/
```

```
#!c++
	const std::string Serialize(void);/// serialize activity log to CVS string
	/**
	* @parameter
        *     None. 
	*/
```

```
#!c++
	JsonString * ExportToJson(void);/// Export activity log record to Json String
	/**
	* @return
	*    Json string of Log value in cvs format
	*/

```

## RMLogPool Interface Functions ##
```
#!c++
	const size_t size();/// Get size of log pool
	/**
 	* @return
	*    number of local cached activity logs
	*/
```

```
#!C++
	const std::string ExportLogStringForUpload(unsigned int num =0);/// serialize numbers of logs to CVS string
	/**
	* @parameter
        *     num   number of logs to export. If 0, export all logs.
	* @return 
	*    CVS string of specified log number
	*/
Note: the logs won't be removed after this function.
```
```
#!C++
	void AddLog(RMActivityLog & log);/// Add one activity log to the pool
	/**
	* @parameter
        *     log  A user activity log record
	* @return 
	*     None
	*/
```
```
#!C++
	void Reset(void);///clear all logs in pool
	/**
	* @parameter
        *     None
	* @return 
	*    None
	*/
```
```
#!c++
	RetValue ImportFromRMSResponse(JsonObject * root);/// Import RMS response after upload
	/**
	* @param
        *    root  Json object returned by RMS uploading log Interface
	*/
Note: after receive success from RMS response for log uploading, all export logs will be removed from log pool
```

## RMNXLFileActivity Interface Functions ##
```
#!c++
const std::string GetEmail(void);/// Get email address field
/**
* @parameter
*     None
* @return
*    the string of email address whose owner make the operation
*/
```

```
#!C++
const std::string GetOperation(void);/// Get operation field
/**
* @parameter
*     None
* @return
*    the string of operation on current nxl file
*/

```
```
#!C++
const std::string GetDeviceType(void);/// Get Device Type field
/**
* @parameter
*     None
* @return
*     the string of device type on which make the operation
*/
```
```
#!C++
const std::string GetDeviceID(void);///Get Device ID field
/**
* @parameter
*     None
* @return
*    the string of Device ID (to identify the device)
*/
```
```
#!c++
const std::string GetAccessResult(void);/// Get the result of operation
/**
* @parameter
*     None
* @return
*    the string of result
*/
```
```
#!c++
uint64_t GetAccessTime(void);/// Get operation time
/**
* @parameter
*     None
* @return
*    operation time
*/
```

## RMNXLFileLogs Interface Functions ##
```
#!c++
const size_t size();/// Get nxl file log number
/**
* @return
*    number of nxl file activity logs
*/
```

```
#!C++
const RMNXLFileActivity * GetAt(size_t index);;/// get file activity log
/**
* @parameter
*     index   the index of activity log record (base 0)
* @return
*    RMNXLFileActivity class
*/
```
```
#!C++
const std::string GetFileName();/// Get NXL file name
/**
* @parameter
*     None
* @return
*     the name of nxl file
*/
```
```
#!C++
const std::string GetDUID();/// DUID of the nxl file
/**
* @parameter
*     None
* @return
*    The DUID string of nxl file
*/
```
```
#!c++
RetValue ImportFromRMSResponse(JsonObject * root);/// Import RMS response of query nxl file activity log
/**
* @param
*    root  Json object returned by RMS query log Interface
*/

```