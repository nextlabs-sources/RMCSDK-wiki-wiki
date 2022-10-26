[HOME](Home)
# RMCCore SDK RMMyProjects interface #

## RMMyProjects Interface class definition ##
```
#!c++

namespace RMCCORE {
        class RMProjectMember : public RestfulBase
	{
	public:
		RMProjectMember();
		~RMProjectMember();

	public:
		unsigned int GetUserID(void) const { return m_userid; }
		std::string GetUserName(void) const { return m_username; }
		std::string GetUserEmail(void) const { return m_useremail; }
		uint64_t	GetJoinTime(void) const { return m_jointime; }
	public: //function inherit from RestfulBase
		RetValue ImportFromJson(JsonObject * value);
		RetValue ImportFromString(std::string jsonstr);

		const std::string ExportToString(void);
		JsonValue * ExportToJson(void);

		RetValue ImportFromRMSResponse(JsonObject * root);
		RetValue ImportFromRMSResponse(std::string jsonstr);
	};

	typedef enum {
		TRIALPROJECT = 0,
		PROJECT,
		ENTERPRISEPROJECT
	}ProjectType;
	typedef enum  {
		ALL = 0,
		OWNEDBYME,
		OWNEDBYOTHER
	} PROJECTFILTER;

	class RMProject : public RestfulBase
	{
	public:
		RMProject();
		~RMProject();
	public:
		bool IsInitialized(void) { return m_initialized; }
		unsigned int GetProjectID(void) const { return m_projid; }
		const std::string & GetProjectName(void) const { return m_name; }
		const std::string & GetDisplayName(void) const { return m_displayname; }
		const std::string & GetDescription(void) const { return m_description; }

		bool IsOwnbyMe(void) const { return m_bowner; }
		ProjectType GetPrjectType(void) const { return m_type; }
		
		unsigned int GetOwnerID(void) const { return m_ownerid; }
		const std::string & GetOwnerName(void) const { return m_ownername; }
		const std::string & GetOwnerEmail(void) const { return m_owneremail; }

		const RMProjectFiles* GetProjectFiles() { return &m_projectFiles; };

		RMProject& operator = (const RMProject& rhs);


	public: //function inherit from RestfulBase
		RetValue ImportFromJson(JsonObject * value);
		RetValue ImportFromString(std::string jsonstr);

		const std::string ExportToString(void);
		JsonValue * ExportToJson(void);

		RetValue ImportFromRMSResponse(JsonObject * root);
		RetValue ImportFromRMSResponse(std::string jsonstr);

		// project files list
		const HTTPRequest &GetListFilesQuery(unsigned int projectId, uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& pathId, const std::string& searchString);
	
		RetValue Initialize(const RMSystemPara &sys, const RMTenant & tenant, unsigned int userid, const std::string ticket);
	};


        class RMMyProjects : public RestfulBase
        {
	public:
		RMMyProjects();
		~RMMyProjects();

		bool IsInitialized(void) { return m_initialized; }
	public:
		size_t	GetProjectNumber(void) { return m_projectlist.size(); }
		const RMProject* GetProject(uint32_t numbr);
		

	public: //function inherit from RestfulBase
		RetValue ImportFromJson(JsonObject * value);
		RetValue ImportFromString(std::string jsonstr);

		const std::string ExportToString(void);
		JsonValue * ExportToJson(void);

		RetValue ImportFromRMSResponse(JsonObject * root);
		RetValue ImportFromRMSResponse(std::string jsonstr);
	public://Project API
		const HTTPRequest &GetListProjectsQuery(uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& searchValue, PROJECTFILTER filter);
		const HTTPRequest &GetDownloadFileQuery(const RMProject &project, const std::string & filepath, bool bviewonly);
};
}
```


