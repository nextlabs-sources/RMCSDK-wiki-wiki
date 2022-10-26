[HOME](Home)
# RMCCore SDK Recipients interface #
Recipients class is based on following Restful API from RMS
[Update recipients from a document](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Sharing%20REST%20API#markdown-header-update-recipients-from-a-document)

## Recipients Interface class definition ##
```
#!c++
namespace RMSDK {
    typedef std::vector<std::string> RMRecipientList;
    
    class RMRecipients : public RestfulBase
    {
    public:
        RMRecipients();
        ~RMRecipients();
    public:
        const RMRecipientList GetRecipients(void);
        const RMRecipientList GetAddRecipients(void);
        const RMRecipientList GetRemoveRecipients(void);
        const std::string GetComments(void);
        
        uint8_t AddRecipients(RMRecipientList recipients);
        uint8_t RemoveRecipients(RMRecipientList recipients);
    public:
        bool NeedUpdateRMS(void);
        RMRecipients& operator = (const RMRecipients& rhs);

        void UpdateComments(const std::string comments);
    public:
        RetValue ImportFromRMSResponse(JsonObject * root);
        RetValue ImportFromRMSResponse(std::string jsonstr);

    public: //function inherit from RestBase
        RetValue ImportFromJson(JsonObject * value);
        RetValue ImportFromString(std::string jsonstr);
        
        const std::string ExportToString(void);
        JsonValue * ExportToJson(void);
    };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##


## Recipients Interface Functions ##
```
#!c++
	RMRecipients();/// constructor
	/**
	* @param
	*    None
	*/
```

```
#!c++
	const RMRecipientList GetRecipients(void);/// Get current Recipients list
	/**
	* @return
	*    Recipients list which has been sent to RMS
	*/
```

```
#!c++
	const RMRecipientList GetRemoveRecipients(void);/// Get Removed Recipients list
	/**
	* @return
	*    Recipients list for removing which has NOT been sent to RMS
	*/
```
```
#!c++
	const RMRecipientList GetAddRecipients(void);/// Get Added Recipients list
	/**
	* @return
	*    Recipients list for adding which has NOT been sent to RMS
	*/
```
```
#!c++

	const std::string GetComments(void);/// Get comments for adding/removing list 
	/**
	* @return
	*    Comments string which has NOT been sent to RMS
	*/
```

```
#!C++

	uint8_t AddRecipients(RMRecipientList recipients);
        /// Update Adding Recipients list 
	/**
	* @param 
	*    recipients recipients list to add
	* @return 
	*    number of recipients added
	*/
```
```
#!C++

	uint8_t RemoveRecipients(RMRecipientList recipients);
        /// Update Removing Recipients list 
	/**
	* @param 
	*    recipients recipients list to remove
	* @return 
	*    number of recipients removed
	*/
```

```
#!c++
	bool NeedUpdateRMS(void);
        /// if there is adding/removing recipient list not sync with RMS
	/**
	* @return
        *    true if the recipient list need sync to RMS
	*/
Note: call HTTP Helper function to sync recipient to RMS.
```

```
#!c++
	void UpdateComments(const std::string comments);/// Update comments
	/**
	* @param
	*    comments  comments string need send to RMS alone with update recipients list
	*/
Note: the previous comments will be overwritten if it is not synced with RMS
```