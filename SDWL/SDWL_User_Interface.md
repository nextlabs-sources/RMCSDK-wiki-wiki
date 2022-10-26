[HOME](Home)

# SDWL User Interface #
To obtain user interface handler, Call [Session Interface](SDWL_Session_Interface) function
```C++
SDWLResult SetLoginResult(std::string jsonreturn, ISDRmUser **puser);
```

## User Class ##

Application call user class to protect, decrypt, share, upload and download files. User calss can get ad-hoc or central policy information.

```
#!c++

class ISDRmUser    
{
public:
const std::wstring GetName();
const std::wstring GetEmail();
USER_IDPTYPE GetIdpType();
SDWLResult LogoutUser() ;

SDWLResult GetMyDriveInfo(uint64_t& usage, uint64_t& totalquota, uint64_t& vaultusage, uint64_t& vaultquota);
const std::string GetPasscode() ;
SDWLResult UpdateUserInfo() ;
std::vector<SDR_PROJECT_INFO>& GetProjectsInfo();

SDWLResult ProtectFile(const std::wstring filepath, const std::vector<SDRmFileRight> rights, SDR_WATERMARK_INFO watermarkinfo, SDR_Expiration expire, const std::string& tags="", const std::string& memberid="");
SDWLResult ShareFile(const std::wstring filepath, const std::vector<SDRmFileRight> rights, const std::vector<std::string> recipientsemail, const std::wstring & comments, SDR_WATERMARK_INFO watermarkinfo, SDR_Expiration expire, const std::string& tags="", const std::string& memberid="");
SDWLResult GetRecipients(ISDRmNXLFile * nxlfile, std::vector<std::string> &recipientsemail, std::vector<std::string> &addrecipientsemail, std::vector<std::string> &removerecipientsemail);
SDWLResult UpdateRecipients(ISDRmNXLFile * nxlfile, const std::vector<std::string> addrecipientsemail, const std::vector<std::string> removerecipientsemail);

SDWLResult GetLocalFileManager(ISDRFiles** pFile);
SDWLResult UploadFile(ISDRmNXLFile* file);
SDWLResult OpenFile(std::wstring nxlfilepath, ISDRmNXLFile ** file);

SDWLResult DecryptNXLFile(ISDRmNXLFile * file, std::wstring targetfilepath, SRMActivityLogOperation purpose);
SDWLResult UploadActivityLogs();
SDWLResult GetNXLFileActivitylog(ISDRmNXLFile * file, uint64_t startPos, uint64_t count, uint8_t searchField, const std::string &searchText, uint8_t orderByField, bool orderByReverse);
SDWLResult GetActivityInfo(std::wstring fileName, std::vector<SDR_FILE_ACTIVITY_INFO>& info);
SDWLResult GetListProjects(uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& searchValue, PROJECT_FILTER filter);
SDWLResult ProjectDownloadFile(const unsigned int projectid, const std::wstring& pathid, const std::wstring& downloadPath, bool bviewonly);
};
SDWLResult GetProjectListFiles(uint32_t projectId, uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& pathId, const std::string& searchString, std::vector<SDR_PROJECT_FILE_INFO>& listFiles);
SDWLResult GetRights(const std::wstring& nxlfilepath, std::vector<std::pair<SDRmFileRight, std::vector<SDR_WATERMARK_INFO>>> &rightsAndWatermarks);
SDWLResult GetFileRightsFromCentralPolicies(const std::wstring& nxlFilePath, std::vector<std::pair<SDRmFileRight, std::vector<SDR_WATERMARK_INFO>>> &rightsAndWatermarks);
SDWLResult GetResourceRightsFromCentralPolicies(const std::wstring& resourceName, const std::wstring& resourceType, const std::vector<std::pair<std::wstring, std::wstring>> &attrs, std::vector<std::pair<SDRmFileRight, std::vector<SDR_OBLIGATION_INFO>>> &rightsAndObligations);
SDWLResult GetHeartBeatInfo();
bool GetPolicyBundle(const std::wstring& tenantName, std::string& policyBundle);
const SDR_WATERMARK_INFO GetWaterMarkInfo();
bool IsFileProtected(std::wstring filepath);
SDWLResult GetClassification(const uint32_t projectid, std::vector<SDR_CLASSIFICATION_CAT>& cats);
SDWLResult GetFilePath(const std::wstring &filename, std::wstring &targetfilepath);
SDWLResult DeleteSavedTokens();

```