## RMProjectMember Interface Functions ##
```

	const bool IsInitialized();/// if the class is initialized
	/**
	* @parameter
        *     None. 
	*/
Note: need call this function to validate the data before use it.
```
```
	unsigned int GetUserID();/// user id
	/**
	* @return
	*    user id
	*/
```
```
	const std::string GetUserName();/// user name
	/**
	* @return
	*   string of user name
	*/
```
```
	const std::string GetUserEmail();/// user email
	/**
	* @return
	*   string of user email
	*/
```
```
	uint64_t GetJoinTime();/// join time
	/**
	* @return
	*    join time
	*/
```
```
	RetValue ImportFromRMSResponse(std::string jsonstr);///Import project member value return from RMS retrieve project member API
	/**
	* @param
        *    jsonstr  Json string returned from RMS project member interface
	* @return
	*    0 if import successfully.
	*/
Note: ImportFromRMSResponse function only fill in the project member 
```


## RMProject Interface Functions ##

```
	const bool IsInitialized();/// if the class is initialized
	/**
	* @parameter
        *     None. 
	*/
Note: need call this function to validate the data before use it.
```
```
	unsigned int GetProjectID();/// project id
	/**
	* @return
	*    project id
	*/
```

```
#!c++
	const std::string GetProjectName();/// project name
	/**
	* @return
	*   string of project name
	*/
```

```
#!c++
	const std::string GetDisplayName();/// project display name
	/**
	* @return
	*   string of project display name
	*/
```
```
#!c++
	const std::string GetDescription();/// project description 
	/**
	* @return
	*   string of project description 
	*/
```
```
#!c++
	ProjectType GetPrjectType();/// project type
	/**
	* @return
	*    project type
	*/
```
```
#!c++
	unsigned int GetOwnerID;/// owner id
	/**
	* @return
	*    project owner id
	*/
```
```
#!c++
	const std::string GetOwnerName();/// project owner name
	/**
	* @return
	*   string of project owner name
	*/
```
```
#!c++
	const std::string GetOwnerEmail();/// project owner email
	/**
	* @return
	*   string of project owner email
	*/
```
```
#!c++
	const RMProjectFiles* GetProjectFiles();/// get project files
	/**
	* @return
	*   RMProjectFiles*
	*/
```
```
#!c++
	const HTTPRequest &GetListFilesQuery(unsigned int projectId, uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& pathId, const std::string& searchString);
/// Get HTTP Request for list files query
	/**
        * @param
        *    projectId  project id
        *    pageId     page id
        *    pageSize   page size
        *    orderBy    order sequence
        *    pathId     path id
        *    searchString    search string
	* @return
	*   HTTPRequest class
	*/
```
```
#!c++
	RetValue ImportFromRMSResponse(std::string jsonstr);///Import project value return from RMS retrieve project API
	/**
	* @param
        *    jsonstr  Json string returned from RMS project member interface
	* @return
	*    0 if import successfully.
	*/
Note: ImportFromRMSResponse function only fill in the project 
```


## RMMyProjects Interface Functions ##
```
	const bool IsInitialized();/// if the class is initialized
	/**
	* @parameter
        *     None. 
	*/
Note: need call this function to validate the data before use it.
```
```
#!c++
	size_t	GetProjectNumber();/// total project number
	/**
	* @return
	*    total project number
	*/
```
```
#!c++
	const RMProject* GetProject(uint32_t numbr);/// get project class
	/**
	* @return
	*    project class
	*/
```
```
#!c++
	RetValue ImportFromRMSResponse(std::string jsonstr);///Import projects value return from RMS retrieve projects API
	/**
	* @param
        *    jsonstr  Json string returned from RMS projects interface
	* @return
	*    0 if import successfully.
	*/
Note: ImportFromRMSResponse function only fill in the project 
```
```
#!c++
	const HTTPRequest &GetListProjectsQuery(uint32_t pageId, uint32_t pageSize, const std::string& orderBy, const std::string& pathId, const std::string& searchValue, PROJECTFILTER filter);
/// Get HTTP Request for list files query
	/**
        * @param
        *    pageId     page id
        *    pageSize   page size
        *    orderBy    order sequence
        *    pathId     path id
        *    searchValue search value
        *    filter     filter
	* @return
	*   HTTPRequest class
	*/
```
```
#!c++
	const HTTPRequest &GetDownloadFileQuery(const RMProject &project, const std::string & filepath, bool bviewonly);
/// Get HTTP Request for download file query
	/**
        * @param
        *    project    project class
        *    filepath   file path
        *    bviewonly  view only
	* @return
	*   HTTPRequest class
	*/
```