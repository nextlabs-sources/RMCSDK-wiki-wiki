[HOME](Home)
# RMCCore SDK User Interface #
Login related classes, User and membership, are based on following Restful API from RMS
[Login flow for RMC/RMC mobile/Web client](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Login%20REST%20API#markdown-header-basic-login) 


## User Interface class definition ##
```
#!c++

namespace RMSDK {
    class RMUser : public RestfulBase
    {
    public:
        RMUser(const RMSystemPara &sys, const RMTenant & tenant) throw(...);
        RMUser(JsonObject * value) throw(...);
        ~RMUser();      
    public:
        const std::string GetName();
        const std::string GetEmail();
        unsigned int GetIdpType();
        unsigned int GetUserID();
        RMMembership &GetDefaultMembership();
        RMMembership * FindMembership(std::string tenantid);
        
        RMMyDrive * GetMyDrive();
        
        RMUser& operator = (const RMUser& rhs);
    public:
        bool IsLogin();
        bool IsLoginExpired();
        uint64_t	GetExpiredTime();
    public:
        RetValue ProtectLocalFile(const std::string& filepath, const std::string& destfilepath, const NXLAttributes & attrs, RMToken& token, RMActivityLog& activitylog, RMNXLFile& rmnxlfile);
        RetValue ShareLocalFile(const std::string& filepath, const std::string& destfilepath, const NXLAttributes & attrs, const std::vector<std::string>& recipients, RMToken& token, const std::string & comments,
        RMActivityLog& activitylog, RMNXLFile& sharefile);

    public: 

        RetValue ImportFromRMSResponse(JsonObject * root);
    public: //login API
        const HTTPRequest &GetUserLoginURL(void);
        const HTTPRequest &GetUserLogoutQuery(void);
        RetValue Logout(JsonObject * rms_response_root);
    public: //User API
        const HTTPRequest &GetBasicProfileQuery(void);
        const HTTPRequest &GetProfileQuery(void);
	public: //membership API
		const HTTPRequest &GetMembershipQuery(const RMMembership& membership);
    public: //Token API
        const HTTPRequest &GetMembershipTokenQuery(const RMMembership& membership, int tokencount);
        const HTTPRequest &GetFileTokenQuery(const RMNXLFile & file);
    public: //Share API
        const HTTPRequest &GetShareLocalFileQuery(const RMMembership & membership, const RMNXLFile & file);
        const HTTPRequest &GetUpdateRecipientsQuery(const RMNXLFile & file, const RMRecipients &recipients);
    public: //MyVault API
        const HTTPRequest &GetProtectLocalFileQuery(const RMNXLFile & file);
        const HTTPRequest &GetNXLFileMetadataQuery(const RMNXLFile & file);
    public://activity log APIs
        const HTTPRequest &GetUploadActivitylogQuery(RMLogPool*	logpool, int lognum = 0);
        const HTTPRequest &GetNXLFileActivitylogQuery(const RMNXLFile & file, uint64_t startPos, uint64_t count, const RMLogSearchField searchField, const std::string &searchText, const RMLogOrderBy orderByField, bool orderByReverse);
    public://Heartbeat API
        const HTTPRequest &GetHeartBeatQuery(const RMHeartbeat & heartbeat);
        const HTTPRequest &GetProjectUploadFileQuery(unsigned int projid, const std::string &pathid, const std::string &filename, bool nxlfile = true);

    public://inherted functions from RestfulBase
        RetValue ImportFromString(std::string jsonstr);
        RetValue ImportFromJson(JsonObject * value);

        RetValue ImportFromRMSResponse(JsonObject * root);
        RetValue ImportFromRMSResponse(std::string jsonstr);
        
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);
    };
}

```
Note: Import functions of class RMUser also initializes all membership classes belongs to this user.

## [RestfulBase class definition](RestfulBase_Interface) ##
## [HTTPRequest class definition](HttpRequest_Interface) ##

## RMUser Interface Functions ##
	
        
```
#!c++
	RMUser(const RMSystemPara &sys, const RMTenant & tenant) throw(...);/// constructor
	/**
	* @param 
	*    sys    system parameter class 
        *    tenant tenant class for current user login to
        * @exception
        *    function will throw exception if the data in system parameter class or tenant class is not valid 
	*/
```
```
#!c++
	RMUser(JsonObject * value) throw(...); throw(...);/// constructor
	/**
	* @param 
	*    value  Json Object. the Object is exported by function ExporttoJson()
        * @exception
        *    function will throw exception if the data in JsonObject is not valid
	*/
```
```
#!c++
	const std::string GetName();/// Get Login User Name
	/**
	* @return 
	*    user name string
        *    If empty, the class is not initialized property. call import functions to initialize the class
	*/
```

```
#!c++
	const std::string GetEmail();/// Get Login User Email address
	/**
	* @return 
	*    user email address string
        *    If empty, the class is not initialized property. call import functions to initialize the class
	*/
```

```
#!c++

	unsigned int GetIdpType();/// Get login user IDP type 
	/**
	* @return
	*    IDP login type returned from RMS
	*/
```
See [IDP Type defintion](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Login%20REST%20API#markdown-header-display-tenant-specific-login-page)


```
#!C++

	unsigned int GetUserID();/// Get User ID 
	/**
	* @return 
	*    value of User ID. 
        *    If 0, the class is not initialized property. call import functions to initialize the class
	*/
```
```
#!C++

RMMyDrive * GetMyDrive();/// Get current User MyDrive class instance
/**
* @return 
*    Pointer to MyDrive class 
*    If user is not login, return NULL
*/
``` 

        
```
#!C++
	bool IsLogin();/// if user is login at RMS
	/**
	* @return
	*    true if user is login.  
	*/
Note: Call function ImportFromRMSResponse with RMS response from login request.
Note: the return maybe not accurate until function IsLoginExpired called.
```
```
#!C++
	bool IsLoginExpired();/// if current User Login session timeout
	/**
	* @return
	*    true if user session timeout 
	*/
Note: user automatically logout after user session timeout
```
```
#!C++
	uint64_t	GetExpiredTime();/// Get seconds until login session timeout
	/**
	* @return
	*    login session timeout value
	*/
```
```
#!C++
	RetValue Logout(JsonObject * rms_response_root);/// Check RMS User logout restful API return
	/**
	* @return
	*    0 if RMS return success. Otherwise return error code.
	*/
```

     
```
#!c++
	RMMembership &GetDefaultMembership();/// Get login user default membership information
	/**
	* @return
        *    membership class with default membership information
	*/
```
```
#!c++
	RMMembership &FindMembership(std::string tenantid);/// search membership information by tenant id
	/**
	* @param
	*    tenantid   tenant id for membership
	* @return
        *    membership class of search result
	*/
```
## [RMMembership Interface Functions](RMCCore_Membership) ##
```
#!c++
RetValue ProtectLocalFile(const std::string& filepath, const std::string& destfilepath, const NXLAttributes & attrs, RMToken& token, RMActivityLog& activitylog, RMNXLFile& rmnxlfile);
        /// protect local file
	/**
	* @param
	*    filepath   full path of original file need to protect
	*    destfilepath   full path of protected nxl file to generated
	*    attrs      nxl file attributes include obligations, rights, expiry and tags string
	*    tokens     token pool for user membership
    *    activitylog[out]     activity log generated by this function if success.
    *    rmnxlfile[out] RMNXFile class for generated nxl file
    * @return
    *    SUCEESS if success otherwise return error code
	*/
```
```
#!c++
RetValue ShareLocalFile(const std::string& filepath, const std::string& destfilepath, const NXLAttributes & attrs, const std::vector<std::string>& recipients, RMToken& token, const std::string & comments, RMActivityLog& activitylog, RMNXLFile& sharefile);
        /// share local file
	/**
	* @param
	*    filepath   full path of original file need to protect
	*    destfilepath   full path of protected nxl file to generated
    *    attrs      nxl file attributes include obligations, rights, expiry and tags string
    *    tokens     token pool for user membership
    *    recipients list of recipients who are granted rights
    *    comments   comments string for share operation
    *    activitylog[out]     activity log generated by this function if success.
    *    rmnxlfile[out] RMNXFile class for generated nxl file
    * @return
    *    SUCEESS if success otherwise return error code
	*/
```
## [RMNXLFile Interface Functions](RMCCore_RMNXLFile) ##

Developer need retrieve the default membership from user interface and call function below to complete user login
```
#!c

RMMembership.ImportCertficateFromRMSResponse()
```
### RMS User Login related API Functions ###
```
#!C++
	const HTTPRequest &GetUserLoginURL(void);
        /// Get HTTP Request for User Login URL
	/**
	* @param
	*    None
	* @return
	*    HTTPRequest class 
	*/
```
```
#!C++
	const HTTPRequest &GetUserLogoutQuery(void);
        /// Get HTTP Request for User logout URL
	/**
	* @param
	*    None
	* @return
	*    HTTPRequest class 
	*/
```
Please see RMS restful wiki page [Login service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Login%20REST%20API) for all Login related Query

### RMS User related API Functions ###
```
#!C++
const HTTPRequest &GetBasicProfileQuery(void);
/// Get HTTP Request for basic User Profile
/**
* @param
*    None
* @return
*    HTTPRequest class 
*/
```
```
#!C++
const HTTPRequest &GetProfileQuery(void);
/// Get HTTP Request for full User Profile
/**
* @param
*    None
* @return
*    HTTPRequest class 
*/
```
Please see RMS restful wiki page [User service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/User%20REST%20API) for all User related Query

### RMS Membership related API Functions ###
```
#!C++
	 const HTTPRequest &GetMembershipQuery(const RMMembership& membership);
        /// Get HTTP Request for Query Membership certificate URL
	/**
	* @param
        *    membership membership class to query certificate from RMS
	* @return
	*    HTTPRequest class 
	*/
```
Please see RMS restful wiki page [Membership service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Membership%20REST%20API) for all membership related Query

### RMS Token related API Functions ###

```
#!C++
	const HTTPRequest &GetMembershipTokenQuery(const RMMembership& membership, int tokencount);
        /// Get HTTP Request for generate encryption token of specified membership
	/**
	* @param
        *    membership membership class to query certificate from RMS
        *    tokencount number of tokens need generated from RMS
	* @return
	*    HTTPRequest class 
	*/
Note: before calling this function, certificates returned by GetMembershipQuery must be imported to RMMembership class with function ImportCertficateFromRMSResponse()
```
```
#!C++
	const HTTPRequest &GetFileTokenQuery(const RMNXLFile & file);
        /// Get HTTP Request for querying nxl file token
	/**
	* @param
        *    file    NXLFile class with local file information
	* @return
	*    HTTPRequest class 
	*/
```
Please see RMS restful wiki page [Token service](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Token%20REST%20API) for all token related Query

### RMS Sharing related API Functions ###
```
#!C++
	const HTTPRequest &GetShareLocalFileQuery(const RMMembership & membership, const RMNXLFile & file);
        /// Get HTTP Request for Sharing Local File
	/**
	* @param
        *    membership membership class to query certificate from RMS
        *    file       NXLFile class of generated local nxl file
	* @return
	*    HTTPRequest class 
	*/
Note: the request doesn't include the file content and end of boundary string.
Caller need add those data when transfer data to RMS.

```
Please see RMS restful wiki page [sharing local files](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Sharing%20REST%20API#markdown-header-sharing-local-files) for detail of Share Local File Query



```
#!C++
	const HTTPRequest &GetUpdateRecipientsQuery(const RMNXLFile & file, const RMRecipients &recipients);
        /// Get HTTP Request for updating nxl file Recipients list
	/**
	* @param
        *    file         NXL file class which stores the file information
        *    recipient    recipients class which has new/delete recipients list.
	* @return
	*    HTTPRequest class 
	*/
Note: To update the local recipients information, Developer should call Recipient class ImportFromRMSResponse function with the data received from RMS.

```
Please see RMS restful wiki page [update recipients from a document](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Sharing%20REST%20API#markdown-header-update-recipients-from-a-document) for detail of Update Recipients Query

### RMS Log related API Functions ###

```
#!C++
	const HTTPRequest &GetUploadActivitylogReqest(RMLogPool* logpool, int lognum = 0);
        /// Get HTTP Request for uploading local cached activity log
	/**
	* @param
        *    logpool    RMLogPool
        *    lognum     the number of logs will upload to RMS. if 0, upload all local cached logs
	* @return
	*    HTTPRequest class 
	*/

```
```
#!C++
	const HTTPRequest &GetNXLFileActivitylogQuery(const RMNXLFile & file, uint64_t startPos, uint64_t count, const RMLogSearchField searchField, const std::string &searchText, const RMLogOrderBy orderByField, bool orderByReverse);
        /// Get HTTP Request for uploading local cached activity log
	/**
	* @param
        *    file       nxl file class
        *    startPos   the first returned log on sort
        *    count      the maximum log number returned in this query
        *    searchField   see structure RMLogSearchField for field name can be searched.
        *    searchText    the search text in the searching filed above(empty means all values)
        *    orderByField  the ordered by field for return result
        *    orderByReverse flag for return result order
	* @return
	*    HTTPRequest class 
	*/
Note: nxl file must be uploaded before calling this function.

```
Please see RMS restful wiki page [Log Restful API](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Log%20REST%20API) for detail of Log Query

### RMS MyValut related API Functions ###
```
#!C++
	const HTTPRequest &GetProtectLocalFileQuery(const RMNXLFile & file);
        /// Get HTTPRequest to upload protected local file
	/**
	* @param
        *    file   the handle to RMNXLFile class
	* @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
	*/

```

```
#!C++
	const HTTPRequest &GetNXLFileMetadataQuery(const RMNXLFile & file);
        /// Get HTTPRequest for NXL File Metadata info in MyVault
	/**
	* @param
        *    file   the handle to RMNXLFile class
	* @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
	*/
Note: NXL file must be uploaded to RMS, received success return from RMS and imported to RMNXLFile class

```
Please see RMS restful wiki page [File Metadata](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/MyVault%20REST%20API#markdown-header-file-metadata) for detail of get File Metadata request

### RMS Heartbeat related API Functions ###
```
#!C++
	const HTTPRequest &GetHeartBeatQuery(const RMHeartbeat & heartbeat);
        /// Get HTTPRequest for heartbeat request
	/**
	* @param
        *    heartbeat the handle to heartbeat class
	* @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
	*/
```
Please see RMS restful wiki page [Heartbeat API](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Heartbeat%20REST%20API) for detail of heartbeat request

### RMS Project related API Functions ###
```
#!C++
	const HTTPRequest &GetProjectUploadFileQuery(unsigned int projid, const std::string &pathid, const std::string &filename, bool nxlfile = true);
        /// Get HTTPRequest for upload project file request
	/**
	* @param
        *    projid  project id
        *    pathid  path id
        *    filename  file name
        *    nxlfile  if nxl file is true, else false
	* @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
	*/
```