## User Class function definition##

```
#!c++
const std::wstring GetName();
/// Get current login user name
/**
* @return
*    User name string
*/
```

```
#!c++
const std::wstring GetEmail();
/// Get current login user email address for SkyDRM
/**
* @return
*    user email string
*/
```

```
#!C++
USER_IDPTYPE GetIdpType();
/// Get current login user identify protocol type
/**
* @return
*    User IDP type
*/
```

```
#!c++
SDWLResult LogoutUser() ;
/// Logout current user
/**
* @param
*    none
* @return
*            SDWL_INVALID_DATA            Invalid logout query return
*           ERROR_INVALID_DATA          Invalid logout result
*/
```

```
#!c++
SDWLResult GetMyDriveInfo(uint64_t& usage, uint64_t& totalquota, uint64_t& vaultusage, uint64_t& vaultquota);
/// Force sync MyDrive information from RMS server
/**
* @param
*    usage          storage usage
*    totalquota     total storage available
*    vaultusage     vault usage
*    vaultquota     total vault available
* @return
*           SDWL_SUCCESS        get the current storage information.
*           SDWL_INVALID_DATA   user not login
*/
```

```
#!c++
const std::string GetPasscode() ;
/// Get current login user passcode for local login
/**
* @return
*    passcode string for current user.
*/
```

```
#!c++
SDWLResult UpdateUserInfo() ;
/// Force sync User information from RMS server
/**
* @param
*    None
* @return
*            SDWL_SUCCESS    synchronized the latest user information from RMS. 
*           SDWL_RMS_ERRORCODE_BASE+    RMS server error     
*/
```

```
#!c++
std::vector<SDR_PROJECT_INFO>& GetProjectsInfo();
/// Get projects information
/**
* @return
*    projects information.
*/
```

```
#!c++
SDWLResult UpdateMyDriveInfo();
/// Force sync MyDrive information from RMS server
/**
* @param
*    None
* @return
*            SDWL_SUCCESS    synchronized the latest MyDrive information from RMS.
*           SDWL_RMS_ERRORCODE_BASE+    RMS server error
*/
```

```
#!c++
SDWLResult ProtectFile(const std::wstring filepath, const std::vector<SDRmFileRight> rights, SDR_WATERMARK_INFO watermarkinfo, SDR_Expiration expire, const std::string& tags="", const std::string& memberid="");
/// Protect a local file
/**
* @param
*    filepath       full path to original file
*    rights         rights assigned to the nxl file
*    watermarkinfo  watermark structure
*    expire         SDR_Expiration structure
*    tags           tags
*    memberid       membership id
* @return
*           SDWL_PATH_NOT_FOUND     can't open the original file
*           SDWL_INTERNAL_ERROR     fail to create nxl file, check return message for detail info.
*
*/
```

```
#!C++
SDWLResult ShareFile(const std::wstring filepath, const std::vector<SDRmFileRight> rights, const std::vector<std::string> recipientsemail, const std::wstring & comments, SDR_WATERMARK_INFO watermarkinfo, SDR_Expiration expire, const std::string& tags="", const std::string& memberid="");
/// Share a local file
/**
* @param
*    filepath           full path to original file
*    rights             rights assigned to the nxl file
*    recipientsemail    email list of recipients who are shared file with.
*    comments           Comments for the file
*    watermarkinfo      watermark structure
*    expire             SDR_Expiration structure
*    tags               tags
*    memberid           membership id
* @return
*           SDWL_PATH_NOT_FOUND     can't open the original file
*           SDWL_INTERNAL_ERROR     fail to create nxl file, check return message for detail info.
*
*/
```

```
#!c++
SDWLResult GetRecipients(ISDRmNXLFile * nxlfile, std::vector<std::string> &recipientsemail, std::vector<std::string> &addrecipientsemail, std::vector<std::string> &removerecipientsemail);
/// Get Recipients list
/**
* @param
*    nxlfile                    nxl file handle
*    recipientsemail            email list of recipients existed
*    addrecipientsemail         email list of recipients added
*    removerecipientsemail      email list of recipients removed
* @return
*
*/
```

