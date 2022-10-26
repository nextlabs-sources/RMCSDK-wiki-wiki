[HOME](Home)
# SDWL Instance Interface for SkyDRM instance #

To obtain instance interface handler, Call [Library Interface](SDWL_Interface) function
```C++
SDWLResult SDWLibCreateSDRmcInstance(const CHAR * productName, uint32_t productMajorVer, uint32_t productMinorVer, uint32_t productBuild, const WCHAR * sdklibfolder, const WCHAR * tempfolder, ISDRmcInstance ** pInstance);
```

## Instance Class ##

Application to use sdk need call instance class first to access all other classes. Application need pass the router, working folder information.
sdk will save all information, such as user, token, ... under the working folder.

```
#!c++
SDWLResult Initialize(std::wstring router, std::wstring tenant);
	/// Initialize RMCInstance Class
	/**
	 * @pre
	 *    Call API function SDWLibCreateSDRmcInstance to obtain handle of RMCInstance Class
	 * @param
	 *    router	router URL for registered tenant. if empty, default value will be used.
	 *    tenant	tenant id string. if empty, default value will be used
	 * @return
	 *    Result: return RESULT(0) when success
	 *			SDWL_CERT_NOT_READY			certificate is not installed/fail to installed
	 *			SDWL_RMS_ERRORCODE_BASE+	RMS server error
	 */
```

```
#!c++
SDWLResult Initialize(std::wstring workingfolder, std::wstring router, std::wstring tenant);
	/// Initialize RMCInstance Class
	/**
	* @pre
	*    Call API function SDWLibCreateSDRmcInstance to obtain handle of RMCInstance Class
	* @param
	*    workingfolder	file folder string to save SDWLInstance internal data files. if no working folder is set
	*					the data files will be saved at temporary folder set at SDWLibCreateSDRmcInstance() 
	*    router			router URL for registered tenant. if empty, default value will be used.
	*    tenant			tenant id string. if empty, default value will be used
	* @return
	*    Result: return RESULT(0) when success
	*			SDWL_PATH_NOT_FOUND			invalid working folder
	*			SDWL_CERT_NOT_READY			certificate is not installed/fail to installed
	*			SDWL_RMS_ERRORCODE_BASE+	RMS server error
	*/
```

```
#!c++
	SDWLResult IsInitFinished(bool& finished);
	/// Check if RMCInstance Class has finished initialization
	/**
	 * @pre
	 *    Initialize() function need be called before calling this funciton
	 * @param
	 *    bool			on success, true if initialization has finished, false if initialization still in progess.
	 * @return
	 *    Result: return RESULT(0) when success
	 */
```

```
#!c++
	SDWLResult CheckSoftwareUpdate(std::string &newVersionStr, std::string &downloadURL, std::string &checksum);
	/// Check if there is a different (either newer or older) version of the software on the server for the current tenant that can be downloaded for updating
	/**
	 * @pre
	 *    SDWLibCreateSDRmcInstance() function needs to be called with productName, productMajorVer, productMinorVer, and productBuild
	 *    IsInitFinished() function need be called before calling this funciton
	 * @param
	 *    newVersionStr	return version string of the software on the server, if any
	 *    downloadURL	return URL for downloading the software, if any
	 *    checksum		return SHA1 checksum of the download package, if any
	 * @return
	 *    Result: return RESULT(0) when the checking is successful (It does not necessarily mean that there is a version available for downloaded.)
	 */
```

```
#!c++
SDWLResult Save(std::wstring folder = L"");
	/// Save SDWLInstance internal data files to specified folder
	/**
	 * @pre
	 *    Intialize() function need be called before calling this funciton
	 * @param 
	 *    folder		file folder string to save SDWLInstance internal data files. if no working folder is set
	 *					the data files will be saved at temporary folder set at SDWLibCreateSDRmcInstance().
	 *					if empty, the workingfolder or temporary folder will be used.
	 *					Note: if no working folder is set, only tenant related information will be saved.
	 * @return
	 *			SDWL_PATH_NOT_FOUND			invalid working folder
	 */
```

```
#!c++
SDWLResult GetCurrentTenant(ISDRmTenant ** ptenant);
	/// Get Current Tenant information
	/**
	* @pre
	*    Intialize() function need be called before calling this funciton
	* @param
	*    ptenant		pointer to current using tenant class
	* @return
	*			SDWL_NOT_FOUND				initialize tenant failed. check the return code of Initialize() for more detail
	*/
```

