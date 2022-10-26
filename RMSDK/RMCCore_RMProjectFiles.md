[HOME](Home)
# RMCCore RMProjectFiles interface #

## RMProjectFiles Interface class definition ##
```
#!c++

	class RMProjectFile : public RestfulBase
	{
	public:
		RMProjectFile();
		~RMProjectFile();

	public:
		unsigned int GetUserID(void) const { return m_userid; }
		std::string GetDisplayName(void) const { return m_displayname; }
		std::string GetUserEmail(void) const { return m_owneremail; }

	public: //function inherit from RestfulBase
		RetValue ImportFromJson(JsonObject * value);
		RetValue ImportFromString(std::string jsonstr);

		const std::string ExportToString(void);
		JsonValue * ExportToJson(void);

		RetValue ImportFromRMSResponse(JsonObject * root);
		RetValue ImportFromRMSResponse(std::string jsonstr);
	};

	class RMProjectFiles : public RestfulBase
	{
	public:
		RMProjectFiles();
		~RMProjectFiles();

	protected:
		RetValue Initialize(const RMSystemPara &sys, const RMTenant & tenant, unsigned int userid, const std::string ticket);

	public: //function inherit from RestfulBase
		RetValue ImportFromJson(JsonObject * value);
		RetValue ImportFromString(std::string jsonstr);

		const std::string ExportToString(void);
		JsonValue * ExportToJson(void);

		RetValue ImportFromRMSResponse(JsonObject * root);
		RetValue ImportFromRMSResponse(std::string jsonstr);
	};

}
```

## RMProjectFile Interface Functions ##
```

	unsigned int GetUserID();/// user id
	/**
	* @return
	*    user id
	*/
```
```
	const std::string GetDisplayName();/// display name
	/**
	* @return
	*   string of display name
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
	RetValue ImportFromRMSResponse(std::string jsonstr);///Import project file value return from RMS retrieve project file API
	/**
	* @param
        *    jsonstr  Json string returned from RMS project member interface
	* @return
	*    0 if import successfully.
	*/
Note: ImportFromRMSResponse function only fill in the project file
```

## RMProjectFiles Interface Functions ##

```
	const bool IsInitialized();/// if the class is initialized
	/**
	* @parameter
        *     None. 
	*/
Note: need call this function to validate the data before use it.
```
```
	RetValue ImportFromRMSResponse(std::string jsonstr);///Import project files value return from RMS retrieve project files API
	/**
	* @param
        *    jsonstr  Json string returned from RMS project member interface
	* @return
	*    0 if import successfully.
	*/
Note: ImportFromRMSResponse function only fill in the project files
```