```
#!c++
SDWLResult UpdateRecipients(ISDRmNXLFile * nxlfile, const std::vector<std::string> addrecipientsemail, const std::vector<std::string> removerecipientsemail);
/// Update Recipients list 
/**
* @param
*    nxlfile        nxl file handle
*    addrecipientsemail            email list of recipients to add
*    removerecipientsemail        email list of recipients to remove
* @return
*
*/
```

```
#!c++
SDWLResult GetLocalFileManager(ISDRFiles** pFile);
/// Get local file manager based on current user
/**
* @param
*    pFile      return pointer to local file manager
* @return
*           SDWL_INVALID_DATA           invalid Parameter
*
*/
```

```
#!c++
SDWLResult UploadFile(ISDRmNXLFile* file);
/// upload  local file 
/**
* @param
*    file        local file to  upload
* @return
*     SDWL_INVALID_DATA            invalid Parameter
*
*/
```

```
#!c++
SDWLResult OpenFile(std::wstring nxlfilepath, ISDRmNXLFile ** file);
/// Open a local NXL file
/**
* @param
*    nxlfilepath        full path to nxl file
*    file[out]        pointer to pointer fo nxl file class handle . NULL if failed.
* @return
*           SDWL_ACCESS_DENIED          User doesn't has right to open target file
*           SDWL_RMS_ERRORCODE_BASE+    RMS server error
*/
```

```
#!c++
SDWLResult DecryptNXLFile(ISDRmNXLFile * file, std::wstring targetfilepath, SRMActivityLogOperation purpose);
/// Decrypt a local NXL file
/**
* @param
*    file               pointer to handle of nxl file class.
*    targetfilepath     full path to save the content
*    purpose            purpose to decrypt file, like to view, or to print
* @return
*           SDWL_ACCESS_DENIED          User doesn't has right to open target file
*           SDWL_RMS_ERRORCODE_BASE+    RMS server error
*/
```

```
#!c++
SDWLResult UploadActivityLogs();
/// Upload local file activity logs
/**
* @param
*    none
* @return
*            SDWL_INVALID_DATA          Invalid log query return
*            ERROR_INVALID_DATA          Invalid log result
*/
```

```
#!c++
SDWLResult GetNXLFileActivitylog(ISDRmNXLFile * file, uint64_t startPos, uint64_t count, uint8_t searchField, const std::string &searchText, uint8_t orderByField, bool orderByReverse);
/// Get file activity log
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
*            SDWL_INVALID_DATA          Invalid log query return
*            ERROR_INVALID_DATA          Invalid log result
*/
```

```
#!c++
SDWLResult GetActivityInfo(std::wstring fileName, std::vector<SDR_FILE_ACTIVITY_INFO>& info);
/// Get file activity information 
/**
* @param
*    fileName   nxl file name
*    info       file activity information
* @return
*     SDWL_NOT_FOUND                    File not found
*
*/
```

```
#!c++
SDWLResult GetListProjects(uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& searchValue, PROJECT_FILTER filter);
/// Get file activity log
/**
* @param
*    pageId     page id
*    pageSize   page size
*    orderBy    order sequence, string can be "lastActionTime" or "name".
*    searchValue search value
*    filter     filter
* @return
*            ERROR_INVALID_DATA          Invalid log result
*/
```

```
#!c++
SDWLResult ProjectDownloadFile(const unsigned int projectid, const std::wstring& pathid, const std::wstring& downloadPath, bool bviewonly);
/// Project download file
/**
* @param
*    projectid  project id
*    pathid     pathid
*    downloadPath  download file path
*    orderBy    order sequence
*    bviewonly  view only
* @return
*            ERROR_INVALID_DATA          Invalid download file result
*/
```