```
#!c++
SDWLResult GetLoginRequest(ISDRmHttpRequest **prequest) = 0;
	/// Get user login http request information based on current Tenant
	/**
	* @pre
	*    Intialize() function need be called before calling this funciton
	* @param
	*    prequest		pointer to SkyDRM User Login http request information
	* @return
	*			SDWL_INVALID_DATA			invalid tenant information. check return message or return code of Initialize() for more detail
	*			
	*/
```

```
#!C++
SDWLResult SetLoginResult(std::string jsonreturn, ISDRmUser **puser);
	/// Set Json return from User Login Request
	/**
	 * @pre
	 *    This instance should not have been used for a different user earlier.
	 *    Intialize() function need be called before calling this funciton.
	 * @param
	 *	  jsonreturn	Returned JSON string from SkyDRM user login http request
	 *    puser			pointer to User interface 
	 * @return
	 *			SDWL_INVALID_DATA			invalid tenant information. check return message or return code of Initialize() for more detail
	 *          SDWL_INVALID_JSON_FORMAT	invalid json string
	 *			SDWL_RMS_ERRORCODE_BASE+	RMS server error	 *
	 */
```

```
#!C++
SDWLResult GetLoginUser(const std::string useremail, const std::string passcode, ISDRmUser **puser);
	/// Get previous login user session
	/**
	 * @pre
	 *    IsInitFinished() function need be called before calling this funciton
	 * @param
	 *	  useremail		user email string of login user
	 *     passcode		passcode assigned to login user account
	 *    puser			pointer to User interface
	 * @return
	 *			SDWL_INVALID_DATA			invalid user email or passcode
	 *           SDWL_LOGIN_REQUIRED			User session timeout, need login again
	 */
```

```
#!C++
bool IsRPMDriverExist();
	/// Check if RPM driver is installed
	/**
	 * @param
	 *	  none
	 * @return
	 *	  return true when driver is installed, otherwise return false
	 */
```

```
#!C++
SDWLResult AddRPMDir(std::wstring filepath);
	/// Add directory for RPM
	/**
	 * @param
	 *	  filepath		directory
	 * @return
	 *	  SDWL_INVALID_DATA			invalid file path
	 *	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	 */
```

```
#!C++
SDWLResult RemoveRPMDir(std::wstring filepath);
	/// Remove directory for RPM
	/**
	 * @param
	 *	  filepath		directory
	 * @return
	 *	  SDWL_INVALID_DATA			invalid file path
	 *	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	 */
```

```
#!C++
SDWLResult SetRPMClientId(std::string clientid);
	/// Set clientid for RPM
	/**
	 * @param
	 *	  clientid		client id
	 * @return
	 *	  SDWL_INVALID_DATA			invalid file path
	 *	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	 */
```

```
#!C++
SDWLResult SetRPMLoginResult(std::string jsonreturn);
	/// Send login data to RPM
	/**
	 * @pre
 	 *     must call SetRPMClientId() first
	 * @param
	 *	  jsonreturn		login data
	 * @return
	 *	  SDWL_INVALID_DATA			invalid file path
	 *	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	 */
```

```
#!C++
SDWLResult RPMLogout();
	/// logout RPM
	/**
	 * 
	 * @return
	 *	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	 */
```

```
#!C++
SDWLResult SetRPMPolicyBundle();
	/// Send policy bundle to RPM
	/**
	*
	* @return
	*	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	*/
```

```
#!C++
SDWLResult SetRPMServiceStop(bool enable=true);
	/// enable or disable RPM stop service
	/**
	 * @param
	 *	  enable		stop service enable (true) or disable (false)
	 * @return
	 *	  SDWL_INVALID_DATA			invalid data
	 *	  SDWL_CERT_NOT_READY         RPM driver/service is not ready
	 */
```

```
#!C++
const std::string  GetLoginData();
	/// Get previous login data
	/**
	*
	* @return
	*			std::string         String is not empty if success.
	*/
```

```
#!C++
SDWLResult SetRPMDeleteCacheToken();
	/// Delete RPM cache token
	/**
	*
	* @return
	*			SDWL_CERT_NOT_READY         RPM driver/service is not ready
	*/

```

```
#!C++
SDWLResult RPMDeleteFileToken(const std::wstring &filePath);
	/**
	* @pre
	*    SetLoginResult()/SetRPMLoginResult function need be called before calling this funciton
	*
	* @return
	*			SDWL_ACCESS_DENIED			RPM driver is not ready
	*           SDWL_LOGIN_REQUIRED			User session timeout, need login again
	*/


```