```
#!c++
SDWLResult GetProjectListFiles(uint32_t projectId, uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& pathId, const std::string& searchString, std::vector<SDR_PROJECT_FILE_INFO>& listFiles);
/// Get project files
/// GetListProjects() function need be called first before calling this funciton.
/**
* @param
*    projectId      project ID
*    pageId         page number (starts from 1)
*    pageSize       number of records to be returned
*    orderBy        comma-separated list of sort keys.
*    pathId         path ID
*    searchString   search-specific string
*    listFiles      return file list
* @return
*           SDWL_INVALID_DATA           Invalid project list files query return
*           ERROR_INVALID_DATA          Invalid project list files result
*/
```

```
#!c++
SDWLResult GetRights(const std::wstring& nxlfilepath, std::vector<std::pair<SDRmFileRight, std::vector<SDR_WATERMARK_INFO>>> &rightsAndWatermarks);
/// Get the rights granted to the current user, no matter the file is a central policy file or ad-hoc policy file
/**
* @param
*    nxlfilepath            full path to NXL file
*    rightsAndWatermarks    rights assigned to the NXL file, and their associated watermark obligations
* @return
*
*/
```

```
#!c++
SDWLResult GetFileRightsFromCentralPolicies(const std::wstring& nxlFilePath, std::vector<std::pair<SDRmFileRight, std::vector<SDR_WATERMARK_INFO>>> &rightsAndWatermarks);
/// Get the rights granted to the current user by central policies for the passed file.
/**
* @param
*    nxlFilePath            full path to NXL file
*    rightsAndWatermarks    rights assigned to the NXL file, and their associated watermark obligations
* @return
*           SDWL_NOT_FOUND          Not policy bundle for file's tenant found
*/
```

```
#!c++
SDWLResult GetResourceRightsFromCentralPolicies(const std::wstring& resourceName, const std::wstring& resourceType, const std::vector<std::pair<std::wstring, std::wstring>> &attrs, std::vector<std::pair<SDRmFileRight, std::vector<SDR_OBLIGATION_INFO>>> &rightsAndObligations);
/// Get the rights granted to the current user by central policies for the passed resource.
/**
* @param
*    resourceName           name of resource
*    resourceType           type of resource (e.g. "fso", "portal")
*    attrs                  resource attributes
*    rightsAndObligations   rights assigned to the resource, and their associated obligations
* @return
*           SDWL_NOT_FOUND          Not policy bundle for current user's tenant found
*/
```

```
#!c++
SDWLResult GetHeartBeatInfo();
/// Get heart beat infomation 
/**
* @param
*    none
* @return
*     SDWL_INVALID_DATA          Invalid heart beat query return
*     ERROR_INVALID_DATA          Invalid heart beat result
*
*/
```

```
#!c++
SDWLResult bool GetPolicyBundle(const std::wstring& tenantName, std::string& policyBundle);
///  Get policy bundle 
/**
* @param
*    tenantName  tenant name
*    policyBundle  policy bundle
* @return
*     success return true, else return false
*
*/
```

```
#!c++
const SDR_WATERMARK_INFO GetWaterMarkInfo();
///  Get water mark info 
/**
* @param
*    none
* @return
*     SDR_WATERMARK_INFO structure
*
*/
```

```
#!c++
bool IsFileProtected(std::wstring filepath);
/// Check file is protected or not
/**
* @param
*    filepath   full path to file 
* @return
*           if it's nxl file return true, otherwise return false
*/
```

```
#!c++
SDWLResult GetClassification(const uint32_t projectid, std::vector<SDR_CLASSIFICATION_CAT>& cats);
/// Get Classification Profile
/**
* @param
*    projid     project id
* @return
*           SDWL_INVALID_DATA       Invalid heart beat query return
*           ERROR_INVALID_DATA      Invalid heart beat result
*/
```

```
#!c++
SDWLResult GetFilePath(const std::wstring &filename, std::wstring &targetfilepath);
	/// Get file path from file name
	/**
	* @param
	*    filename  file name
	* @return
	*            SDWL_INVALID_DATA       Invalid data
	*            SDWL_NOT_FOUND          File is not in the working directory
	*
	*/

```

```
#!c++
SDWLResult DeleteSavedTokens();
	/// Delete saved tokens
	/**
	* @return
	*            SDWL_INVALID_DATA       Invalid data
	*
	*/

```